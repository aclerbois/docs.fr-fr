---
title: "ICorDebugType::GetType, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugType.GetType
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugType::GetType
helpviewer_keywords:
- ICorDebugType::GetType method [.NET Framework debugging]
- GetType method, ICorDebugType interface [.NET Framework debugging]
ms.assetid: d6e64534-4d47-4ad0-a340-7590e07e2b4a
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 20e2a1415d5dda9c4097d984af46942ebcf2365a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugtypegettype-method"></a><span data-ttu-id="97206-102">ICorDebugType::GetType, méthode</span><span class="sxs-lookup"><span data-stu-id="97206-102">ICorDebugType::GetType Method</span></span>
<span data-ttu-id="97206-103">Obtient une valeur CorElementType qui décrit le type natif du common language runtime (CLR) <xref:System.Type> représenté par cet ICorDebugType.</span><span class="sxs-lookup"><span data-stu-id="97206-103">Gets a CorElementType value that describes the native type of the common language runtime (CLR) <xref:System.Type> represented by this ICorDebugType.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="97206-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="97206-104">Syntax</span></span>  
  
```  
HRESULT GetType (  
    [out] CorElementType   *ty  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="97206-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="97206-105">Parameters</span></span>  
 `ty`  
 <span data-ttu-id="97206-106">[out] Un pointeur vers une valeur de la `CorElementType` énumération qui indique le CLR <xref:System.Type> par ce `ICorDebugType` représente.</span><span class="sxs-lookup"><span data-stu-id="97206-106">[out] A pointer to a value of the `CorElementType` enumeration that indicates the CLR <xref:System.Type> that this `ICorDebugType` represents.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="97206-107">Remarques</span><span class="sxs-lookup"><span data-stu-id="97206-107">Remarks</span></span>  
 <span data-ttu-id="97206-108">Si la valeur de `ty` est ELEMENT_TYPE_CLASS ou ELEMENT_TYPE_VALUETYPE, la [ICorDebugType::GetClass](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md) méthode peut être appelée pour obtenir le type non instancié pour un type générique ; sinon, n’appelez pas `ICorDebugType::GetClass`.</span><span class="sxs-lookup"><span data-stu-id="97206-108">If the value of `ty` is either ELEMENT_TYPE_CLASS or ELEMENT_TYPE_VALUETYPE, the [ICorDebugType::GetClass](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md) method may be called to get the uninstantiated type for a generic type; otherwise, do not call `ICorDebugType::GetClass`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="97206-109">Spécifications</span><span class="sxs-lookup"><span data-stu-id="97206-109">Requirements</span></span>  
 <span data-ttu-id="97206-110">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="97206-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="97206-111">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="97206-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="97206-112">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="97206-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="97206-113">**Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="97206-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>