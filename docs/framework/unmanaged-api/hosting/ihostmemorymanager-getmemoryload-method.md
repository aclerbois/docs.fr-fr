---
title: "IHostMemoryManager::GetMemoryLoad, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostMemoryManager.GetMemoryLoad
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostMemoryManager::GetMemoryLoad
helpviewer_keywords:
- IHostMemoryManager::GetMemoryLoad method [.NET Framework hosting]
- GetMemoryLoad method [.NET Framework hosting]
ms.assetid: e8138f6e-a0a4-48d4-8dae-9466b4dc6180
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7296790eb80fe90cd115150749e533ce1800834b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="ihostmemorymanagergetmemoryload-method"></a><span data-ttu-id="44ef5-102">IHostMemoryManager::GetMemoryLoad, méthode</span><span class="sxs-lookup"><span data-stu-id="44ef5-102">IHostMemoryManager::GetMemoryLoad Method</span></span>
<span data-ttu-id="44ef5-103">Obtient la quantité de mémoire physique qui est actuellement en cours d’utilisation et par conséquent pas disponible, comme indiqué par l’hôte.</span><span class="sxs-lookup"><span data-stu-id="44ef5-103">Gets the amount of physical memory that is currently in use, and therefore unavailable, as reported by the host.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="44ef5-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="44ef5-104">Syntax</span></span>  
  
```  
HRESULT GetMemoryLoad (  
    [out] DWORD*  pMemoryLoad,   
    [out] SIZE_T  *pAvailableBytes  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="44ef5-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="44ef5-105">Parameters</span></span>  
 `pMemoryLoad`  
 <span data-ttu-id="44ef5-106">[out] Pointeur vers le pourcentage approximatif de mémoire physique totale qui est actuellement en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="44ef5-106">[out] A pointer to the approximate percentage of total physical memory that is currently in use.</span></span>  
  
 `pAvailableBytes`  
 <span data-ttu-id="44ef5-107">[out] Pointeur vers le nombre d’octets disponibles pour le common language runtime (CLR).</span><span class="sxs-lookup"><span data-stu-id="44ef5-107">[out] A pointer to the number of bytes available to the common language runtime (CLR).</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="44ef5-108">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="44ef5-108">Return Value</span></span>  
  
|<span data-ttu-id="44ef5-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="44ef5-109">HRESULT</span></span>|<span data-ttu-id="44ef5-110">Description</span><span class="sxs-lookup"><span data-stu-id="44ef5-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="44ef5-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="44ef5-111">S_OK</span></span>|<span data-ttu-id="44ef5-112">`GetMemoryLoad`retourné avec succès.</span><span class="sxs-lookup"><span data-stu-id="44ef5-112">`GetMemoryLoad` returned successfully.</span></span>|  
|<span data-ttu-id="44ef5-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="44ef5-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="44ef5-114">Le CLR n’a pas été chargé dans un processus ou le CLR est dans un état dans lequel il ne peut pas exécuter du code managé ou traiter l’appel avec succès.</span><span class="sxs-lookup"><span data-stu-id="44ef5-114">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="44ef5-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="44ef5-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="44ef5-116">L’appel a expiré.</span><span class="sxs-lookup"><span data-stu-id="44ef5-116">The call timed out.</span></span>|  
|<span data-ttu-id="44ef5-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="44ef5-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="44ef5-118">L’appelant ne possède pas le verrou.</span><span class="sxs-lookup"><span data-stu-id="44ef5-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="44ef5-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="44ef5-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="44ef5-120">Un événement a été annulé alors qu’un thread bloqué ou une fibre l’attendait.</span><span class="sxs-lookup"><span data-stu-id="44ef5-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="44ef5-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="44ef5-121">E_FAIL</span></span>|<span data-ttu-id="44ef5-122">Une défaillance grave et inconnue s’est produite.</span><span class="sxs-lookup"><span data-stu-id="44ef5-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="44ef5-123">Lorsqu’une méthode retourne E_FAIL, le CLR n’est plus utilisable dans le processus.</span><span class="sxs-lookup"><span data-stu-id="44ef5-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="44ef5-124">Les appels suivants aux méthodes d’hébergement retournent HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="44ef5-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="44ef5-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="44ef5-125">Remarks</span></span>  
 <span data-ttu-id="44ef5-126">`GetMemoryLoad`encapsule Win32 `GlobalMemoryStatus` (fonction).</span><span class="sxs-lookup"><span data-stu-id="44ef5-126">`GetMemoryLoad` wraps the Win32 `GlobalMemoryStatus` function.</span></span> <span data-ttu-id="44ef5-127">La valeur de `pMemoryLoad` est l’équivalent de la `dwMemoryLoad` champ dans le `MEMORYSTATUS` structure retournée à partir de `GlobalMemoryStatus`.</span><span class="sxs-lookup"><span data-stu-id="44ef5-127">The value of `pMemoryLoad` is the equivalent of the `dwMemoryLoad` field in the `MEMORYSTATUS` structure returned from `GlobalMemoryStatus`.</span></span>  
  
 <span data-ttu-id="44ef5-128">Le runtime utilise la valeur de retour comme heuristique pour le garbage collector.</span><span class="sxs-lookup"><span data-stu-id="44ef5-128">The runtime uses the return value as a heuristic for the garbage collector.</span></span> <span data-ttu-id="44ef5-129">Par exemple, si l’hôte indique que la majorité de la mémoire est en cours d’utilisation, le garbage collector peut choisir collecter à partir de plusieurs générations afin d’augmenter la quantité de mémoire peut potentiellement devenir disponible.</span><span class="sxs-lookup"><span data-stu-id="44ef5-129">For example, if the host reports that the majority of memory is in use, the garbage collector may elect to collect from multiple generations to increase the amount of memory that can potentially become available.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="44ef5-130">Spécifications</span><span class="sxs-lookup"><span data-stu-id="44ef5-130">Requirements</span></span>  
 <span data-ttu-id="44ef5-131">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="44ef5-131">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="44ef5-132">**En-tête :** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="44ef5-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="44ef5-133">**Bibliothèque :** inclus en tant que ressource dans MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="44ef5-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="44ef5-134">**Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="44ef5-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="44ef5-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="44ef5-135">See Also</span></span>  
 <xref:System.GC?displayProperty=nameWithType>  
 [<span data-ttu-id="44ef5-136">IHostMemoryManager (Interface)</span><span class="sxs-lookup"><span data-stu-id="44ef5-136">IHostMemoryManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)