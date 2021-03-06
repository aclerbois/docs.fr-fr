---
title: "Exportation et importation de métadonnées"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: metadata [WCF], exporting and importing
ms.assetid: 614a75bb-e0b0-4c95-b6d8-02cb5e5ddb38
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 91b03e29c2841434d4222f59ae62028bf2431a84
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="exporting-and-importing-metadata"></a>Exportation et importation de métadonnées
Dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], le processus d'exportation de métadonnées consiste à décrire des points de terminaison de service et à les projeter dans une représentation parallèle standardisée qui permet aux clients de comprendre comment utiliser le service. L'importation des métadonnées du service est le processus de génération d'instances <xref:System.ServiceModel.Description.ServiceEndpoint> ou de parties de métadonnées de service.  
  
## <a name="exporting-metadata"></a>Exportation de métadonnées  
 Pour exporter des métadonnées à partir des instances <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>, utilisez une implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataExporter>. Le type <xref:System.ServiceModel.Description.WsdlExporter> est l'implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataExporter> fournie avec [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Le type <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> génère les métadonnées WSDL (Web Services Description Language) avec les expressions de stratégie attachées encapsulées dans une instance <xref:System.ServiceModel.Description.MetadataSet>. Vous pouvez utiliser une instance <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> pour exporter de manière itérative les métadonnées pour les objets <xref:System.ServiceModel.Description.ContractDescription> et les objets <xref:System.ServiceModel.Description.ServiceEndpoint>. Vous pouvez également exporter une collection d'objets <xref:System.ServiceModel.Description.ServiceEndpoint> et les associer avec un nom de service spécifique.  
  
> [!NOTE]
>  `WsdlExporter` permet uniquement d'exporter des métadonnées à partir d'instances `ContractDescription` qui contiennent des informations de type CLR (Common Language Runtime), telles qu'une instance `ContractDescription` créée à l'aide de la méthode `ContractDescription.GetContract` ou créée en tant que partie de la `ServiceDescription` d'une instance `ServiceHost`. Vous ne pouvez pas utiliser `WsdlExporter` pour exporter des métadonnées à partir d'instances `ContractDescription` importées depuis les métadonnées du service ou construites sans information de type.  
  
## <a name="importing-metadata"></a>Exportation de métadonnées  
  
### <a name="importing-wsdl-documents"></a>Importation de documents WSDL  
 Pour importer des métadonnées de service dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], utilisez une implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataImporter>. Le type <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> est l'implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataImporter> fournie avec [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Le type <xref:System.ServiceModel.Description.WsdlImporter> importe des métadonnées WSDL avec les stratégies attachées fournies dans un objet <xref:System.ServiceModel.Description.MetadataSet>.  
  
 Le type <xref:System.ServiceModel.Description.WsdlImporter> vous permet de contrôler comment importer les métadonnées. Vous pouvez importer tous les points de terminaison, toutes les liaisons ou tous les contrats. Vous pouvez importer tous les points de terminaison associés à un service WSDL spécifique, une liaison ou un type de port. Vous pouvez également importer le point de terminaison d'un port WSDL spécifique, la liaison d'une liaison WSDL spécifique ou le contrat d'un type de port WSDL spécifique.  
  
 <xref:System.ServiceModel.Description.WsdlImporter> expose également une propriété <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A> qui vous permet de spécifier un jeu de contrats ne devant pas être importés. <xref:System.ServiceModel.Description.WsdlImporter> utilise les contrats dans la propriété <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A> au lieu d'importer un contrat avec le même nom qualifié à partir des métadonnées.  
  
