---
title: "Un tableau déclaré en tant que variable de contrôle de boucle for ne peut pas être déclaré avec une taille initiale"
ms.date: 07/20/2015
ms.prod: .net
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc32039
- bc32039
helpviewer_keywords: BC32039
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 0635e1b18b24a241fabad6d67da34f8dde9530db
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="array-declared-as-for-loop-control-variable-cannot-be-declared-with-an-initial-size"></a>Un tableau déclaré en tant que variable de contrôle de boucle for ne peut pas être déclaré avec une taille initiale
A `For Each` boucle utilise un tableau comme sa *élément* variable d’itération initialise mais ce tableau.  
  
 Les instructions suivantes montrent comment cette erreur peut être générée.  
  
```  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 La première `For Each` instruction est la méthode correcte pour accéder aux éléments de `arrayList`. La seconde `For Each` instruction génère cette erreur.  
  
 **ID d’erreur :** BC32039  
  
## <a name="to-correct-this-error"></a>Pour corriger cette erreur  
  
-   Supprimez l’initialisation de la déclaration de la *élément* variable d’itération.  
  
## <a name="see-also"></a>Voir aussi  
 [For...Next (instruction)](../../../visual-basic/language-reference/statements/for-next-statement.md)  
 [Tableaux](../../../visual-basic/programming-guide/language-features/arrays/index.md)  
 [Collections](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)
