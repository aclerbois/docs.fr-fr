---
title: Binding2
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: b9e44d161e1229db9145f4ed7e337396bbd98c68
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="binding"></a>Liaison
WMI Binding  
  
## <a name="syntax"></a>Syntaxe  
  
```  
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>Méthodes  
 La classe Binding ne définit pas de méthodes.  
  
## <a name="properties"></a>Propriétés  
 La classe Binding a les propriétés suivantes :  
  
### <a name="bindingelements"></a>BindingElement  
 Type de données : tableau BindingElement  
  
 Type d'accès : lecture seule  
  
 Collection d'éléments de liaison implémentés par la liaison.  
  
### <a name="closetimeout"></a>CloseTimeout  
 Type de données : datetime  
  
 Type d'accès : lecture seule  
  
 Intervalle de temps spécifié pour l'exécution d'une opération de fermeture.  
  
### <a name="name"></a>Nom  
 Type de données : chaîne  
  
 Type d'accès : lecture seule  
  
 Le nom de la liaison.  
  
### <a name="namespace"></a>Espace de noms  
 Type de données : chaîne  
  
 Type d'accès : lecture seule  
  
 Espace de noms XML de la liaison.  
  
### <a name="opentimeout"></a>OpenTimeout  
 Type de données : datetime  
  
 Type d'accès : lecture seule  
  
 Intervalle de temps spécifié pour l'exécution d'une opération d'ouverture.  
  
### <a name="receivetimeout"></a>ReceiveTimeout  
 Type de données : datetime  
  
 Type d'accès : lecture seule  
  
 Intervalle de temps spécifié pour l'exécution d'une opération de réception.  
  
### <a name="scheme"></a>Scheme  
 Type de données : chaîne  
  
 Type d'accès : lecture seule  
  
 Modèle de transport URI utilisé par les fabrications et écouteurs de canal construits par la liaison.  
  
### <a name="sendtimeout"></a>SendTimeout  
 Type de données : datetime  
  
 Type d'accès : lecture seule  
  
 Intervalle de temps spécifié pour l'exécution d'une opération d'envoi.  
  
## <a name="requirements"></a>Spécifications  
  
|MOF|Déclaré dans Servicemodel.mof.|  
|---------|-----------------------------------|  
|Espace de noms|Défini dans root\ServiceModel|  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.Channels.Binding>
