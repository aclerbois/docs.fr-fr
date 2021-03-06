---
title: moduloObjectHashcode (MDA)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- managed debugging assistants (MDAs), hashcode modulus
- Modulo object hash code
- moduloObjectHashcode MDA
- hashcode modulus
- MDAs (managed debugging assistants), hashcode modulus
- GetHashCode method
- modulus of hashcodes
ms.assetid: b45366ff-2a7a-4b8e-ab01-537b72e9de68
caps.latest.revision: "10"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 1a3062365f41247c579f5420497946128b183a88
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="moduloobjecthashcode-mda"></a>moduloObjectHashcode (MDA)
L’Assistant Débogage managé `moduloObjectHashcode` modifie le comportement de la classe <xref:System.Object> pour effectuer une opération modulo sur le code de hachage retourné par la méthode <xref:System.Object.GetHashCode%2A>. Le modulo par défaut pour cet Assistant Débogage managé est 1, ce qui fait que <xref:System.Object.GetHashCode%2A> retourne 0 pour tous les objets.  
  
## <a name="symptoms"></a>Symptômes  
 Après le passage à une nouvelle version du common language runtime, un programme ne s’exécute plus correctement :  
  
-   Le programme reçoit un objet incorrect d’un <xref:System.Collections.Hashtable>.  
  
-   L’ordre d’énumération d’un <xref:System.Collections.Hashtable> a changé et le programme ne fonctionne plus correctement.  
  
-   Deux objets qui étaient habituellement égaux ne le sont plus.  
  
-   Deux objets qui étaient habituellement inégaux sont maintenant égaux.  
  
## <a name="cause"></a>Cause  
 Votre programme reçoit peut-être un objet incorrect d’un <xref:System.Collections.Hashtable> en raison du fait que l’implémentation de la méthode <xref:System.Object.Equals%2A> sur la classe pour la clé dans le <xref:System.Collections.Hashtable> teste l’égalité des objets en comparant les résultats de l’appel à la méthode <xref:System.Object.GetHashCode%2A>. Les codes de hachage ne doivent pas être utilisés pour tester l’égalité entre des objets, car deux objets peuvent avoir le même code de hachage même si leurs champs respectifs ont des valeurs différentes. Ces collisions de codes de hachage, bien que rares dans la pratique, se produisent. L’effet de ceci sur une recherche dans <xref:System.Collections.Hashtable> est que deux clés qui ne sont pas égales apparaissent comme étant égales et que l’objet incorrect est retourné depuis le <xref:System.Collections.Hashtable>. Pour des raisons de performances, l’implémentation de <xref:System.Object.GetHashCode%2A> peut changer entre les versions du runtime : ainsi, des collisions qui ne se produisent pas sur une version peuvent se produire sur les versions ultérieures. Activez cet Assistant Débogage managé pour tester si votre code comporte des bogues en cas de collision de codes de hachage. Quand il est activé, cet Assistant Débogage managé fait que la méthode <xref:System.Object.GetHashCode%2A> retourne 0, ce qui entraîne une collision de tous les codes de hachage. Le seul effet que l’activation de cet Assistant Débogage managé doit avoir sur votre programme est que celui-ci s’exécute plus lentement.  
  
 L’ordre d’énumération d’un <xref:System.Collections.Hashtable> peut changer d’une version du runtime à l’autre si l’algorithme utilisé pour calculer les codes de hachage de la clé change. Pour tester si votre programme est dépendant de l’ordre d’énumération des clés ou des valeurs provenant d’une table de hachage, vous pouvez activer cet Assistant Débogage managé.  
  
## <a name="resolution"></a>Résolution  
 N’utilisez jamais de codes de hachage en remplacement de l’identité d’un objet. Implémentez le remplacement de la méthode <xref:System.Object.Equals%2A?displayProperty=nameWithType> de façon à ne pas comparer les codes de hachage.  
  
 Ne créez pas de dépendances par rapport à l’ordre des énumérations de clés ou de valeurs dans des tables de hachage.  
  
## <a name="effect-on-the-runtime"></a>Effet sur le runtime  
 Les applications s’exécutent plus lentement quand cet Assistant Débogage managé est activé. Cet Assistant Débogage managé prend le code de hachage qui aurait été retourné et retourne à la place le reste de la division par un modulo.  
  
## <a name="output"></a>Sortie  
 Cet Assistant Débogage managé n’a pas de sortie.  
  
## <a name="configuration"></a>Configuration  
 L’attribut `modulus` spécifie le modulo utilisé sur le code de hachage. La valeur par défaut est 1.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <moduloObjectHashcode modulus="1" />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType>  
 <xref:System.Object.Equals%2A?displayProperty=nameWithType>  
 [Diagnostic d’erreurs avec les Assistants Débogage managé](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
