---
title: "ICorDebugStepper::SetInterceptMask, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugStepper.SetInterceptMask
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugStepper::SetInterceptMask
helpviewer_keywords:
- SetInterceptMask method [.NET Framework debugging]
- ICorDebugStepper::SetInterceptMask method [.NET Framework debugging]
ms.assetid: 6245e2ae-5cc2-43ff-8cc1-71953d12113a
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 2a99b504c0ce58ca6b89153667598cd4c2c682d9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugsteppersetinterceptmask-method"></a><span data-ttu-id="d95e1-102">ICorDebugStepper::SetInterceptMask, méthode</span><span class="sxs-lookup"><span data-stu-id="d95e1-102">ICorDebugStepper::SetInterceptMask Method</span></span>
<span data-ttu-id="d95e1-103">Définit une valeur qui spécifie les types de code qui sont en retrait dans.</span><span class="sxs-lookup"><span data-stu-id="d95e1-103">Sets a value that specifies the types of code that are stepped into.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d95e1-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d95e1-104">Syntax</span></span>  
  
```  
HRESULT SetInterceptMask (  
    [in] CorDebugIntercept    mask  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="d95e1-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d95e1-105">Parameters</span></span>  
 `mask`  
 <span data-ttu-id="d95e1-106">[in] Une combinaison de valeurs de l’énumération CorDebugIntercept qui spécifie les types de code.</span><span class="sxs-lookup"><span data-stu-id="d95e1-106">[in] A combination of values of the CorDebugIntercept enumeration that specifies the types of code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d95e1-107">Remarques</span><span class="sxs-lookup"><span data-stu-id="d95e1-107">Remarks</span></span>  
 <span data-ttu-id="d95e1-108">Si le bit pour un intercepteur est défini, l’exécution pas à pas se termine lorsque le type donné de code d’interception est rencontré.</span><span class="sxs-lookup"><span data-stu-id="d95e1-108">If the bit for an interceptor is set, the stepper will complete when the given type of intercepting code is encountered.</span></span> <span data-ttu-id="d95e1-109">Si le bit est désactivé, le code d’interception sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="d95e1-109">If the bit is cleared, the intercepting code will be skipped.</span></span>  
  
 <span data-ttu-id="d95e1-110">Le `SetInterceptMask` méthode peut avoir des interactions imprévues avec [ICorDebugStepper::SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) (à partir de point de vue de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="d95e1-110">The `SetInterceptMask` method may have unforeseen interactions with [ICorDebugStepper::SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) (from the user's point of view).</span></span> <span data-ttu-id="d95e1-111">Par exemple, si visible uniquement (autrement dit, non interne) partie du code d’initialisation de classe ne possède pas les informations de mappage et que STOP_NO_MAPPING_INFO n’est pas défini (consultez la [ICorDebugStepper::SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) (méthode) et le CorDebugUnmappedStop (énumération)), l’ignorera l’initialisation de classe.</span><span class="sxs-lookup"><span data-stu-id="d95e1-111">For example, if the only visible (that is, non-internal) portion of class initialization code lacks mapping information and STOP_NO_MAPPING_INFO isn't set (see the [ICorDebugStepper::SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) method and the CorDebugUnmappedStop enumeration), the stepper will step over the class initialization.</span></span> <span data-ttu-id="d95e1-112">Par défaut, seule la valeur INTERCEPT_NONE de le `CorDebugIntercept` énumération sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="d95e1-112">By default, only the INTERCEPT_NONE value of the `CorDebugIntercept` enumeration will be used.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d95e1-113">Spécifications</span><span class="sxs-lookup"><span data-stu-id="d95e1-113">Requirements</span></span>  
 <span data-ttu-id="d95e1-114">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d95e1-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d95e1-115">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d95e1-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d95e1-116">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d95e1-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d95e1-117">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d95e1-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>