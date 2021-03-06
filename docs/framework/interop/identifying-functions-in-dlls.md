---
title: Identification des fonctions des DLL
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- platform invoke, identifying functions
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- identifying DLL functions
- DLL functions
ms.assetid: 3e3f6780-6d90-4413-bad7-ba641220364d
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 1b5aa725d30e280d672724c7b7f4fd11a848a3ae
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="identifying-functions-in-dlls"></a>Identification des fonctions des DLL
L’identité d’une fonction DLL est composée des éléments suivants :  
  
-   ordinal ou nom de la fonction ;  
  
-   nom du fichier DLL dans lequel l’implémentation figure.  
  
 Par exemple, la spécification de la fonction **MessageBox** dans User32.dll identifie la fonction (**MessageBox**) et son emplacement (User32.dll, User32 ou user32). L’interface de programmation d’applications Microsoft Windows (API Win32) peut comporter deux versions de chaque fonction qui gère les caractères et les chaînes : une version ANSI pour les caractères à 1 octet et une version Unicode pour les caractères à 2 octets. Quand le jeu de caractères représenté par le champ <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> n’est pas spécifié, sa valeur par défaut est ANSI. Certaines fonctions peuvent posséder plus de deux versions.  
  
 **MessageBoxA** est le point d’entrée ANSI de la fonction **MessageBox** ; **MessageBoxW** correspond à la version Unicode. Vous pouvez obtenir une liste de noms de fonctions pour une DLL spécifique, telle que user32.dll, en exécutant une variété d’outils en ligne de commande. Par exemple, vous pouvez utiliser `dumpbin /exports user32.dll` ou `link /dump /exports user32.dll` pour obtenir des noms de fonctions.  
  
 Vous pouvez renommer une fonction non managée à votre convenance dans votre code à partir du moment où vous mappez le nouveau nom au point d’entrée d’origine dans la DLL. Pour obtenir des instructions sur l’attribution d’un nouveau nom à une fonction DLL non managée dans du code source managé, consultez [Spécification d’un point d’entrée](../../../docs/framework/interop/specifying-an-entry-point.md).  
  
 L’appel de code non managé vous permet de contrôler une partie importante du système d’exploitation en appelant des fonctions dans l’interface API Win32 et dans d’autres DLL. Outre l’interface API Win32, de nombreuses autres interfaces API et DLL sont à votre disposition via l’appel de code non managé.  
  
 Le tableau suivant décrit plusieurs DLL fréquemment utilisées dans l’interface API Win32.  
  
|DLL|Description du contenu|  
|---------|-----------------------------|  
|GDI32.dll|Fonctions GDI (Graphics Device Interface) pour la sortie d’appareils, telles que celles pour la gestion du dessin et des polices.|  
|Kernel32.dll|Fonctions du système d’exploitation de bas niveau pour la gestion de la mémoire et des ressources.|  
|User32.dll|Fonctions de gestion Windows pour les messages, les minuteries, les menus et les communications.|  
  
 Pour obtenir une documentation complète sur l’interface API Win32, consultez le Kit Platform SDK. Pour afficher des exemples montrant comment construire des déclarations .NET à utiliser avec l’appel de code non managé, consultez [Marshaling de données à l’aide de l’appel de code non managé](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Consommation de fonctions DLL non managées](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)  
 [Spécification d'un point d'entrée](../../../docs/framework/interop/specifying-an-entry-point.md)  
 [Création d’une classe pour contenir des fonctions DLL](../../../docs/framework/interop/creating-a-class-to-hold-dll-functions.md)  
 [Création de prototypes dans du code managé](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)  
 [Appel à une fonction DLL](../../../docs/framework/interop/calling-a-dll-function.md)
