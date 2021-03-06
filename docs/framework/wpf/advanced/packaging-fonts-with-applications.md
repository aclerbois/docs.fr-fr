---
title: Empaquetage de polices avec des applications
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], packaging fonts with
- fonts [WPF], packaging with applications
- typography [WPF], packaging fonts with applications
- packaging fonts with applications [WPF]
ms.assetid: db15ee48-4d24-49f5-8b9d-a64460865286
caps.latest.revision: "29"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: f60668f1bdac6607383b2ddf5c5ab1e41e31862b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="packaging-fonts-with-applications"></a>Empaquetage de polices avec des applications
Cette rubrique fournit une vue d’ensemble de la façon d’empaqueter des polices avec votre [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] application.  
  
> [!NOTE]
>  Comme avec la plupart des types de logiciels, les fichiers de police sont sous licence et ne sont pas vendus. Les licences qui régissent l’utilisation des polices varient d’un fournisseur à l’autre mais en général, la plupart des licences, y compris celles portant sur les polices [!INCLUDE[TLA#tla_ms#initcap](../../../../includes/tlasharptla-mssharpinitcap-md.md)] fournies avec des applications et [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)], n’autorisent pas les polices incorporées dans des applications ou dans le cas contraire redistribuée. Par conséquent, en tant que développeur, c’est à vous de vérifier que vous disposez des droits de licence nécessaires pour toute police incorporée dans une application ou redistribuée.  
  

  
<a name="introduction_to_packaging_fonts"></a>   
## <a name="introduction-to-packaging-fonts"></a>Présentation de l’empaquetage de polices  
 Vous pouvez empaqueter facilement des polices en tant que ressources dans votre [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applications pour afficher le texte de l’interface utilisateur et d’autres types de texte en fonction de contenu. Les polices peuvent être séparées des fichiers d’assembly de l’application ou y être incorporées. Vous pouvez également créer une bibliothèque de polices de ressources uniquement, que votre application peut référencer.  
  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]et [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] polices contiennent un indicateur de type (fsType) qui indique les droits d’incorporation de licence pour la police. Toutefois, cet indicateur de type concerne uniquement les polices incorporées stockées dans un document. Il ne concerne pas les polices incorporées dans une application. Vous pouvez récupérer la police de l’incorporation des droits pour une police en créant un <xref:System.Windows.Media.GlyphTypeface> objet et en référençant sa <xref:System.Windows.Media.GlyphTypeface.EmbeddingRights%2A> propriété. Reportez-vous à la section « mesures OS/2 et Windows » de la [spécification OpenType](http://www.microsoft.com/typography/otspec/os2.htm) pour plus d’informations sur l’indicateur fsType.  
  
 Le [Microsoft Typography](http://www.microsoft.com/typography/links/) site Web comporte des informations de contact qui peuvent vous aider à localiser un fournisseur de police particulière ou trouver un fournisseur de polices pour un.  
  
<a name="adding_fonts_as_content_items"></a>   
## <a name="adding-fonts-as-content-items"></a>Ajout de polices comme éléments de contenu  
 Vous pouvez ajouter des polices à votre application sous forme d’éléments de contenu de projet séparés des fichiers d’assembly de l’application. Cela signifie que les éléments de contenu ne sont pas incorporés sous forme de ressources dans un assembly. L’exemple de fichier projet suivant montre comment définir des éléments de contenu.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Content Include="Peric.ttf" />  
    <Content Include="Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
 Pour vérifier que l’application peut utiliser les polices au moment de l’exécution, ces dernières doivent être accessibles dans le répertoire de déploiement de l’application. Le `<CopyToOutputDirectory>` élément dans le fichier de projet de l’application vous permet de copier automatiquement les polices dans le répertoire de déploiement d’application pendant le processus de génération. L’exemple de fichier projet suivant montre comment copier les polices dans le répertoire de déploiement.  
  
```xml  
<ItemGroup>  
  <Content Include="Peric.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
  <Content Include="Pericl.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
</ItemGroup>  
```  
  
 L’exemple de code suivant montre comment référencer la police de l’application comme élément de contenu. L’élément de contenu référencé doit être dans le même répertoire que les fichiers d’assembly de l’application.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet8)]  
  
<a name="adding_fonts_as_resource_items"></a>   
## <a name="adding-fonts-as-resource-items"></a>Ajout de polices comme éléments de ressource  
 Vous pouvez ajouter des polices à votre application sous forme d’éléments de ressource de projet incorporés dans les fichiers d’assembly de l’application. L’utilisation d’un sous-répertoire distinct pour les ressources permet d’organiser les fichiers projet de l’application. L’exemple de fichier projet suivant montre comment définir des polices comme éléments de ressource dans un sous-répertoire distinct.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Resource Include="resources\Peric.ttf" />  
    <Resource Include="resources\Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
> [!NOTE]
>  Lorsque vous ajoutez des polices en tant que ressources dans votre application, assurez-vous que vous définissez la `<Resource>` élément et non le `<EmbeddedResource>` élément dans le fichier projet de votre application. Le `<EmbeddedResource>` , élément pour l’action de génération n’est pas pris en charge.  
  
 L’exemple de balisage suivant indique comment référencer les ressources de police de l’application.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet1)]  
  
