---
title: "Création d’écouteurs de journalisation personnalisés (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- custom log listeners
- My.Application.Log object, custom log listeners
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: b1bda4a3465af4ed95de720117ea2e03f9a86b84
ms.sourcegitcommit: 685143b62385500f59bc36274b8adb191f573a16
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2017
---
# <a name="walkthrough-creating-custom-log-listeners-visual-basic"></a>Procédure pas à pas : création d'écouteurs de journalisation personnalisés (Visual Basic)
Cette procédure pas à pas illustre comment créer un écouteur de journalisation personnalisé et le configurer pour écouter la sortie de l’objet `My.Application.Log`.  
  
## <a name="getting-started"></a>Prise en main  
 Les écouteurs de journalisation doivent hériter de la classe <xref:System.Diagnostics.TraceListener>.  
  
#### <a name="to-create-the-listener"></a>Pour créer l’écouteur  
  
-   Dans votre application, créez une classe nommée `SimpleListener` qui hérite de <xref:System.Diagnostics.TraceListener>.  
  
     [!code-vb[VbVbalrMyApplicationLog#16](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_1.vb)]  
  
     Les méthodes <xref:System.Diagnostics.TraceListener.Write%2A> et <xref:System.Diagnostics.TraceListener.WriteLine%2A>, requises par la classe de base, appellent `MsgBox` pour afficher leur entrée.  
  
     L’attribut <xref:System.Security.Permissions.HostProtectionAttribute> est appliqué aux méthodes <xref:System.Diagnostics.TraceListener.Write%2A> et <xref:System.Diagnostics.TraceListener.WriteLine%2A> afin que leurs attributs correspondent aux méthodes de classe de base. L’attribut <xref:System.Security.Permissions.HostProtectionAttribute> permet à l’hôte qui exécute le code de déterminer que ce dernier expose la synchronisation de la protection de l’hôte.  
  
    > [!NOTE]
    >  L’attribut <xref:System.Security.Permissions.HostProtectionAttribute> n’est effectif que sur les applications non managées, telles que SQL Server, qui hébergent le Common Language Runtime et implémentent la protection de l’hôte.  
  
 Pour vérifier que `My.Application.Log` utilise votre écouteur de journalisation, vous devez attribuer un nom fort à l’assembly qui le contient.  
  
 La procédure suivante fournit des étapes simples pour créer un assembly d’écouteur de journalisation portant un nom fort. Pour plus d’informations, consultez [Création et utilisation d’assemblys avec nom fort](../../../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md).  
  
#### <a name="to-strongly-name-the-log-listener-assembly"></a>Pour attribuer un nom fort à l’assembly de l’écouteur de journalisation  
  
1.  Sélectionnez un projet dans l' **Explorateur de solutions**. Dans le menu **Projet** , choisissez **Propriétés**. Pour plus d’informations, consultez [Introduction au Concepteur de projets](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Cliquez sur l’onglet **Signature**.  
  
3.  Sélectionnez la zone **Signer l’assembly**.  
  
4.  Sélectionnez **\<Nouveau** dans la liste déroulante **Choisir un fichier de clé de nom fort**.  
  
     La boîte de dialogue **Créer une clé de nom fort** s’ouvre.  
  
5.  Fournissez un nom pour le fichier de clé dans la zone **Nom du fichier de clé**.  
  
6.  Entrez un mot de passe dans les zones **Entrer le mot de passe** et **Confirmer le mot de passe**.  
  
7.  Cliquez sur **OK**.  
  
8.  Régénérez l’application.  
  
## <a name="adding-the-listener"></a>Ajout de l’écouteur  
 Maintenant que l’assembly a un nom fort, vous devez déterminer le nom fort de l’écouteur afin que `My.Application.Log` utilise votre écouteur de journalisation.  
  
 Le format d’un type portant un nom fort se présente comme suit.  
  
 \<nom type>, \<nom assembly>, \<numéro version>, \<culture>, \<nom fort>  
  
#### <a name="to-determine-the-strong-name-of-the-listener"></a>Pour déterminer le nom fort de l’écouteur  
  
-   Le code suivant indique comment déterminer le nom de type fort pour `SimpleListener`.  
  
     [!code-vb[VbVbalrMyApplicationLog#17](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_2.vb)]  
  
     Le nom fort du type dépend de votre projet.  
  
 Avec le nom fort, vous pouvez ajouter l’écouteur à la collection de l’écouteur de journalisation `My.Application.Log`.  
  
#### <a name="to-add-the-listener-to-myapplicationlog"></a>Pour ajouter l’écouteur à My.Application.Log  
  
1.  Cliquez avec le bouton droit sur app.config dans l’**Explorateur de solutions** et sélectionnez **Ouvrir**.  
  
     ou  
  
     S’il existe un fichier app.config :  
  
    1.  Dans le menu **Projet** , choisissez **Ajouter un nouvel élément**.  
  
    2.  Dans la boîte de dialogue **Ajouter un nouvel élément** , choisissez **Fichier de configuration de l’application**.  
  
    3.  Cliquez sur **Ajouter**.  
  
2.  Recherchez la section `<listeners>` dans la section `<source>` avec l’attribut `name` « DefaultSource », qui se trouve dans la section `<sources>` . La section `<sources>` se trouve dans la section `<system.diagnostics>` , dans la section `<configuration>` de plus haut niveau.  
  
3.  Ajoutez cet élément à la section `<listeners>` :  
  
    ```xml  
    <add name="SimpleLog" />  
    ```  
  
4.  Recherchez la section `<sharedListeners>` dans la section `<system.diagnostics>` , dans la section `<configuration>` de plus haut niveau.  
  
5.  Ajoutez cet élément à cette section `<sharedListeners>` :  
  
    ```xml  
    <add name="SimpleLog" type="SimpleLogStrongName" />  
    ```  
  
     Modifiez la valeur de `SimpleLogStrongName` pour qu’elle soit le nom fort de l’écouteur.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>  
 [Utilisation des journaux des applications](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)  
 [Guide pratique : enregistrer des exceptions](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)  
 [Guide pratique : écrire des messages de journal](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)  
 [Procédure pas à pas : modification de l’emplacement des informations My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
