---
title: "IInstallReferenceItem::GetReference, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IInstallReferenceItem.GetReference
api_location: fusion.dll
api_type: COM
f1_keywords: IInstallReferenceItem::GetReference
helpviewer_keywords:
- IInstallReferenceItem::GetReference method [.NET Framework fusion]
- GetReference method [.NET Framework fusion]
ms.assetid: 8960332f-c98a-405a-ba92-7003de0c1187
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8686e27e63d7363e61bf4c8f1898b71d21fda52b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="iinstallreferenceitemgetreference-method"></a>IInstallReferenceItem::GetReference, méthode
Obtient un pointeur vers le [FUSION_INSTALL_REFERENCE](../../../../docs/framework/unmanaged-api/fusion/fusion-install-reference-structure.md) structure représentée par ce [IInstallReferenceItem](../../../../docs/framework/unmanaged-api/fusion/iinstallreferenceitem-interface.md) objet.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT GetReference (  
    [out] LPFUSION_INSTALL_REFERENCE *ppRefData,  
    [in]  DWORD dwFlags,  
    [in]  LPVOID pvReserved  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `ppRefData`  
 [out] Retourné `FUSION_INSTALL_REFERENCE` pointeur.  
  
 `dwFlags`  
 [in] Réservé pour une future extensibilité. `dwFlags`doit être 0 (zéro).  
  
 `pvReserved`  
 [in] Réservé pour une future extensibilité. `pvReserved`doit être une référence null.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** Fusion.h  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [IInstallReferenceItem (Interface)](../../../../docs/framework/unmanaged-api/fusion/iinstallreferenceitem-interface.md)  
 [FUSION_INSTALL_REFERENCE (Structure)](../../../../docs/framework/unmanaged-api/fusion/fusion-install-reference-structure.md)