### <a name="importing-policies"></a>Importation de stratégies  
 Le type <xref:System.ServiceModel.Description.WsdlImporter> recueille les expressions de stratégie jointes aux sujets du message, de l'opération et de la stratégie de point de terminaison, puis utilise les implémentations <xref:System.ServiceModel.Description.IPolicyImportExtension> dans la collection <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> pour importer les expressions de stratégie.  
  
 La logique d'importation de la stratégie gère automatiquement les références aux expressions de stratégie dans le même document WSDL et est identifiée avec un attribut `wsu:Id` ou `xml:id`. La logique d'importation de la stratégie protège les applications contre les références de stratégie circulaires en limitant la taille d'une expression de stratégie à 4096 nœuds, où un nœud est l'un des éléments suivants : `wsp:Policy`, `wsp:All`, `wsp:ExactlyOne`, `wsp:policyReference`.  
  
 La logique d'importation de stratégie normalise également automatiquement des expressions de stratégie. Les expressions de stratégie imbriquées et l'attribut `wsp:Optional` ne sont pas normalisés. Le traitement de normalisation effectué est limitée à 4096 étapes, où chaque étape cède une assertion de stratégie ou un élément enfant d'un élément `wsp:ExactlyOne`.  
  
 Le type <xref:System.ServiceModel.Description.WsdlImporter> essaye jusqu'à 32 combinaisons d'alternatives de stratégie jointes aux différents sujets de stratégie WSDL. Si aucune combinaison n'est correctement importée, la première combinaison est utilisée pour construire une liaison personnalisée partielle.  
  
## <a name="error-handling"></a>Gestion des erreurs  
 Les types <xref:System.ServiceModel.Description.MetadataExporter> et <xref:System.ServiceModel.Description.MetadataImporter> exposent une propriété `Errors` qui peut contenir une collection de messages d'erreur et d'avertissement rencontrés pendant les processus d'exportation et d'importation, respectivement ; ces derniers peuvent être utilisés lors de l'implémentation d'outils.  
  
 Le type <xref:System.ServiceModel.Description.WsdlImporter> lève généralement une exception pour une exception détectée pendant l'importation et ajoute une erreur correspondante à sa propriété `Errors`. Les méthodes <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A>et <xref:System.ServiceModel.Description.WsdlImporter.ImportEndpoints%2A>, toutefois, ne lèvent pas ces exceptions, vous devez donc vérifier la propriété `Errors` pour déterminer si un problème s'est produit lors de l'appel de ces méthodes.  
  
 Le type <xref:System.ServiceModel.Description.WsdlExporter> lève à nouveau toutes les exceptions détectées pendant le processus d'exportation. Ces exceptions ne sont pas capturées en tant qu'erreurs dans la propriété `Errors`. Une fois que <xref:System.ServiceModel.Description.WsdlExporter> lève une exception, celle-ci se trouve dans un état de faute et ne peut pas être réutilisée. <xref:System.ServiceModel.Description.WsdlExporter> ajoute des avertissements à sa propriété `Errors` lorsqu'une opération ne peut pas être exportée parce qu'elle utilise des actions génériques et lorsque des noms de liaison dupliqués sont rencontrés.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Comment : importer des métadonnées dans les points de terminaison de Service](../../../../docs/framework/wcf/feature-details/how-to-import-metadata-into-service-endpoints.md)  
 Décrit comment importer les métadonnées téléchargées dans des objets description.  
  
 [Comment : exporter les métadonnées à partir de points de terminaison de Service](../../../../docs/framework/wcf/feature-details/how-to-export-metadata-from-service-endpoints.md)  
 Décrit comment exporter des objets description dans des métadonnées.  
  
 [ServiceDescription et WSDL référence](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)  
 Décrit le mappage entre les objets description et WSDL.  
  
 [Comment : utiliser Svcutil.exe pour exporter les métadonnées à partir de Code de Service compilé](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)  
 Décrit l'utilisation de Svcutil.exe pour exporter les métadonnées pour les services, les contrats et les types de données dans les assemblys compilés.  
  
 [Référence de schéma de contrat de données](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)  
 Décrit le sous-ensemble du schéma XML (XSD) utilisé par <xref:System.Runtime.Serialization.DataContractSerializer> pour décrire les types CLR (Common Language Run-time) pour la sérialisation XML.  
  
## <a name="reference"></a>Référence  
 <xref:System.ServiceModel.Description.WsdlExporter>  
  
 <xref:System.ServiceModel.Description.WsdlImporter>  
  
## <a name="see-also"></a>Voir aussi  
 [Exportation de métadonnées personnalisées pour une Extension WCF](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md)  
 [Importation de métadonnées personnalisées pour une Extension WCF](../../../../docs/framework/wcf/extending/importing-custom-metadata-for-a-wcf-extension.md)