### <a name="referencing-font-resource-items-from-code"></a>Référencement d’éléments de ressource de police à partir du code  
 Pour référencer les éléments de ressource de police à partir du code, vous devez fournir une référence de ressource de police en deux parties : la base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]; et la référence d’emplacement de police. Ces valeurs sont utilisées comme paramètres pour la <xref:System.Windows.Media.FontFamily.%23ctor%2A> (méthode). L’exemple de code suivant indique comment référencer les ressources de police de l’application dans le sous-répertoire de projet appelé `resources`.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet2)]
 [!code-vb[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet2)]  
  
 La base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] peut inclure le sous-répertoire d’application où se trouve la ressource de police. Dans ce cas, la référence d’emplacement de police n’a pas besoin de spécifier un répertoire, mais devrait inclure un préfixe «`./`», ce qui indique la ressource de police est dans le même répertoire que celui spécifié par la base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]. L’exemple de code suivant montre une autre façon de référencer l’élément de ressource de police. Il est équivalent à l’exemple de code précédent.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet5)]
 [!code-vb[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet5)]  
  
### <a name="referencing-fonts-from-the-same-application-subdirectory"></a>Référencement de polices à partir du même sous-répertoire d’application  
 Vous pouvez placer le contenu de l’application et les fichiers de ressources dans le même sous-répertoire défini par l’utilisateur de votre projet d’application. L’exemple de fichier projet suivant montre une page de contenu et des ressources de police définies dans le même sous-répertoire.  
  
