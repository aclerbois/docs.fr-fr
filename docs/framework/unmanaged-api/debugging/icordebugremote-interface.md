---
title: ICorDebugRemote, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugRemote
api_location: CorDebug.dll
api_type: COM
f1_keywords: ICorDebugRemote
helpviewer_keywords: ICorDebugRemote interface [.NET Framework debugging]
ms.assetid: 53d073c6-fa02-40d2-82e1-b9452bb6abaa
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: a6195b53d11877c6b7b2a52c3fd8d194dfb51810
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugremote-interface"></a>ICorDebugRemote, interface
Fournit la possibilité de lancer ou de joindre un débogueur managé à un processus distant cible.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
interface ICorDebugRemote : IUnknown  
{  
    HRESULT CreateProcessEx  
      (  
      [in] ICorDebugRemoteTarget *     pRemoteTarget,  
      [in] LPCWSTR                     lpApplicationName,  
      [in] LPWSTR                      lpCommandLine,  
      [in] LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
      [in] LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
      [in] BOOL                        bInheritHandles,  
      [in] DWORD                       dwCreationFlags,  
      [in] PVOID                       lpEnvironment,  
      [in] LPCWSTR                     lpCurrentDirectory,  
      [in] LPSTARTUPINFOW              lpStartupInfo,  
      [in] LPPROCESS_INFORMATION       lpProcessInformation,  
      [in] CorDebugCreateProcessFlags  debuggingFlags,  
      [out] ICorDebugProcess **        ppProcess  
      );  
  
    HRESULT DebugActiveProcessEx  
      (  
      [in] ICorDebugRemoteTarget *   pRemoteTarget,  
      [in] DWORD                     dwProcessId,  
      [in] BOOL                      fWin32Attach,  
      [out] ICorDebugProcess **      ppProcess  
      );  
};  
```  
  
## <a name="methods"></a>Méthodes  
  
|Méthode|Description|  
|------------|-----------------|  
|[ICorDebugRemote::CreateProcessEx (méthode)](../../../../docs/framework/unmanaged-api/debugging/icordebugremote-createprocessex-method.md)|Crée un processus sur un ordinateur distant pour le débogage managé.|  
|[ICorDebugRemote::DebugActiveProcessEx (méthode)](../../../../docs/framework/unmanaged-api/debugging/icordebugremote-debugactiveprocessex-method.md)|Lance un processus sur un ordinateur distant sous le débogueur.|  
  
## <a name="remarks"></a>Remarques  
 Actuellement, cette fonctionnalité est prise en charge uniquement pour le débogage d’une cible d’une application basée sur Silverlight qui s’exécute sur un ordinateur Macintosh distant.  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :** 4.5, 4, 3.5 SP1  
  
## <a name="see-also"></a>Voir aussi  
 [ICorDebugRemoteTarget (Interface)](../../../../docs/framework/unmanaged-api/debugging/icordebugremotetarget-interface.md)  
 [ICorDebug (Interface)](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)  
    
 [Interfaces de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
