---
title: "CorOpenFlags, énumération"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CorOpenFlags
api_location: mscoree.dll
api_type: COM
f1_keywords: CorOpenFlags
helpviewer_keywords: CorOpenFlags enumeration [.NET Framework metadata]
ms.assetid: e27a83b5-2698-4996-9032-1e0fed8b91ca
topic_type: apiref
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: c7599a4b85a166aedd7a2293b79699b3ef03d14d
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="coropenflags-enumeration"></a>CorOpenFlags, énumération
Contient des valeurs d'indicateurs qui contrôlent le comportement des métadonnées après ouverture des fichiers manifeste.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
typedef enum CorOpenFlags  
{  
    ofRead              =   0x00000000,  
    ofWrite             =   0x00000001,  
    ofReadWriteMask     =   0x00000001,  
    ofCopyMemory        =   0x00000002,  
    ofCacheImage        =   0x00000004,  
    ofManifestMetadata  =   0x00000008,  
    ofReadOnly          =   0x00000010,  
    ofTakeOwnership     =   0x00000020,  
    ofCacheImage        =   0x00000004,  
    ofNoTypeLib         =   0x00000080,  
    ofNoTransform       =   0x00001000,  
    ofReserved1         =   0x00000100,  
    ofReserved2         =   0x00000200,  
    ofReserved          =   0xffffff40  
} CorOpenFlags;  
```  
  
## <a name="members"></a>Membres  
  
|Membre|Description|  
|------------|-----------------|  
|`ofRead`|Indique que le fichier doit être ouvert en lecture seule.|  
|`ofWrite`|Indique que le fichier doit être ouvert en écriture.<br /><br /> Si vous utilisez l'indicateur `ofWrite` lors de l'ouverture d'un fichier .winmd, vous devez aussi passer l'indicateur `ofNoTransform`.|  
|`ofReadWriteMask`|Un masque pour la lecture et l'écriture.|  
|`ofCopyMemory`|Indique que le fichier doit être lu en mémoire. Les métadonnées doivent gérer leur propre copie.|  
|`ofCacheImage`|Obsolète. Cet indicateur est ignoré.|  
|`ofManifestMetadata`|Obsolète. Cet indicateur est ignoré.|  
|`ofReadOnly`|Indique que le fichier doit être ouvert pour lecture et qu’un appel à `QueryInterface` pour un [IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md) ne peut pas être établie.|  
|`ofTakeOwnership`|Indique que la mémoire a été allouée à l’aide d’un appel à [CoTaskMemAlloc](http://msdn.microsoft.com/en-us/c4cb588d-9482-4f90-a92e-75b604540d5c) et sera libérée par les métadonnées.|  
|`ofNoTypeLib`|Obsolète. Cet indicateur est ignoré.|  
|`ofNoTransform`|Indique que les transformations automatiques de fichiers .winmd doivent être désactivées. En d'autres termes, la projection d'un type Windows Runtime vers un type .NET Framework doit être désactivée. Pour plus d’informations, consultez [Underneath the Hood avec .NET et Windows Runtime](http://msdn.microsoft.com/magazine/jj651569.aspx).|  
|`ofReserved1`|Réservé à un usage interne.|  
|`ofReserved2`|Réservé à un usage interne.|  
|`ofReserved`|Réservé à un usage interne.|  
  
## <a name="requirements"></a>Spécifications  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorHdr.h  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Énumérations de métadonnées](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
