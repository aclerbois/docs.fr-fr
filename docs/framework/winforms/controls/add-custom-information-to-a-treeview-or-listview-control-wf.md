---
title: "Comment : ajouter des informations personnalisées à un contrôle TreeView ou ListView (Windows Forms)"
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
- cpp
f1_keywords: ListItem
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- examples [Windows Forms], ListView control
- ListView control [Windows Forms], adding custom information
- TreeView control [Windows Forms], adding custom information
ms.assetid: 68be11de-1d5b-430e-901f-cfbe48d14b19
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 0e7086e52992f575781449e5dc2a83c3443f558d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-add-custom-information-to-a-treeview-or-listview-control-windows-forms"></a>Comment : ajouter des informations personnalisées à un contrôle TreeView ou ListView (Windows Forms)
Vous pouvez créer un nœud dérivé dans un Windows Forms <xref:System.Windows.Forms.TreeView> contrôle ou un élément dérivé dans un <xref:System.Windows.Forms.ListView> contrôle. La dérivation vous permet d’ajouter les champs dont vous avez besoin, ainsi que des méthodes et des constructeurs personnalisés pour traiter les champs. Une utilisation de cette fonctionnalité consiste à attacher un objet Customer à chaque élément de liste ou nœud de l’arborescence. Ces exemples sont pour un <xref:System.Windows.Forms.TreeView> contrôle, mais la même approche peut être utilisé pour un <xref:System.Windows.Forms.ListView> contrôle.  
  
### <a name="to-derive-a-tree-node"></a>Pour dériver un nœud d’arborescence  
  
-   Créer une nouvelle classe de nœud, dérivée de la <xref:System.Windows.Forms.TreeNode> (classe), qui comporte un champ personnalisé pour enregistrer un chemin d’accès de fichier.  
  
    ```vb  
    Class myTreeNode  
       Inherits TreeNode  
  
       Public FilePath As String  
  
       Sub New(ByVal fp As String)  
          MyBase.New()  
          FilePath = fp  
          Me.Text = fp.Substring(fp.LastIndexOf("\"))  
       End Sub  
    End Class  
    ```  
  
    ```csharp  
    class myTreeNode : TreeNode  
    {  
       public string FilePath;  
  
       public myTreeNode(string fp)  
       {  
          FilePath = fp;  
          this.Text = fp.Substring(fp.LastIndexOf("\\"));  
       }  
    }  
    ```  
  
    ```cpp  
    ref class myTreeNode : public TreeNode  
    {  
    public:  
       System::String ^ FilePath;  
  
       myTreeNode(System::String ^ fp)  
       {  
          FilePath = fp;  
          this->Text = fp->Substring(fp->LastIndexOf("\\"));  
       }  
    };  
    ```  
  
### <a name="to-use-a-derived-tree-node"></a>Pour utiliser un nœud d’arborescence dérivé  
  
1.  Vous pouvez utiliser le nouveau nœud d’arborescence dérivé en tant que paramètre pour les appels de fonction.  
  
     Dans l’exemple ci-dessous, le chemin d’accès défini pour l’emplacement du fichier texte est le dossier Mes documents. En effet, vous pouvez supposer que la plupart des ordinateurs exécutant le système d’exploitation Windows incluent ce répertoire. Cela permet également aux utilisateurs avec des niveaux d’accès minimum au système d’exécuter l’application en toute sécurité.  
  
    ```vb  
    ' You should replace the bold text file   
    ' in the sample below with a text file of your own choosing.  
    TreeView1.Nodes.Add(New myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\ TextFile.txt ") )  
    ```  
  
    ```csharp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    treeView1.Nodes.Add(new myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\TextFile.txt") );  
    ```  
  
    ```cpp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    treeView1->Nodes->Add(new myTreeNode(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\TextFile.txt")));  
    ```  
  
2.  Si vous sont passés au nœud d’arbre et elle est tapée comme une <xref:System.Windows.Forms.TreeNode> de classe, vous devez effectuer un cast vers votre classe dérivée. Le cast est une conversion explicite d’un type d’objet vers un autre. Pour plus d’informations sur le cast, consultez [Conversions implicites et explicites](~/docs/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) ([!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]), [() Opérateur](~/docs/csharp/language-reference/operators/invocation-operator.md) ([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]) ou [Opérateur de cast : ()](/cpp/cpp/cast-operator-parens) ([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]).  
  
    ```vb  
    Public Sub TreeView1_AfterSelect(ByVal sender As Object, ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       Dim mynode As myTreeNode  
       mynode = CType(e.node, myTreeNode)  
       MessageBox.Show("Node selected is " & mynode.filepath)  
    End Sub  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,  
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       myTreeNode myNode = (myTreeNode)e.Node;  
       MessageBox.Show("Node selected is " + myNode.FilePath);  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          myTreeNode ^ myNode = safe_cast<myTreeNode^>(e->Node);  
          MessageBox::Show(String::Concat("Node selected is ",   
             myNode->FilePath));  
       }  
    ```  
  
## <a name="see-also"></a>Voir aussi  
 [TreeView, contrôle](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)  
 [Contrôle ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)
