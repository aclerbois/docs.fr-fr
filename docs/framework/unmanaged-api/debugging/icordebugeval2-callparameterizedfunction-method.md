---
title: "ICorDebugEval2::CallParameterizedFunction, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugEval2.CallParameterizedFunction
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugEval2::CallParameterizedFunction
helpviewer_keywords:
- ICorDebugEval2::CallParameterizedFunction method [.NET Framework debugging]
- CallParameterizedFunction method [.NET Framework debugging]
ms.assetid: 72f54a45-dbe6-4bb4-8c99-e879a27368e5
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 720d9c4fb9b997538ee2bb18ac7987350f6bfb57
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugeval2callparameterizedfunction-method"></a>ICorDebugEval2::CallParameterizedFunction, méthode
Définit un appel à ICorDebugFunction spécifié, qui peut être imbriquée dans une classe dont le constructeur prend <xref:System.Type> paramètres, ou peut lui-même prendre <xref:System.Type> paramètres.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT CallParameterizedFunction (  
    [in] ICorDebugFunction     *pFunction,  
    [in] ULONG32               nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType *ppTypeArgs[],  
    [in] ULONG32               nArgs,  
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]  
);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `pFunction`  
 [in] Un pointeur vers un `ICorDebugFunction` objet qui représente la fonction à appeler.  
  
 `nTypeArgs`  
 [in] Le nombre d’arguments que la fonction accepte.  
  
 `ppTypeArgs`  
 [in] Tableau de pointeurs, chacun pointant vers un objet ICorDebugType qui représente un argument de fonction.  
  
 `nArgs`  
 [in] Le nombre de valeurs passées dans la fonction.  
  
 `ppArgs`  
 [in] Un tableau de pointeurs, chacun pointant vers un objet ICorDebugValue qui représente une valeur passée dans un argument de fonction.  
  
## <a name="remarks"></a>Remarques  
 `CallParameterizedFunction`est semblable à [ICorDebugEval::CallFunction](../../../../docs/framework/unmanaged-api/debugging/icordebugeval-callfunction-method.md) , sauf que la fonction peut être à l’intérieur d’une classe avec des paramètres de type, peut prendre elle-même les paramètres de type, ou les deux. Les arguments de type convient tout d’abord pour la classe, puis pour la fonction.  
  
 Si la fonction est dans un domaine d’application différent, une transition se produit. Toutefois, tous les arguments de type et la valeur doivent être dans le domaine d’application cible.  
  
 L’évaluation de fonction peut être effectuée uniquement dans les scénarios limités. Si `CallParameterizedFunction` ou `ICorDebugEval::CallFunction` échoue, le HRESULT retourné indiquera la raison possible plus générale de l’échec.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
