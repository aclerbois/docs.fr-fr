---
title: "Implémentation du modèle asynchrone basé sur des tâches"
ms.date: 06/14/2017
ms.prod: .net
ms.technology: dotnet-clr
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: fab6bd41-91bd-44ad-86f9-d8319988aa78
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 3e61b0c94b1512509008d67017389fa11f938999
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="implementing-the-task-based-asynchronous-pattern"></a>Implémentation du modèle asynchrone basé sur des tâches
Vous pouvez implémenter le modèle asynchrone basé sur des tâches (TAP) de trois façons : à l’aide des compilateurs C# et Visual Basic dans Visual Studio, manuellement, ou par une combinaison des méthodes du compilateur et des méthodes manuelles. Les sections suivantes abordent chacune de ces méthodes en détail. Vous pouvez utiliser le modèle TAP pour implémenter des opérations asynchrones liées aux calculs et e/S. Le [les charges de travail](#workloads) section décrit chaque type d’opération.

## <a name="generating-tap-methods"></a>Génération de méthodes TAP

### <a name="using-the-compilers"></a>L’aide des compilateurs
En commençant par [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], toute méthode qui est attribuée à la `async` (mot clé) (`Async` en Visual Basic) est considéré comme une méthode asynchrone, les compilateurs c# et Visual Basic effectuent les transformations nécessaires pour implémenter le méthode de façon asynchrone à l’aide de drainage. Une méthode asynchrone doit retourner un objet <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> ou <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>. Dans le second cas, le corps de la fonction doit retourner un `TResult`, le compilateur garantit ensuite que ce résultat est rendu disponible via l’objet de tâche qui en résulte. De même, toutes les exceptions non gérées dans le corps de la méthode sont marshalées vers la tâche de sortie et provoquent la fin de la tâche résultante avec l'état <xref:System.Threading.Tasks.TaskStatus.Faulted?displayProperty=nameWithType>. Une exception est levée quand un <xref:System.OperationCanceledException> (ou un type dérivé) n'est pas géré, auquel cas la tâche qui en résulte se termine avec l'état <xref:System.Threading.Tasks.TaskStatus.Canceled?displayProperty=nameWithType>.

### <a name="generating-tap-methods-manually"></a>Générer manuellement les méthodes TAP
Vous pouvez implémenter le modèle TAP manuellement pour mieux contrôler l’implémentation. Le compilateur s'appuie sur la surface publique exposée depuis l'espace de noms <xref:System.Threading.Tasks?displayProperty=nameWithType> et sur les types de prise en charge de l'espace de noms <xref:System.Runtime.CompilerServices?displayProperty=nameWithType>. Pour implémenter le modèle TAP vous-même, créez un objet <xref:System.Threading.Tasks.TaskCompletionSource%601>, effectuez l'opération asynchrone, et lorsqu'elle est terminée, appelez la méthode <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A> ou <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A>, ou bien la version `Try` de l'une de ces méthodes. Quand vous implémentez une méthode TAP manuellement, vous devez achever la tâche qui en résulte quand l'opération asynchrone représentée se termine. Exemple :

