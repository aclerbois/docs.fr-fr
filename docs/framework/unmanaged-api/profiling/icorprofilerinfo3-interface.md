---
title: ICorProfilerInfo3, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo3
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo3
helpviewer_keywords: ICorProfilerInfo3 interface [.NET Framework profiling]
ms.assetid: 044a262f-0fa7-485d-b0c1-64cdc359c654
topic_type: apiref
caps.latest.revision: "17"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 471fbae929723fb47dd6bc2a65196de1800717bb
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo3-interface"></a>ICorProfilerInfo3, interface
Fournit des méthodes utilisées par les profileurs de code pour communiquer avec le Common Language Runtime (CLR) pour contrôler la surveillance des événements et demander des informations. Le `ICorProfilerInfo3` interface est une extension de la [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md) interface. Elle fournit de nouvelles méthodes prises en charge dans le [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] et ses versions ultérieures.  
  
## <a name="methods"></a>Méthodes  
  
|Méthode|Description|  
|------------|-----------------|  
|[EnumJITedFunctions (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md)|Retourne un énumérateur pour toutes les fonctions précédemment compilées juste-à-temps.|  
|[EnumModules (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enummodules-method.md)|Retourne un énumérateur qui fournit des méthodes pour itérer séquentiellement au sein d’une collection de modules managés chargés dans l’application.|  
|[GetAppDomainsContainingModule (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getappdomainscontainingmodule-method.md)|Obtient les identificateurs des domaines d'application dans lesquels le module donné a été chargé.|  
|[GetFunctionEnter3Info (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md)|Fournit les informations de frame et d’arguments de pile de la fonction signalée au profileur par la [FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md) fonction ; peut être appelée uniquement pendant le `FunctionEnter3WithInfo` rappel.|  
|[GetFunctionLeave3Info (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md)|Fournit le frame de pile et la valeur de retour de la fonction signalée au profileur par la [FunctionLeave3WithInfo fonction](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md) fonction ; peut être appelée uniquement pendant le `FunctionLeave3WithInfo` rappel.|  
|[GetFunctionTailcall3Info (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md)|Fournit le frame de pile de la fonction signalée au profileur par la [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md) fonction ; peut être appelée uniquement pendant le `FunctionTailcall3WithInfo` rappel.|  
|[GetModuleInfo2 (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)|Pour un ID de module donné, retourne le nom de fichier du module, l'ID de l'assembly parent du module et un masque de bits qui décrit les propriétés du module.|  
|[GetRuntimeInformation (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getruntimeinformation-method.md)|Fournit des informations de version sur le runtime en cours de profilage.|  
|[GetStringLayout2 (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getstringlayout2-method.md)|Obtient des informations sur la disposition d'un objet string.|  
|[GetThreadStaticAddress2 (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getthreadstaticaddress2-method.md)|Obtient l’adresse du champ static de thread spécifié qui est dans l’étendue du thread et du domaine d’application spécifiés.|  
|[RequestProfilerDetach (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-requestprofilerdetach-method.md)|Indique au runtime de détacher le profileur.|  
|[SetEnterLeaveFunctionHooks3 (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)|Spécifie les fonctions implémentées par le profileur qui seront appelées sur le [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md), [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md), et [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md) fonctions.|  
|[SetEnterLeaveFunctionHooks3WithInfo (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)|Spécifie les fonctions implémentées par le profileur qui seront appelées sur le [FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md), [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md), et [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md) raccordements de fonctions managées.|  
|[SetFunctionIDMapper2 (méthode)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)|Spécifie la fonction implémentée par le profileur qui sera appelée pour mapper des valeurs `FunctionID` sur d'autres valeurs, qui sont passées aux raccordements d'entrée/sortie de fonction du profileur. Cette méthode étend [ICorProfilerInfo::SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md) avec un paramètre que les profileurs peuvent utiliser pour distinguer les différents runtimes.|  
  
## <a name="remarks"></a>Remarques  
 Le CLR implémente les méthodes de l'interface `ICorProfilerInfo3` à l'aide du modèle libre de threads. Chaque méthode retourne un HRESULT pour indiquer la réussite ou l'échec. Pour obtenir la liste des codes de retour possibles, consultez le fichier CorError.h.  
  
 Le CLR passe une `ICorProfilerInfo3` interface à chaque profileur de code pendant l’initialisation, à l’aide de l’implémentation du profileur de la [ICorProfilerCallback::Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md) ou [ICorProfilerCallback3::I nitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) (méthode). Un profileur de code peut ensuite appeler les méthodes `ICorProfilerInfo3` pour obtenir des informations sur le code managé qui est en cours d'exécution sous le contrôle du CLR.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorProf.idl, CorProf.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Interfaces de profilage](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [ICorProfilerInfo (Interface)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
