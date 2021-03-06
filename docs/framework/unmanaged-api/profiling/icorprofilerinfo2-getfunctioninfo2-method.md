---
title: "ICorProfilerInfo2::GetFunctionInfo2, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo2.GetFunctionInfo2
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo2::GetFunctionInfo2
helpviewer_keywords:
- GetFunctionInfo2 method [.NET Framework profiling]
- ICorProfilerInfo2::GetFunctionInfo2 method [.NET Framework profiling]
ms.assetid: 0aa60f24-8bbd-4c83-83c5-86ad191b1d82
topic_type: apiref
caps.latest.revision: "18"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 8b0c288b88c868bc6e324ec57b3956344f03f34e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo2getfunctioninfo2-method"></a>ICorProfilerInfo2::GetFunctionInfo2, méthode
Obtient la classe parente, le jeton de métadonnées et le `ClassID` de chaque argument de type, le cas échéant, d'une fonction.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT GetFunctionInfo2(  
    [in]  FunctionID funcId,  
    [in]  COR_PRF_FRAME_INFO frameInfo,  
    [out] ClassID *pClassId,  
    [out] ModuleID *pModuleId,  
    [out] mdToken *pToken,  
    [in]  ULONG32 cTypeArgs,  
    [out] ULONG32 *pcTypeArgs,  
    [out] ClassID typeArgs[]);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `funcId`  
 [in] ID de la fonction pour laquelle obtenir la classe parente et d'autres informations.  
  
 `frameInfo`  
 [in] Valeur `COR_PRF_FRAME_INFO` qui pointe vers les informations sur un frame de pile.  
  
 `pClassId`  
 [out] Pointeur vers la classe parente de la fonction.  
  
 `pModuleId`  
 [out] Pointeur vers le module dans lequel la classe parente de la fonction est définie.  
  
 `pToken`  
 [out] Pointeur vers le jeton de métadonnées de la fonction.  
  
 `cTypeArgs`  
 [in] Taille du tableau `typeArgs`.  
  
 `pcTypeArgs`  
 [out] Pointeur vers le nombre total de valeurs `ClassID`.  
  
 `typeArgs`  
 [out] Tableau de valeurs `ClassID` qui représentent chacune l'ID d'un argument de type de la fonction. Suite au retour de la méthode, `typeArgs` contient une partie ou la totalité des valeurs `ClassID`.  
  
## <a name="remarks"></a>Remarques  
 Le code du profileur peut appeler [ICorProfilerInfo::GetModuleMetaData](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md) pour obtenir un [métadonnées](../../../../docs/framework/unmanaged-api/metadata/index.md) interface pour un module donné. Le jeton de métadonnées qui est retourné à l'emplacement référencé par `pToken` peut alors servir à accéder aux métadonnées pour la fonction.  
  
 L'ID de classe et les arguments de type retournés via les paramètres `pClassId` et `typeArgs` dépendent de la valeur qui est passée dans le paramètre `frameInfo`, comme indiqué dans le tableau suivant.  
  
|Valeur du paramètre `frameInfo`.|Résultat|  
|----------------------------------------|------------|  
|Valeur `COR_PRF_FRAME_INFO` obtenue d'un rappel `FunctionEnter2`|La valeur `ClassID`, retournée dans l'emplacement référencé par `pClassId`, et tous les arguments de type, retournés dans le tableau `typeArgs`, seront exacts.|  
|`COR_PRF_FRAME_INFO` obtenu à partir d'une source autre qu'un rappel `FunctionEnter2`|La valeur `ClassID` et les arguments de type exacts ne peuvent pas être déterminés. Autrement dit, la valeur `ClassID` peut être null et certains arguments de type peuvent être retournés comme <xref:System.Object>.|  
|Zéro|La valeur `ClassID` et les arguments de type exacts ne peuvent pas être déterminés. Autrement dit, la valeur `ClassID` peut être null et certains arguments de type peuvent être retournés comme <xref:System.Object>.|  
  
 Suite au retour de `GetFunctionInfo2`, vous devez vérifier que la mémoire tampon `typeArgs` est suffisamment grande pour contenir toutes les valeurs `ClassID`. Pour ce faire, comparez la valeur vers laquelle `pcTypeArgs` pointe à celle du paramètre `cTypeArgs`. Si `pcTypeArgs` pointe vers une valeur supérieure à `cTypeArgs` divisée par la taille d'une valeur `ClassID`, allouez une mémoire tampon `pcTypeArgs` plus grande, mettez à jour `cTypeArgs` pour refléter la nouvelle taille et rappelez `GetFunctionInfo2`.  
  
 Vous pouvez également commencer par appeler `GetFunctionInfo2` avec une mémoire tampon `pcTypeArgs` de longueur nulle pour obtenir la taille correcte de la mémoire tampon. Vous pouvez ensuite affecter à la taille de la mémoire tampon la valeur retournée dans `pcTypeArgs` divisée par la taille d'une valeur `ClassID` et rappeler `GetFunctionInfo2`.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorProf.idl, CorProf.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [ICorProfilerInfo (Interface)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [ICorProfilerInfo2 (Interface)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)  
 [Interfaces de profilage](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [Profilage](../../../../docs/framework/unmanaged-api/profiling/index.md)