```xml  
<ItemGroup>  
  <Page Include="pages\HomePage.xaml" />  
</ItemGroup>  
<ItemGroup>  
  <Resource Include="pages\Peric.ttf" />  
  <Resource Include="pages\Pericl.ttf" />  
</ItemGroup>  
```  
  
 Comme le contenu de l’application et la police sont dans le même sous-répertoire, la référence de police est relative au contenu d’application. Les exemples suivants montrent comment référencer les ressources de police de l’application quand la police se trouve dans le même répertoire que l’application.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml#fontpackagesnippet3)]  
  
 [!code-csharp[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml.cs#fontpackagesnippet4)]
 [!code-vb[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/pages/homepage.xaml.vb#fontpackagesnippet4)]  
  
### <a name="enumerating-fonts-in-an-application"></a>Énumération des polices dans une application  
 Pour énumérer des polices en tant qu’éléments de ressource dans votre application, utilisez le <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> ou <xref:System.Windows.Media.Fonts.GetTypefaces%2A> (méthode). L’exemple suivant montre comment utiliser le <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> méthode pour retourner la collection de <xref:System.Windows.Media.FontFamily> objets à partir de l’emplacement de police d’application. Dans cet exemple, l’application contient un sous-répertoire nommé « Resources ».  
  
 [!code-csharp[FontSnippets#FontsSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet3)]
 [!code-vb[FontSnippets#FontsSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet3)]  
  
 L’exemple suivant montre comment utiliser le <xref:System.Windows.Media.Fonts.GetTypefaces%2A> méthode pour retourner la collection de <xref:System.Windows.Media.Typeface> objets à partir de l’emplacement de police d’application. Dans cet exemple, l’application contient un sous-répertoire nommé « Resources ».  
  
 [!code-csharp[FontSnippets#FontsSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet7)]
 [!code-vb[FontSnippets#FontsSnippet7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet7)]  
  
<a name="creating_a_font_resource_library"></a>   
## <a name="creating-a-font-resource-library"></a>Création d’une bibliothèque de ressources de police  
 Vous pouvez créer une bibliothèque de ressources uniquement qui contient seulement des polices, aucun code ne fait partie de ce type de projet de bibliothèque. La création d’une bibliothèque de ressources uniquement est une technique courante pour découpler les ressources du code d’application qui les utilise. Cela permet également d’inclure l’assembly de bibliothèque dans plusieurs projets d’application. L’exemple de fichier projet suivant montre les parties clés d’un projet de bibliothèque de ressources uniquement.  
  
```xml  
<PropertyGroup>  
  <AssemblyName>FontLibrary</AssemblyName>  
  <OutputType>library</OutputType>  
  ...  
</PropertyGroup>  
...  
<ItemGroup>  
  <Resource Include="Kooten.ttf" />  
  <Resource Include="Pesca.ttf" />  
</ItemGroup  
```  
  
### <a name="referencing-a-font-in-a-resource-library"></a>Référencement d’une police dans une bibliothèque de ressources  
 Pour référencer une police dans une bibliothèque de ressources à partir de votre application, vous devez faire précéder la référence de police du nom de l’assembly de bibliothèque. Dans cet exemple, l’assembly de ressource de police est « FontLibrary ». Pour séparer le nom de l’assembly de la référence dans l’assembly, utilisez un caractère « ; ». L’ajout du mot clé « Component » suivi de la référence au nom de la police complète la référence aux ressources de la bibliothèque de polices. L’exemple de code suivant indique comment référencer une police dans un assembly de bibliothèque de ressources.  
  
 [!code-xaml[OpenTypeFontsSample#OpenTypeFontsSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontsSample/CS/Kootenay.xaml#opentypefontssample1)]  
  
> [!NOTE]
>  Ce kit de développement logiciel contient un jeu d’exemples [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] les polices que vous pouvez utiliser avec [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applications. Les polices sont définies dans une bibliothèque de ressources uniquement. Pour plus d’informations, consultez [Exemple de pack de polices OpenType](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md).  
  
<a name="limitations_on_font_usage"></a>   
## <a name="limitations-on-font-usage"></a>Limitations de l’utilisation des polices  
 La liste suivante décrit plusieurs restrictions sur l’empaquetage et l’utilisation de polices dans [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applications :  
  
-   **Bits d’autorisation d’incorporation de police :** Les applications [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ne vérifient ni n’appliquent les bits d’autorisation d’incorporation de police. Consultez le [Introduction à l’empaquetage polices](#introduction_to_packaging_fonts) section pour plus d’informations.  
  
-   **Site de polices d’origine :** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applications n’autorisent pas une référence de police pour http ou ftp [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)].  
  
-   **URI absolu à l’aide du pack : notation :** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applications n’autorisent pas vous permet de créer un <xref:System.Windows.Media.FontFamily> par programmation à l’aide de l’objet « pack : » dans le cadre d’absolu [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] référence à une police. Par exemple, `"pack://application:,,,/resources/#Pericles Light"` est une référence de police non valide.  
  
-   **Incorporation de police automatique :** Au moment de la conception, il n’est pas possible de rechercher les polices utilisées par une application et de les incorporer automatiquement dans les ressources de l’application.  
  
-   **Sous-ensembles de polices :** Les applications [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ne prennent pas en charge la création de sous-ensembles de polices pour les documents non fixes.  
  
-   En cas de référence incorrecte, l’application utilise une police disponible à la place.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Documents.Typography>  
 <xref:System.Windows.Media.FontFamily>  
 [Typographie de Microsoft : Des liens, des actualités et des Contacts](http://www.microsoft.com/typography/links/)  
 [Spécification OpenType](http://www.microsoft.com/typography/otspec/)  
 [Fonctionnalités des polices OpenType](../../../../docs/framework/wpf/advanced/opentype-font-features.md)  
 [Exemple de pack de polices OpenType](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)
