---
title: "Référence à l’assembly &#39; requise &lt;assemblyname&gt;&#39; contenant la classe de base &#39;&lt; ClassName&gt;&#39;"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30007
- vbc30007
helpviewer_keywords: BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: f7413c82a9c61d13e7ca6fa18f27a4769a0937f0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="reference-required-to-assembly-39ltassemblynamegt39-containing-the-base-class-39ltclassnamegt39"></a>Référence à l’assembly &#39; requise &lt;assemblyname&gt;&#39; contenant la classe de base &#39;&lt; ClassName&gt;&#39;
Référence à l’assembly requise '\<nom_assembly >' contenant la classe de base\<nom_classe >'. Ajoutez-en une à votre projet.  
  
 La classe est définie dans une bibliothèque de liens dynamiques (DLL) ou un assembly qui n’est pas directement référencé dans votre projet. Le compilateur [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] nécessite une référence pour éviter toute ambiguïté au cas où la classe serait définie dans plusieurs DLL ou assemblys.  
  
 **ID d’erreur :** BC30007  
  
## <a name="to-correct-this-error"></a>Pour corriger cette erreur  
  
-   Incluez le nom de la DLL ou de l’assembly non référencé dans vos références de projet.  
  
## <a name="see-also"></a>Voir aussi  
 [NIB Comment : ajouter ou supprimer des références à l’aide de la boîte de dialogue Ajouter une référence](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)  
 [Gestion des références dans un projet](/visualstudio/ide/managing-references-in-a-project)  
 [Dépannage de références rompues](/visualstudio/ide/troubleshooting-broken-references)
