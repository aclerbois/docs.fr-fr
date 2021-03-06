---
title: "ICorDebugHeapValue::IsValid, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugHeapValue.IsValid
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugHeapValue::IsValid
helpviewer_keywords:
- IsValid method [.NET Framework debugging]
- ICorDebugHeapValue::IsValid method [.NET Framework debugging]
ms.assetid: 68e20e62-203d-46d8-bb91-8d3c61cfacc3
topic_type: apiref
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: df7105c94a6f88c9c196f1d9d6be6f4a62f7c258
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugheapvalueisvalid-method"></a>ICorDebugHeapValue::IsValid, méthode
Obtient une valeur qui indique si l’objet représenté par ICorDebugHeapValue est valide.  
  
 Cette méthode a été déconseillée dans le .NET Framework version 2.0.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT IsValid (  
    [out] BOOL    *pbValid  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `pbValid`  
 [out] Pointeur vers une valeur booléenne qui indique si cette valeur sur le tas est valide.  
  
## <a name="remarks"></a>Remarques  
 La valeur n’est pas valide si elle a été récupéré par le garbage collector.  
  
 Cette méthode est dépréciée. Dans le .NET Framework 2.0, toutes les valeurs sont valides jusqu'à ce que [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) est appelée, à laquelle les valeurs sont invalidés.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
