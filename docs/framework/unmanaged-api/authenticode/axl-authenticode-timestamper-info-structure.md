---
title: AXL_AUTHENTICODE_TIMESTAMPER_INFO, structure
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 89e41a81-0f41-45ad-8f20-a120e4ff24fb
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0ada8f5b21328d008ad34f4ac96cbf24e881a93b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="axlauthenticodetimestamperinfo-structure"></a>AXL_AUTHENTICODE_TIMESTAMPER_INFO, structure
Définit les informations de l'horodateur Authenticode.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
typedef struct _AXL_AUTHENTICODE_SIGNER_INFO {  
    DWORD cbSize;  
    HRESULT dwError;  
    ALG_ID algHash;  
    FILETIME ftTimestamp  
    PCCERT_CHAIN_CONTEXT pChainContext;  
} AXL_AUTHENTICODE_TIMESTAMPER_INFO, * PAXL_AUTHENTICODE_TIMESTAMPER_INFO;  
```  
  
## <a name="members"></a>Membres  
  
|Membre|Description|  
|------------|-----------------|  
|`cbSize`|La taille de cette structure.|  
|`dwError`|Le code d'erreur.|  
|`algHash`|L'algorithme de hachage.|  
|`ftTimestamp`|La date/heure de l'horodatage.|  
|`pChainContext`|La chaîne de contexte de l'horodateur.  Consultez le [CERT_CONTEXT](http://msdn.microsoft.com/library/windows/desktop/aa377189.aspx) structure.|  
  
## <a name="see-also"></a>Voir aussi  
 [Authenticode](../../../../docs/framework/unmanaged-api/authenticode/index.md)
