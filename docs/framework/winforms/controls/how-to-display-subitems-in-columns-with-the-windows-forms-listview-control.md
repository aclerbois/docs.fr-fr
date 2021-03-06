---
title: "Comment : afficher des sous-éléments en colonnes avec le contrôle ListView Windows Forms"
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
- list items
- Details view
- ListView control [Windows Forms], adding ListSubItems
- subitems
ms.assetid: e465f044-cde7-4fd9-a687-788a73a0f554
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: be1b055c8ea0e7a7c6466033735431a17ecc32f6
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-display-subitems-in-columns-with-the-windows-forms-listview-control"></a>Comment : afficher des sous-éléments en colonnes avec le contrôle ListView Windows Forms
Windows Forms <xref:System.Windows.Forms.ListView> contrôle peut afficher un texte supplémentaire ou des sous-éléments pour chaque élément dans la vue Détails. La première colonne affiche le texte de l’élément, par exemple un numéro d’employé. Le deuxième, troisième et les colonnes suivantes affichent le premier, deuxième, et les sous-éléments suivants.  
  
### <a name="to-add-subitems-to-a-list-item"></a>Pour ajouter des sous-éléments à un élément de liste  
  
1.  Ajouter des colonnes si nécessaires. Étant donné que la première colonne affiche l’élément <xref:System.Windows.Forms.ListView.Text%2A> propriété, vous avez besoin d’une colonne de plus qu’il ne sont sous-éléments. Pour plus d’informations sur l’ajout de colonnes, consultez [Comment : ajouter des colonnes au contrôle ListView Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md).  
  
2.  Appelez le <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection.Add%2A> méthode de la collection retournée par la <xref:System.Windows.Forms.ListViewItem.SubItems%2A> propriété d’un élément. L’exemple de code suivant définit le nom de l’employé et le service pour un élément de liste.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#61)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#61)]  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble du contrôle ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)  
 [Guide pratique pour ajouter et supprimer des éléments avec le contrôle ListView Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)  
 [Guide pratique pour ajouter des colonnes au contrôle ListView Windows Forms](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)  
 [Guide pratique pour afficher des icônes pour le contrôle ListView Windows Forms](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)  
 [Guide pratique pour ajouter des informations personnalisées à un contrôle TreeView ou ListView (Windows Forms)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)
