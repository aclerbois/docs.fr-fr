---
title: Guide pratique pour supprimer un assembly du Global Assembly Cache
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- global assembly cache, removing assemblies
- strong-named assemblies, global assembly cache
- removing assemblies from global assembly cache
- deleting assemblies in global assembly cache
- Global Assembly Cache tool
- GAC (global assembly cache), removing assemblies
ms.assetid: acdcc588-b458-436d-876c-726de68244c1
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: a17478c350d789d320e97d6b50d6f5f9daaf6db3
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-remove-an-assembly-from-the-global-assembly-cache"></a>Guide pratique pour supprimer un assembly du Global Assembly Cache
Il existe deux façons de supprimer un assembly du Global Assembly Cache (GAC) :  
  
-   Utilisation de l’[outil Global Assembly Cache (Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md). Vous pouvez utiliser cette option pour désinstaller des assemblys que vous avez placés dans le GAC lors du développement et des tests.  
  
-   Utilisation de [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx). Utilisez cette option pour désinstaller des assemblys quand vous testez des packages d'installation et pour les systèmes de production.  
  
### <a name="removing-an-assembly-with-gacutilexe"></a>Suppression d'un assembly avec Gacutil.exe  
  
1.  À l'invite de commandes, tapez la commande suivante :  
  
     **gacutil –u** \<*nom_assembly*>  
  
     Dans cette commande, *nom_assembly* est le nom de l’assembly à supprimer du Global Assembly Cache.  
  
    > [!WARNING]
    >  Vous ne devez pas utiliser Gacutil.exe pour supprimer des assemblys sur des systèmes de production, en raison de la possibilité que l'assembly soit encore requis par certaines applications. Au lieu de cela, vous devez utiliser Windows Installer, qui conserve un comptage des références pour chaque assembly qu'il installe dans le GAC.  
  
 L'exemple suivant supprime un assembly nommé `hello.dll` du Global Assembly Cache.  
  
```  
gacutil -u hello  
```  
  
### <a name="removing-an-assembly-with-windows-installer"></a>Suppression d'un assembly avec Windows Installer  
  
1.  Dans l’application **Programmes et fonctionnalités** du **Panneau de configuration**, sélectionnez l’application que vous voulez désinstaller. Si le package d'installation a placé les assemblys dans le GAC, Windows Installer les supprime s'ils ne sont pas utilisés par une autre application.  
  
    > [!NOTE]
    >  Windows Installer conserve un comptage des références pour les assemblys installés dans le GAC. Un assembly est supprimé du GAC seulement quand son comptage des références atteint zéro, ce qui indique qu'il n'est utilisé par aucune application installée par un package Windows Installer.  
  
## <a name="see-also"></a>Voir aussi  
 [Utilisation d’assemblys et du Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
 [Guide pratique pour installer un assembly dans le Global Assembly Cache](../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
 [Gacutil.exe (outil Global Assembly Cache)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)
