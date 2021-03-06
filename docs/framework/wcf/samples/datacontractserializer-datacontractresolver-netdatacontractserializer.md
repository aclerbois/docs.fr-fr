---
title: "Utilisation de DataContractSerializer et DataContractResolver pour fournir les fonctionnalités de NetDataContractSerializer"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1376658f-f695-45f7-a7e0-94664e9619ff
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 91d3293b1229434462dd0f6b31bc1de2df925a40
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="using-datacontractserializer-and-datacontractresolver-to-provide-the-functionality-of-netdatacontractserializer"></a>Utilisation de DataContractSerializer et DataContractResolver pour fournir les fonctionnalités de NetDataContractSerializer
Cet exemple montre comment l'utilisation de <xref:System.Runtime.Serialization.DataContractSerializer> avec un <xref:System.Runtime.Serialization.DataContractResolver> approprié fournit les mêmes fonctionnalités que <xref:System.Runtime.Serialization.NetDataContractSerializer>. Cet exemple montre comment créer le <xref:System.Runtime.Serialization.DataContractResolver> approprié et comment l'ajouter au <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
## <a name="sample-details"></a>Détails de l'exemple  
 <xref:System.Runtime.Serialization.NetDataContractSerializer> diffère de <xref:System.Runtime.Serialization.DataContractSerializer> sur un point important : <xref:System.Runtime.Serialization.NetDataContractSerializer> inclut des informations de type CLR dans le XML sérialisé ; <xref:System.Runtime.Serialization.DataContractSerializer> ne le fait pas. Par conséquent, <xref:System.Runtime.Serialization.NetDataContractSerializer> peut être utilisé uniquement si les extrémités de sérialisation et de désérialisation partagent toutes deux les mêmes types CLR. Toutefois, il est recommandé d'utiliser <xref:System.Runtime.Serialization.DataContractSerializer>, car il offre de meilleures performances que <xref:System.Runtime.Serialization.NetDataContractSerializer>. Vous pouvez modifier les informations sérialisées dans <xref:System.Runtime.Serialization.DataContractSerializer> en lui ajoutant un <xref:System.Runtime.Serialization.DataContractResolver>.  
  
 Cet exemple est composé de deux projets. Le premier projet utilise <xref:System.Runtime.Serialization.NetDataContractSerializer> pour sérialiser un objet. Le second projet utilise <xref:System.Runtime.Serialization.DataContractSerializer> avec un <xref:System.Runtime.Serialization.DataContractResolver> pour fournir les mêmes fonctionnalités que le premier projet.  
  
 L'exemple de code suivant illustre l'implémentation d'un <xref:System.Runtime.Serialization.DataContractResolver> personnalisé, nommé `MyDataContractResolver`, qui est ajouté au <xref:System.Runtime.Serialization.DataContractSerializer> du projet DCSwithDCR.  
  
```  
class MyDataContractResolver : DataContractResolver  
{  
    private XmlDictionary dictionary = new XmlDictionary();  
  
    public MyDataContractResolver()  
    {  
    }  
  
    // Used at deserialization  
    // Allows users to map xsi:type name to any Type   
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        Type type = knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        if (type == null)  
        {  
            type = Type.GetType(typeName + ", " + typeNamespace);  
        }  
        return type;  
    }  
  
    // Used at serialization  
    // Maps any Type to a new xsi:type representation  
    public override void ResolveType(Type dataContractType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        knownTypeResolver.ResolveType(dataContractType, null, out typeName, out typeNamespace);  
        if (typeName == null || typeNamespace == null)  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add(dataContractType.FullName);  
            typeNamespace = dictionary.Add(dataContractType.Assembly.FullName);  
        }  
    }  
}  
```  
  
#### <a name="to-use-this-sample"></a>Pour utiliser cet exemple  
  
1.  À l'aide de [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], ouvrez le fichier solution DCRSample.sln.  
  
2.  Cliquez sur le fichier solution et choisissez **propriétés**.  
  
3.  Dans le **les Pages de propriétés de Solution** boîte de dialogue, sous **propriétés communes**, **projet de démarrage**, sélectionnez **plusieurs projets de démarrage :**.  
  
4.  À côté du **DCSwithDCR** projet, sélectionnez **Démarrer** à partir de la **Action** liste déroulante.  
  
5.  À côté du **NetDCS** projet, sélectionnez **Démarrer** à partir de la **Action** liste déroulante.  
  
6.  Cliquez sur **OK** pour fermer la boîte de dialogue.  
  
7.  Pour générer la solution, appuyez sur Ctrl+Maj+B.  
  
8.  Pour exécuter la solution, appuyez sur Ctrl+F5.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Data\NetDcSasDcSwithDCR`  
  
## <a name="see-also"></a>Voir aussi