[!code-csharp[Conceptual.TAP_Patterns#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#1)]
[!code-vb[Conceptual.TAP_Patterns#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#1)]

### <a name="hybrid-approach"></a>Approche hybride
 Il peut s’avérer utile d’implémenter le modèle TAP manuellement pour déléguer la logique de base de l’implémentation du compilateur. Par exemple, vous pouvez utiliser l'approche hybride pour vérifier des arguments en dehors d'une méthode asynchrone générée par le compilateur, pour que les exceptions puissent être échappées vers l'appelant direct de la méthode, plutôt que d'être exposées par un objet <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> :

 [!code-csharp[Conceptual.TAP_Patterns#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#2)]
 [!code-vb[Conceptual.TAP_Patterns#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#2)]

 La délégation est également utile quand vous implémentez une optimisation de chemin d'accès rapide et souhaitez retourner une tâche mise en cache.

## <a name="workloads"></a>Charges de travail
Vous pouvez implémenter des opérations asynchrones liées aux calculs et liées aux E/S en tant que méthodes TAP. Toutefois, quand des méthodes TAP sont exposées publiquement depuis une bibliothèque, elles doivent uniquement être fournies pour les charges de travail qui impliquent des opérations d'E/S (elles peuvent également impliquer des calculs, mais ne doivent pas consister uniquement de calculs). Si une méthode est entièrement liée, elle doit être exposée uniquement en tant qu’une implémentation synchrone. Le code qui la consomme peut ensuite décider s’il faut encapsuler un appel de cette méthode synchrone dans une tâche pour décharger le travail vers un autre thread ou pour atteindre un parallélisme. Et si une méthode est lié aux e/s, elle doit être exposée uniquement en tant qu’une implémentation asynchrone.

### <a name="compute-bound-tasks"></a>Tâches liées aux calculs
La classe <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> convient parfaitement aux opérations de calcul intensives. Par défaut, elle tire parti de la prise en charge spéciale de la classe <xref:System.Threading.ThreadPool> pour assurer une exécution efficace. Elle permet également de contrôler de manière précise le moment, l'endroit et la manière dont sont exécutés les calculs asynchrones.

Vous pouvez générer des tâches liées au calcul de la manière suivante :

- Dans le .NET Framework 4, utilisez la méthode <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> qui accepte un délégué (en général un <xref:System.Action%601> ou un <xref:System.Func%601>) devant être exécuté de façon asynchrone. Si vous fournissez un délégué <xref:System.Action%601>, la méthode retourne un objet <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> qui représente l'exécution asynchrone de ce délégué. Si vous fournissez un délégué <xref:System.Func%601>, la méthode retourne un objet <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>. Les surcharges de la méthode <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> acceptent un jeton d'annulation, (<xref:System.Threading.CancellationToken>), des options de création de tâche (<xref:System.Threading.Tasks.TaskCreationOptions>) et un planificateur de tâches (<xref:System.Threading.Tasks.TaskScheduler>) qui permettent un contrôle précis de la planification et de l'exécution de la tâche. Une instance de fabrique qui cible le planificateur de tâches actuel est disponible sous la forme d'une propriété statique (<xref:System.Threading.Tasks.Task.Factory%2A>) de la classe<xref:System.Threading.Tasks.Task>, par exemple `Task.Factory.StartNew(…)`.

- Dans le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] et versions ultérieures (y compris .NET Core et .NET Standard), utilisez la méthode statique <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> un raccourci vers la méthode <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType>. Vous pouvez utiliser <xref:System.Threading.Tasks.Task.Run%2A> pour lancer facilement une tâche liée aux calculs qui cible le pool de threads. Dans le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] et versions ultérieures, il s’agit du moyen privilégié de lancer une tâche liée. Utilisez `StartNew` directement que lorsque vous souhaitez un contrôle plus précis sur la tâche.

- Utilisez les constructeurs du type `Task` ou de la méthode `Start` pour générer et planifier la tâche séparément. Les méthodes publiques doivent retourner uniquement les tâches qui ont déjà été lancées.

- Utilisez les surcharges de la méthode <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType>. Cette méthode crée une nouvelle tâche qui est planifiée quand l'exécution d'une autre tâche se termine. Certaines surcharges <xref:System.Threading.Tasks.Task.ContinueWith%2A> acceptent un jeton d'annulation, des options de continuation et un planificateur de tâches pour un meilleur contrôle de la planification et de l'exécution de la tâche de continuation.

- Utilisez le <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A?displayProperty=nameWithType> et <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A?displayProperty=nameWithType> méthodes. Ces méthodes créent une nouvelle tâche qui est planifiée quand une partie ou l’intégralité d’un ensemble de tâches fourni se termine. Ces méthodes fournissent également des surcharges permettant de contrôler la planification et l’exécution de ces tâches.

Dans les tâches liées aux calculs, le système peut empêcher l’exécution d’une tâche planifiée s’il reçoit une demande d’annulation avant l’exécution de la tâche. Par conséquent, si vous fournissez un jeton d'annulation (un objet <xref:System.Threading.CancellationToken>), vous pouvez passer ce jeton au code asynchrone qui surveille le jeton. Vous pouvez également fournir le jeton pour l'une des méthodes mentionnées précédemment telles que `StartNew` ou `Run`, pour que le runtime `Task` puisse également surveiller le jeton.

Prenons, par exemple, une méthode asynchrone qui génère le rendu d'une image. Le corps de la tâche peut interroger le jeton d'annulation pour que l'exécution du code puisse s'arrêter plus tôt si une demande d'annulation arrive pendant le rendu. De plus, si la demande d'annulation arrive avant le début du rendu, vous pourrez empêcher l'opération de rendu :

[!code-csharp[Conceptual.TAP_Patterns#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#3)]
[!code-vb[Conceptual.TAP_Patterns#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#3)]

Les tâches liées aux calculs se terminent avec l'état <xref:System.Threading.Tasks.TaskStatus.Canceled> si au moins l'une des conditions suivantes est remplie :

- Une demande d'annulation arrive via l'objet <xref:System.Threading.CancellationToken>, qui est fourni en tant qu'argument à la méthode de création (par exemple, `StartNew` ou `Run`) avant que la tâche ne passe à l'état <xref:System.Threading.Tasks.TaskStatus.Running>.

- Une exception <xref:System.OperationCanceledException> n'est pas gérée dans le corps d'une telle tâche. Cette exception contient le même <xref:System.Threading.CancellationToken> qui est passé à la tâche et ce jeton indique qu'une annulation a été demandée.

Si une autre exception n'est pas gérée dans le corps de la tâche, la tâche se termine avec l'état <xref:System.Threading.Tasks.TaskStatus.Faulted>, et toute tentative d'attendre la tâche ou d'accéder à son résultat provoque la levée d'une exception.

### <a name="io-bound-tasks"></a>Tâches d’e/S
Pour créer une tâche qui ne doit pas être sauvegardée directement par un thread pour l'intégralité de son exécution, utilisez le type <xref:System.Threading.Tasks.TaskCompletionSource%601>. Ce type expose une propriété <xref:System.Threading.Tasks.TaskCompletionSource%601.Task%2A> qui retourne une instance <xref:System.Threading.Tasks.Task%601> associée. Le cycle de vie de cette tâche est contrôlé par les méthodes <xref:System.Threading.Tasks.TaskCompletionSource%601> telles que <xref:System.Threading.Tasks.TaskCompletionSource%601.SetResult%2A>, <xref:System.Threading.Tasks.TaskCompletionSource%601.SetException%2A> et <xref:System.Threading.Tasks.TaskCompletionSource%601.SetCanceled%2A>, et leurs variantes `TrySet`.

Supposons que vous vouliez créer une tâche devant se terminer après une période spécifiée. Par exemple, vous pouvez vouloir différer une activité dans l'interface utilisateur. La classe <xref:System.Threading.Timer?displayProperty=nameWithType> fournit déjà la possibilité d'appeler un délégué de façon asynchrone après une période donnée, et grâce à <xref:System.Threading.Tasks.TaskCompletionSource%601>, vous pouvez ajouter un <xref:System.Threading.Tasks.Task%601> au minuteur, par exemple :

[!code-csharp[Conceptual.TAP_Patterns#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#4)]
[!code-vb[Conceptual.TAP_Patterns#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#4)]

Depuis le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], la méthode <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> est fournie à cet effet, et peut être utilisée dans une autre méthode asynchrone, par exemple, pour implémenter une boucle d'interrogation asynchrone :

[!code-csharp[Conceptual.TAP_Patterns#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#5)]
[!code-vb[Conceptual.TAP_Patterns#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#5)]

La classe <xref:System.Threading.Tasks.TaskCompletionSource%601> ne possède pas d'équivalent non générique. Toutefois, <xref:System.Threading.Tasks.Task%601> dérive de <xref:System.Threading.Tasks.Task>. Vous pouvez donc utiliser l'objet <xref:System.Threading.Tasks.TaskCompletionSource%601> générique pour les méthodes d'E/S qui ne font que retourner une tâche. Pour ce faire, vous pouvez utiliser une source avec un `TResult` factice (<xref:System.Boolean> est un bon choix par défaut, mais si vous avez peur que l'utilisateur de la <xref:System.Threading.Tasks.Task> en fasse une classe de base <xref:System.Threading.Tasks.Task%601>, vous pouvez utiliser un type `TResult` privé à la place). Par exemple, la méthode `Delay` de l'exemple précédent retourne l'heure actuelle, ainsi que le décalage résultant (`Task<DateTimeOffset>`). Si une telle valeur n'est pas nécessaire, la méthode peut être codée comme suit (notez le changement du type de retour et le remplacement de l'argument par <xref:System.Threading.Tasks.TaskCompletionSource%601.TrySetResult%2A>) :

[!code-csharp[Conceptual.TAP_Patterns#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#6)]
[!code-vb[Conceptual.TAP_Patterns#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#6)]

### <a name="mixed-compute-bound-and-io-bound-tasks"></a>Tâches liées aux calculs et aux e/S mixtes
Les méthodes asynchrones peuvent comprendre à la fois des opérations de calcul et d'E/S. En réalité, les opérations asynchrones sont souvent combinées au sein de plus grandes opérations mixtes. Par exemple, la méthode `RenderAsync` de l'exemple précédent permettait d'exécuter une opération de calcul intensive pour restituer une image basée sur des `imageData` d'entrée. Ces `imageData` peuvent provenir d'un service web auquel vous pouvez accéder de manière asynchrone :

[!code-csharp[Conceptual.TAP_Patterns#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap_patterns/cs/patterns1.cs#7)]
[!code-vb[Conceptual.TAP_Patterns#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap_patterns/vb/patterns1.vb#7)]

Cet exemple montre également comment un jeton d'annulation peut être associé à un thread par l'intermédiaire de plusieurs opérations asynchrones. Pour plus d’informations, consultez la section Utilisation de l’annulation de [utilisation du modèle asynchrone basé sur des tâches](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md).

## <a name="see-also"></a>Voir aussi
 [Modèle asynchrone basé sur les tâches (TAP, Task-based Asynchronous Pattern)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)  
 [Utilisation du modèle asynchrone basé sur les tâches](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)  
 [Interopérabilité avec d’autres types et modèles asynchrones](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)  
