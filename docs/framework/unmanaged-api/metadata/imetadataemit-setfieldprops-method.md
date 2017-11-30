---
title: "IMetaDataEmit::SetFieldProps, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataEmit.SetFieldProps
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataEmit::SetFieldProps
helpviewer_keywords:
- IMetaDataEmit::SetFieldProps method [.NET Framework metadata]
- SetFieldProps method [.NET Framework metadata]
ms.assetid: 47132dda-fa92-4bd1-ae4b-24cd9a60665a
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 5f031e79deab57184043eaa44d2d8a3d369187c7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataemitsetfieldprops-method"></a><span data-ttu-id="9c4e3-102">IMetaDataEmit::SetFieldProps, méthode</span><span class="sxs-lookup"><span data-stu-id="9c4e3-102">IMetaDataEmit::SetFieldProps Method</span></span>
<span data-ttu-id="9c4e3-103">Définit ou met à jour la valeur par défaut pour le champ référencé par le jeton de champ spécifié.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-103">Sets or updates the default value for the field referenced by the specified field token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9c4e3-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9c4e3-104">Syntax</span></span>  
  
```  
HRESULT SetFieldProps (  
    [in]  mdFieldDef  fd,   
    [in]  DWORD       dwFieldFlags,   
    [in]  DWORD       dwCPlusTypeFlag,   
    [in]  void const  *pValue,   
    [in]  ULONG       cchValue   
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="9c4e3-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9c4e3-105">Parameters</span></span>  
 `fd`  
 <span data-ttu-id="9c4e3-106">[in] Le jeton pour le champ cible.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-106">[in] The token for the target field.</span></span>  
  
 `dwFieldFlags`  
 <span data-ttu-id="9c4e3-107">[in] Attributs de champ.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-107">[in] Field attributes.</span></span> <span data-ttu-id="9c4e3-108">Il s’agit d’un masque de bits de `CorFieldAttr` valeurs.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-108">This is a bitmask of `CorFieldAttr` values.</span></span>  
  
 `dwCPlusTypeFlag`  
 <span data-ttu-id="9c4e3-109">[in] Le `ELEMENT_TYPE_`  *\**  pour la valeur de constante.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-109">[in] The `ELEMENT_TYPE_`*\** for the constant value.</span></span> <span data-ttu-id="9c4e3-110">Il s’agit d’un `CorElementType` valeur.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-110">This is a `CorElementType` value.</span></span> <span data-ttu-id="9c4e3-111">Si une constante n’est pas définie, définissez cette valeur sur `ELEMENT_TYPE_END`.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-111">If a constant is not being defined, set this value to `ELEMENT_TYPE_END`.</span></span>  
  
 `pValue`  
 <span data-ttu-id="9c4e3-112">[in] La valeur de constante pour le champ.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-112">[in] The constant value for the field.</span></span>  
  
 `cchValue`  
 <span data-ttu-id="9c4e3-113">[in] La taille, en caractères Unicode de `pValue`.</span><span class="sxs-lookup"><span data-stu-id="9c4e3-113">[in] The size, in Unicode characters, of `pValue`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9c4e3-114">Spécifications</span><span class="sxs-lookup"><span data-stu-id="9c4e3-114">Requirements</span></span>  
 <span data-ttu-id="9c4e3-115">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9c4e3-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9c4e3-116">**En-tête :** Cor.h</span><span class="sxs-lookup"><span data-stu-id="9c4e3-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="9c4e3-117">**Bibliothèque :** utilisé en tant que ressource dans MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="9c4e3-117">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="9c4e3-118">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9c4e3-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9c4e3-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9c4e3-119">See Also</span></span>  
 [<span data-ttu-id="9c4e3-120">IMetaDataEmit (Interface)</span><span class="sxs-lookup"><span data-stu-id="9c4e3-120">IMetaDataEmit Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)  
 [<span data-ttu-id="9c4e3-121">IMetaDataEmit2 (Interface)</span><span class="sxs-lookup"><span data-stu-id="9c4e3-121">IMetaDataEmit2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)