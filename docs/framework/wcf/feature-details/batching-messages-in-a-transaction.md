---
title: Traitement par lots des messages dans une transaction
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: batching messages [WCF]
ms.assetid: 53305392-e82e-4e89-aedc-3efb6ebcd28c
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: d9effe9b44a8e6f786103162930852de80ab4f8d
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="batching-messages-in-a-transaction"></a>Traitement par lots des messages dans une transaction
Les applications en file d’attente utilisent des transactions pour garantir l’exactitude et la remise fiable des messages. Toutefois, les transactions sont des opérations coûteuses et peuvent réduire considérablement le débit de message. L'une des méthodes utilisées pour améliorer le débit de message est de disposer d'une application capable de lire et de traiter plusieurs messages dans une transaction unique. Le compromis réside entre la performance et la récupération : à mesure que le nombre de messages dans un lot augmente, la quantité de travail de récupération nécessaire en cas de restauration des transactions augmente également. Il est important de noter la différence entre le traitement par lot des messages dans une transaction et dans des sessions. A *session* est un regroupement de messages traités par une application unique et validés en tant qu’unité unique. Les sessions sont en général utilisées lorsqu'un groupe de messages du même type doivent être traités ensemble. Un site web d’achat en ligne en est un exemple. *Lots* utilisés pour traiter plusieurs, indépendants des messages de façon qu’augmente le débit des messages. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]sessions, consultez [regrouper en file d’attente des Messages dans une Session](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md). Les messages d’un lot sont également traités par une application unique et sont validés en tant qu’unité unique, mais il peut n’y avoir aucune relation entre eux. Le traitement par lot des messages dans une transaction est une optimisation qui ne modifie pas la manière dont l'application s'exécute.  
  
## <a name="entering-batching-mode"></a>Passage en mode de traitement par lot  
 Le comportement de point de terminaison <xref:System.ServiceModel.Description.TransactedBatchingBehavior> contrôle le traitement par lot. L'ajout de ce comportement de point de terminaison à un point de terminaison de service indique à [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] de traiter par lot les messages dans une transaction. Pas tous les messages d’une transaction, seuls les messages qui requièrent une transaction sont placés dans un lot, et seuls les messages envoyés à partir d’opérations marquées avec `TransactionScopeRequired`  =  `true` et `TransactionAutoComplete`  =  `true` sont pris en compte pour un lot. Si toutes les opérations sur le contrat de service sont marquées avec `TransactionScopeRequired`  =  `false` et `TransactionAutoComplete`  =  `false`, le mode de traitement par lot n’est jamais entré.  
  
## <a name="committing-a-transaction"></a>Validation d’une transaction  
 Une transaction par lot est validée selon les éléments suivants :  
  
-   `MaxBatchSize`. Propriété du comportement <xref:System.ServiceModel.Description.TransactedBatchingBehavior>. Cette propriété détermine le nombre maximal de messages placés dans un lot. Lorsque ce nombre est atteint, le lot est validé. Cette valeur n'est pas une limite stricte et il est possible de valider un lot avant d'avoir reçu ce nombre de messages.  
  
-   `Transaction Timeout`. Lorsque 80 pourcent du délai d'expiration de la transaction est écoulé, le lot est validé et un nouveau lot est créé. Cela signifie que s'il reste 20 pourcent ou moins du temps accordé à une transaction pour se terminer, le lot est validé.  
  
