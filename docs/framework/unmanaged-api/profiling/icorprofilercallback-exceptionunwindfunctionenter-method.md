---
title: "ICorProfilerCallback::ExceptionUnwindFunctionEnter, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.ExceptionUnwindFunctionEnter
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::ExceptionUnwindFunctionEnter
helpviewer_keywords:
- ICorProfilerCallback::ExceptionUnwindFunctionEnter method [.NET Framework profiling]
- ExceptionUnwindFunctionEnter method [.NET Framework profiling]
ms.assetid: ea3dc625-5650-4bf4-8e67-01e42be065b1
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: cc41dc95776ca31178153402d2e145a3d2c13bf5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilercallbackexceptionunwindfunctionenter-method"></a>ICorProfilerCallback::ExceptionUnwindFunctionEnter, méthode
Notifie le profileur que la phase de déroulement de la gestion des exceptions a commencé à dérouler une fonction.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT ExceptionUnwindFunctionEnter(  
    [in] FunctionID functionId);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `functionId`  
 [in] L’ID de la fonction qui n’est pas vidée.  
  
## <a name="remarks"></a>Remarques  
 Le profileur ne doit pas bloquer dans son implémentation de cette méthode, car la pile ne peut pas être dans un état qui autorise le garbage collection, et par conséquent, le garbage collection préemptif ne peut pas être activé. Si le profileur bloque ici et le garbage collection est tenté, le runtime bloque jusqu'à ce que ce rappel retourne.  
  
 L’implémentation du profileur de cette méthode ne doit pas appeler dans du code managé ou de quelque manière qu’une allocation de mémoire managée.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorProf.idl, CorProf.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Interface ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [ExceptionUnwindFunctionLeave (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionleave-method.md)
