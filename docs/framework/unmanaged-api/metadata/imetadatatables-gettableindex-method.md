---
title: "IMetaDataTables::GetTableIndex, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataTables.GetTableIndex
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataTables::GetTableIndex
helpviewer_keywords:
- GetTableIndex method [.NET Framework metadata]
- IMetaDataTables::GetTableIndex method [.NET Framework metadata]
ms.assetid: c6ec3800-e0d9-4387-afb8-ddc0b818114c
topic_type: apiref
caps.latest.revision: "16"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: d49e1258011d68a6278d1c40500386024a2cb0d2
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="imetadatatablesgettableindex-method"></a><span data-ttu-id="fc2c0-102">IMetaDataTables::GetTableIndex, méthode</span><span class="sxs-lookup"><span data-stu-id="fc2c0-102">IMetaDataTables::GetTableIndex Method</span></span>
<span data-ttu-id="fc2c0-103">Obtient l’index de la table référencée par le jeton spécifié.</span><span class="sxs-lookup"><span data-stu-id="fc2c0-103">Gets the index for the table referenced by the specified token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fc2c0-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="fc2c0-104">Syntax</span></span>  
  
```  
HRESULT GetTableIndex (  
    [in]  ULONG   token,  
    [out] ULONG   *pixTbl  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="fc2c0-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="fc2c0-105">Parameters</span></span>  
 `token`  
 <span data-ttu-id="fc2c0-106">[in] Le jeton qui fait référence à la table.</span><span class="sxs-lookup"><span data-stu-id="fc2c0-106">[in] The token that references the table.</span></span>  
  
 `pixTbl`  
 <span data-ttu-id="fc2c0-107">[out] Pointeur vers l’index retourné pour la table référencée.</span><span class="sxs-lookup"><span data-stu-id="fc2c0-107">[out] A pointer to the returned index for the referenced table.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fc2c0-108">Remarques</span><span class="sxs-lookup"><span data-stu-id="fc2c0-108">Remarks</span></span>  
 <span data-ttu-id="fc2c0-109">Nous déconseillons l’utilisation de cette méthode, car elle ne retourne pas de résultats cohérents.</span><span class="sxs-lookup"><span data-stu-id="fc2c0-109">We do not recommend the use of this method, because it does not return consistent results.</span></span> <span data-ttu-id="fc2c0-110">Pour plus d’informations sur la table GUID, consultez la documentation du Common Language Infrastructure (CLI), en particulier « Partition II : Metadata Definition et Semantics ».</span><span class="sxs-lookup"><span data-stu-id="fc2c0-110">For information about the GUID table, see the Common Language Infrastructure (CLI) documentation, especially "Partition II: Metadata Definition and Semantics".</span></span> <span data-ttu-id="fc2c0-111">La documentation est disponible en ligne. Consultez [ECMA C# and Common Language Infrastructure Standards](http://go.microsoft.com/fwlink/?LinkID=99212) sur MSDN et [Standard ECMA-335 - Common Language Infrastructure (CLI)](http://go.microsoft.com/fwlink/?LinkID=65552) sur le site web d’Ecma International.</span><span class="sxs-lookup"><span data-stu-id="fc2c0-111">The documentation is available online; see [ECMA C# and Common Language Infrastructure Standards](http://go.microsoft.com/fwlink/?LinkID=99212) on MSDN and [Standard ECMA-335 - Common Language Infrastructure (CLI)](http://go.microsoft.com/fwlink/?LinkID=65552) on the Ecma International Web site.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fc2c0-112">Spécifications</span><span class="sxs-lookup"><span data-stu-id="fc2c0-112">Requirements</span></span>  
 <span data-ttu-id="fc2c0-113">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="fc2c0-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fc2c0-114">**En-tête :** Cor.h</span><span class="sxs-lookup"><span data-stu-id="fc2c0-114">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="fc2c0-115">**Bibliothèque :** utilisé en tant que ressource dans MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="fc2c0-115">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="fc2c0-116">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fc2c0-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc2c0-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fc2c0-117">See Also</span></span>  
 [<span data-ttu-id="fc2c0-118">IMetaDataTables (Interface)</span><span class="sxs-lookup"><span data-stu-id="fc2c0-118">IMetaDataTables Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)  
 [<span data-ttu-id="fc2c0-119">IMetaDataTables2 (Interface)</span><span class="sxs-lookup"><span data-stu-id="fc2c0-119">IMetaDataTables2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)