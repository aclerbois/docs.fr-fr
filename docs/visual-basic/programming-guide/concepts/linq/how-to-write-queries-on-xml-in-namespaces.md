---
title: "Comment : écrire des requêtes sur du code XML dans les espaces de noms (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d4131b5-3288-414f-b77c-b2edc2a1f465
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 5708a2a162132262722f390842f59c9c6a6838e4
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-write-queries-on-xml-in-namespaces-visual-basic"></a>Comment : écrire des requêtes sur du code XML dans les espaces de noms (Visual Basic)
Pour écrire des requêtes sur du code XML qui est dans un espace de noms, vous devez utiliser des objets <xref:System.Xml.Linq.XName> qui ont l'espace de noms correct.  
  
 Dans Visual Basic, l'approche la plus courante consiste à définir un espace de noms global, puis à utiliser des littéraux XML et des propriétés XML qui emploient l'espace de noms global. Vous pouvez définir un espace de noms par défaut global, auquel cas les éléments dans les littéraux XML seront par défaut dans l'espace de noms. En guise d'alternative, vous pouvez définir un espace de noms global avec un préfixe, puis utiliser le préfixe selon les besoins dans les littéraux XML et les propriétés XML. Comme avec d'autres formes de code XML, les attributs ne sont jamais dans aucun espace de noms par défaut.  
  
 Le premier ensemble d’exemples de cette rubrique montre comment créer une arborescence XML dans un espace de noms par défaut. Le second ensemble illustre la création d’une arborescence XML dans un espace de noms avec un préfixe.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant crée une arborescence XML qui est dans un espace de noms par défaut. Il récupère ensuite une collection d'éléments.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>1</Child>  
                <Child>2</Child>  
                <Child>3</Child>  
                <AnotherChild>4</AnotherChild>  
                <AnotherChild>5</AnotherChild>  
                <AnotherChild>6</AnotherChild>  
            </Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(el.Value)  
        Next  
    End Sub  
End Module  
```  
  
 Cet exemple génère la sortie suivante :  
  
```  
1  
2  
3  
```  
  
## <a name="example"></a>Exemple  
 En Visual Basic, toutefois, l’écriture de requêtes sur sur arborescence XML qui utilise un espace de noms avec un préfixe diffère de l’écriture sur une arborescence XML dans un espace de noms par défaut. En général, vous devez utiliser l'instruction `Imports` pour importer l'espace de noms avec un préfixe. Vous utilisez ensuite le préfixe dans les noms d'éléments et d'attributs, lors de la construction de l'arborescence XML. Vous utilisez également le préfixe lors de l'interrogation d'une arborescence XML avec des propriétés XML.  
  
 L'exemple suivant crée une arborescence XML qui est dans un espace de noms avec un préfixe. Il récupère ensuite une collection d'éléments.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>1</aw:Child>  
                <aw:Child>2</aw:Child>  
                <aw:Child>3</aw:Child>  
                <aw:AnotherChild>4</aw:AnotherChild>  
                <aw:AnotherChild>5</aw:AnotherChild>  
                <aw:AnotherChild>6</aw:AnotherChild>  
            </aw:Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<aw:Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(CInt(el))  
        Next  
    End Sub  
End Module  
```  
  
 Cet exemple génère la sortie suivante :  
  
```  
1  
2  
3  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Utilisation des espaces de noms XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
