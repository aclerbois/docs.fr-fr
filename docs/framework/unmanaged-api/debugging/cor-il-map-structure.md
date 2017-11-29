---
title: COR_IL_MAP, structure
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_IL_MAP
api_location: mscordbi.dll
api_type: COM
f1_keywords: COR_IL_MAP
helpviewer_keywords: COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: ffcd4dc32f2f509dd9421b2c24781fb2819418b5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="corilmap-structure"></a><span data-ttu-id="a43b4-102">COR_IL_MAP, structure</span><span class="sxs-lookup"><span data-stu-id="a43b4-102">COR_IL_MAP Structure</span></span>
<span data-ttu-id="a43b4-103">Spécifie des modifications dans le décalage relatif d'une fonction.</span><span class="sxs-lookup"><span data-stu-id="a43b4-103">Specifies changes in the relative offset of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a43b4-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a43b4-104">Syntax</span></span>  
  
```  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;   
    ULONG32 newOffset;   
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a><span data-ttu-id="a43b4-105">Membres</span><span class="sxs-lookup"><span data-stu-id="a43b4-105">Members</span></span>  
  
|<span data-ttu-id="a43b4-106">Membre</span><span class="sxs-lookup"><span data-stu-id="a43b4-106">Member</span></span>|<span data-ttu-id="a43b4-107">Description</span><span class="sxs-lookup"><span data-stu-id="a43b4-107">Description</span></span>|  
|------------|-----------------|  
|`oldOffset`|<span data-ttu-id="a43b4-108">L’ancien Microsoft offset intermediate language (MSIL) par rapport au début de la fonction.</span><span class="sxs-lookup"><span data-stu-id="a43b4-108">The old Microsoft intermediate language (MSIL) offset relative to the beginning of the function.</span></span>|  
|`newOffset`|<span data-ttu-id="a43b4-109">Nouvel offset MSIL par rapport au début de la fonction.</span><span class="sxs-lookup"><span data-stu-id="a43b4-109">The new MSIL offset relative to the beginning of the function.</span></span>|  
|`fAccurate`|<span data-ttu-id="a43b4-110">`true`Si le mappage est avéré précis ; dans le cas contraire, `false`.</span><span class="sxs-lookup"><span data-stu-id="a43b4-110">`true` if the mapping is known to be accurate; otherwise, `false`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a43b4-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="a43b4-111">Remarks</span></span>  
 <span data-ttu-id="a43b4-112">Le format de la carte est le suivant : le débogueur suppose que `oldOffset` fait référence à un offset MSIL dans le code MSIL non modifié d’origine.</span><span class="sxs-lookup"><span data-stu-id="a43b4-112">The format of the map is as follows: The debugger will assume that `oldOffset` refers to an MSIL offset within the original, unmodified MSIL code.</span></span> <span data-ttu-id="a43b4-113">Le `newOffset` paramètre fait référence à l’offset MSIL correspondant dans le nouveau code instrumenté.</span><span class="sxs-lookup"><span data-stu-id="a43b4-113">The `newOffset` parameter refers to the corresponding MSIL offset within the new, instrumented code.</span></span>  
  
 <span data-ttu-id="a43b4-114">Pour exécuter pas à pas pour fonctionner correctement, les conditions suivantes doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="a43b4-114">For stepping to work properly, the following requirements should be met:</span></span>  
  
-   <span data-ttu-id="a43b4-115">Le mappage doit être trié par ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="a43b4-115">The map should be sorted in ascending order.</span></span>  
  
-   <span data-ttu-id="a43b4-116">Code MSIL instrumenté ne doit pas être réorganisé.</span><span class="sxs-lookup"><span data-stu-id="a43b4-116">Instrumented MSIL code should not be reordered.</span></span>  
  
-   <span data-ttu-id="a43b4-117">Code MSIL d’origine ne doit pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="a43b4-117">Original MSIL code should not be removed.</span></span>  
  
-   <span data-ttu-id="a43b4-118">Le mappage doit inclure des entrées pour mapper tous les points de séquence dans le fichier du programme (PDB) de la base de données.</span><span class="sxs-lookup"><span data-stu-id="a43b4-118">The map should include entries to map all the sequence points from the program database (PDB) file.</span></span>  
  
 <span data-ttu-id="a43b4-119">Le mappage n’interpole pas les entrées manquantes.</span><span class="sxs-lookup"><span data-stu-id="a43b4-119">The map does not interpolate missing entries.</span></span> <span data-ttu-id="a43b4-120">L’exemple suivant montre un mappage et ses résultats.</span><span class="sxs-lookup"><span data-stu-id="a43b4-120">The following example shows a map and its results.</span></span>  
  
 <span data-ttu-id="a43b4-121">Carte :</span><span class="sxs-lookup"><span data-stu-id="a43b4-121">Map:</span></span>  
  
-   <span data-ttu-id="a43b4-122">ancien offset 0, nouvel offset 0</span><span class="sxs-lookup"><span data-stu-id="a43b4-122">0 old offset, 0 new offset</span></span>  
  
-   <span data-ttu-id="a43b4-123">ancien offset 5, nouvel offset 10</span><span class="sxs-lookup"><span data-stu-id="a43b4-123">5 old offset, 10 new offset</span></span>  
  
-   <span data-ttu-id="a43b4-124">ancien offset 9, nouvel offset 20</span><span class="sxs-lookup"><span data-stu-id="a43b4-124">9 old offset, 20 new offset</span></span>  
  
 <span data-ttu-id="a43b4-125">Résultats :</span><span class="sxs-lookup"><span data-stu-id="a43b4-125">Results:</span></span>  
  
-   <span data-ttu-id="a43b4-126">Un ancien offset de 0, 1, 2, 3 ou 4 sera mappé à un nouvel offset de 0.</span><span class="sxs-lookup"><span data-stu-id="a43b4-126">An old offset of 0, 1, 2, 3, or 4 will be mapped to a new offset of 0.</span></span>  
  
-   <span data-ttu-id="a43b4-127">Un ancien offset de 5, 6, 7 ou 8 sera mappé au nouvel offset 10.</span><span class="sxs-lookup"><span data-stu-id="a43b4-127">An old offset of 5, 6, 7, or 8 will be mapped to new offset 10.</span></span>  
  
-   <span data-ttu-id="a43b4-128">Un ancien offset de 9 ou version ultérieure sera mappé au nouvel offset 20.</span><span class="sxs-lookup"><span data-stu-id="a43b4-128">An old offset of 9 or higher will be mapped to new offset 20.</span></span>  
  
-   <span data-ttu-id="a43b4-129">Un nouvel offset de 0, 1, 2, 3, 4, 5, 6, 7, 8 ou 9 sera mappé à l’ancien offset 0.</span><span class="sxs-lookup"><span data-stu-id="a43b4-129">A new offset of 0, 1, 2, 3, 4, 5, 6, 7, 8, or 9 will be mapped to old offset 0.</span></span>  
  
-   <span data-ttu-id="a43b4-130">Un nouvel offset de 10, 11, 12, 13, 14, 15, 16, 17, 18 ou 19 sera mappé à l’ancien offset 5.</span><span class="sxs-lookup"><span data-stu-id="a43b4-130">A new offset of 10, 11, 12, 13, 14, 15, 16, 17, 18, or 19 will be mapped to old offset 5.</span></span>  
  
-   <span data-ttu-id="a43b4-131">Un nouvel offset de 20 ou supérieur sera mappé à l’ancien offset 9.</span><span class="sxs-lookup"><span data-stu-id="a43b4-131">A new offset of 20 or higher will be mapped to old offset 9.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a43b4-132">Spécifications</span><span class="sxs-lookup"><span data-stu-id="a43b4-132">Requirements</span></span>  
 <span data-ttu-id="a43b4-133">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a43b4-133">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a43b4-134">**En-tête :** CorDebug.idl, CorProf.idl</span><span class="sxs-lookup"><span data-stu-id="a43b4-134">**Header:** CorDebug.idl, CorProf.idl</span></span>  
  
 <span data-ttu-id="a43b4-135">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a43b4-135">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a43b4-136">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a43b4-136">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a43b4-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a43b4-137">See Also</span></span>  
 [<span data-ttu-id="a43b4-138">Structures de débogage</span><span class="sxs-lookup"><span data-stu-id="a43b4-138">Debugging Structures</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)  
 [<span data-ttu-id="a43b4-139">Débogage</span><span class="sxs-lookup"><span data-stu-id="a43b4-139">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)