-   `TransactionScopeRequired`. Lors du traitement d’un lot de messages, si [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trouve un qui a `TransactionScopeRequired`  =  `false`, il valide le lot et en rouvre un nouveau lot sur la réception du premier message avec `TransactionScopeRequired`  =  `true` et `TransactionAutoComplete` = `true`.  
  
-   S'il n'y a plus de message dans la file d'attente, le lot actuel est validé, même si `MaxBatchSize` n'a pas été atteint ou que 80 pourcent du délai d'expiration de la transaction ne se sont pas écoulés.  
  
## <a name="leaving-batching-mode"></a>Conservation du mode de traitement par lot  
 Si un message dans un lot provoque l'abandon de la transaction, les étapes suivantes se produisent :  
  
1.  L'ensemble du lot de messages est restauré.  
  
2.  Les messages sont lus un par un jusqu'à ce que le nombre de messages lus dépasse le double de la taille de lot maximale.  
  
3.  Le mode de traitement par lot est réactivé.  
  
## <a name="choosing-the-batch-size"></a>Sélection de la taille de lot  
 La taille d'un lot varie en fonction de l'application. La méthode empirique s'avère être la meilleure pour arriver à une taille de lot optimale pour l'application. Sélectionnez la taille de lot en fonction du modèle de déploiement réel de votre application. Par exemple, lors du déploiement de l'application, si un serveur SQL doit être installé sur un ordinateur distant et qu'une transaction doit couvrir la file d'attente et le serveur SQL, la taille de lot sera déterminée de manière optimale en exécutant cette configuration exacte.  
  
## <a name="concurrency-and-batching"></a>Traitement par lot simultané  
 Pour augmenter le débit, vous pouvez également exécuter un grand nombre de lots simultanément. Pour activer le traitement par lot simultané, définissez `ConcurrencyMode.Multiple` dans `ServiceBehaviorAttribute`.  
  
 *Limitation de service* est un comportement de service qui est utilisé pour indiquer le nombre maximal d’appels simultanés permettre être effectué sur le service. Lorsqu'il est utilisé en combinaison avec le traitement par lot, il permet d'indiquer le nombre de lots simultanés qui peuvent être exécutés. Si la limitation de service n'est pas définie, le nombre maximal d'appels simultanés par défaut de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] est de 16. Par conséquent, si le comportement de traitement par lot a été ajouté par défaut, 16 lots au maximum peuvent être simultanément actifs. Il est préférable d'ajuster la limitation de service et le traitement par lot en fonction de votre capacité. Par exemple, si la file d'attente contient 100 messages et qu'un lot de 20 est souhaité, un nombre maximal d'appels simultanés à 16 n'est pas utile car, selon débit, 16 transactions pourraient être actives, ce qui revient au même que de ne pas avoir de traitement par lot activé. Par conséquent, lors de l'optimisation des performances, n'activez pas le traitement par lot simultané ou définissez également une taille de limitation de service correcte.  
  
## <a name="batching-and-multiple-endpoints"></a>Traitement par lot et points de terminaison multiples  
 Un point de terminaison est composé d'une adresse et d'un contrat. Plusieurs points de terminaison peuvent partager la même liaison. Deux points de terminaison peuvent partager la même liaison et écouter un URI (Uniform Resource Identifier) ou une adresse de file d'attente. Si deux points de terminaison lisent à partir de la même file d'attente, et que le comportement de traitement par lot avec transaction est ajouté à ces deux points de terminaison, un conflit dans les tailles de lot spécifiées peut se produire. Il est résolu en implémentant le traitement par lot à l'aide de la taille de lot minimale spécifiée entre les deux comportements de traitement par lot avec transaction. Dans ce scénario, si l'un des points de terminaison ne spécifie pas de traitement par lot avec transaction, les deux points de terminaison ne l'utiliseront pas.  
  
## <a name="example"></a>Exemple  
 L'exemple suivant indique comment spécifier `TransactedBatchingBehavior` dans un fichier de configuration.  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="TransactedBatchingBehavior"
              maxBatchSize="100" />
  </endpointBehaviors>
</behaviors>
```  
  
 L'exemple suivant indique comment spécifier <xref:System.ServiceModel.Description.TransactedBatchingBehavior> dans le code.  
  
```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
     ServiceEndpoint sep = ServiceHost.AddServiceEndpoint(typeof(IOrderProcessor), new NetMsmqBinding(), "net.msmq://localhost/private/ServiceModelSamplesTransacted");
     sep.Behaviors.Add(new TransactedBatchingBehavior(100));
     
     // Open the ServiceHost to create listeners and start listening for messages.
    serviceHost.Open();
  
    // The service can now be accessed.
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.WriteLine();
    Console.ReadLine();
  
    // Close the ServiceHostB to shut down the service.
    serviceHost.Close();
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble des files d’attente](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
 [Queuing dans WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
