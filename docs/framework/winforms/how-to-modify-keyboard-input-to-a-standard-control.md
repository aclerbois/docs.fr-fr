---
title: "Comment : modifier l'entrée au clavier pour un contrôle standard"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keyboard input [Windows Forms], modifying
- modifying keyboard input
- Windows Forms, modifying keyboard input
- keyboards [Windows Forms], keyboard input
ms.assetid: 626d3712-d866-4988-bcda-a2d5b36ec0ba
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 2c95ba3ef1c590f5c7e5d5e89ed05cf28c7829d4
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-modify-keyboard-input-to-a-standard-control"></a>Comment : modifier l'entrée au clavier pour un contrôle standard
Windows Forms offre la possibilité de consommer et de modifier l'entrée au clavier. Consommer une touche signifie gérer une touche dans une méthode ou un gestionnaire d'événements pour que d'autres méthodes et événements plus loin dans la file d'attente de messages ne reçoivent pas la valeur de la touche. Modifier une touche signifie modifier sa valeur pour que les méthodes et les gestionnaires d'événements plus loin dans la file d'attente de messages reçoivent une valeur de touche différente. Cette rubrique montre comment accomplir ces tâches.  
  
### <a name="to-consume-a-key"></a>Pour consommer une touche  
  
-   Dans un gestionnaire d'événements <xref:System.Windows.Forms.Control.KeyPress>, affectez la valeur `true` à la propriété <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> de la classe <xref:System.Windows.Forms.KeyPressEventArgs>.  
  
     ou  
  
     Dans un gestionnaire d'événements <xref:System.Windows.Forms.Control.KeyDown>, affectez la valeur `true` à la propriété <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> de la classe <xref:System.Windows.Forms.KeyEventArgs>.  
  
    > [!NOTE]
    >  La définition de la propriété <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> dans le gestionnaire d'événements <xref:System.Windows.Forms.Control.KeyDown> n'empêche pas les événements <xref:System.Windows.Forms.Control.KeyPress> et <xref:System.Windows.Forms.Control.KeyUp> d'être déclenchés pour la séquence de touches actuelle. Vous devez pour cela utiliser la propriété <xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A>.  
  
     L'exemple suivant est un extrait d'instruction `switch` qui examine la propriété <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> du <xref:System.Windows.Forms.KeyPressEventArgs> reçu par un gestionnaire d'événements <xref:System.Windows.Forms.Control.KeyPress>. Ce code consomme les touches de caractère « A » et « a ».  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#6)]  
  
### <a name="to-modify-a-standard-character-key"></a>Pour modifier une touche de caractère standard  
  
-   Dans un gestionnaire d'événements <xref:System.Windows.Forms.Control.KeyPress>, affectez à la propriété <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> de la classe <xref:System.Windows.Forms.KeyPressEventArgs> la valeur de la nouvelle touche de caractère.  
  
     L'exemple suivant est un extrait d'instruction `switch` qui remplace « B » par « A » et « b » par « a ». Notez que la propriété <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> du paramètre <xref:System.Windows.Forms.KeyPressEventArgs> a la valeur `false`, pour que la nouvelle valeur de touche soit propagée aux autres méthodes et événements dans la file d'attente de messages.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#7)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#7)]  
  
### <a name="to-modify-a-noncharacter-key"></a>Pour modifier une touche non-caractère  
  
-   Substituez une méthode <xref:System.Windows.Forms.Control> qui traite les messages Windows, détectez le message WM_KEYDOWN ou WM_SYSKEYDOWN et affectez à la propriété <xref:System.Windows.Forms.Message.WParam%2A> du paramètre <xref:System.Windows.Forms.Message> la valeur <xref:System.Windows.Forms.Keys> qui représente la nouvelle touche non-caractère.  
  
     L'exemple de code suivant montre comment substituer la méthode <xref:System.Windows.Forms.Control.PreProcessMessage%2A> d'un contrôle pour détecter les touches F1 à F9 et modifier toute activation de la touche F3 en F1. Pour plus d’informations sur <xref:System.Windows.Forms.Control> les méthodes que vous pouvez substituer pour intercepter des messages de clavier, consultez [entrée d’utilisateur dans une Application Windows Forms](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md) et [fonctionnement des entrées au clavier](../../../docs/framework/winforms/how-keyboard-input-works.md).  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#12)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#12)]  
  
## <a name="example"></a>Exemple  
 L'exemple de code suivant est l'application complète pour les exemples de code des sections précédentes. L'application utilise un contrôle personnalisé dérivé de la classe <xref:System.Windows.Forms.TextBox> pour consommer et modifier l'entrée au clavier.  
  
 [!code-csharp[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Cet exemple nécessite :  
  
-   des références aux assemblys System, System.Drawing et System.Windows.Forms.  
  
 Pour plus d’informations sur la création de cet exemple à partir de la ligne de commande pour [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], consultez [Génération à partir de la ligne de commande](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) ou [Génération à partir de la ligne de commande avec csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Vous pouvez également générer cet exemple dans [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] en collant le code dans un nouveau projet.  Consultez également [Guide pratique pour compiler et exécuter un exemple complet de code Windows Forms à l’aide de Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="see-also"></a>Voir aussi  
 [Entrée au clavier dans une application Windows Forms](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)  
 [Entrée d’utilisateur dans une application Windows Forms](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md)  
 [Fonctionnement de l’entrée au clavier](../../../docs/framework/winforms/how-keyboard-input-works.md)
