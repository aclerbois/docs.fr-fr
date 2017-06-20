---
title: "Filtrage avec DataView (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5632d74a-ff53-4ea7-9fe7-4a148eeb1c68
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Filtrage avec DataView (LINQ to DataSet)
La possibilité de filtrer des données en utilisant des critères spécifiques, puis de les présenter à un client à travers un contrôle d'interface utilisateur, est un important aspect de la liaison de données.  <xref:System.Data.DataView> propose plusieurs manières de filtrer les données et de retourner des sous\-ensembles de lignes de données correspondant à des critères de filtre spécifiques.  Outre les capacités de filtrage basé sur chaîne, <xref:System.Data.DataView> donne également la possibilité d'utiliser des expressions [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] pour les critères de filtrage. Les expressions [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] permettent des opérations de filtrage bien plus complexes et puissantes que le filtrage basé sur chaîne.  
  
 Il existe deux façons de filtrer des données à l'aide d'un <xref:System.Data.DataView> :  
  
-   Créer un <xref:System.Data.DataView> à partir d'une requête [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] comprenant une clause Where.  
  
-   Utiliser les fonctionnalités de filtrage basé sur chaîne existantes de <xref:System.Data.DataView>.  
  
## Création d'un DataView à partir d'une requête avec informations de filtrage  
 Un objet <xref:System.Data.DataView> peut être créé à partir d'une requête [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Si cette requête contient une clause `Where`, le <xref:System.Data.DataView> est créé avec les informations de filtrage de la requête.  L'expression dans la clause `Where` sert à déterminer quelles lignes de données seront incluses dans le <xref:System.Data.DataView>, et est la base du filtre.  
  
 Les filtres basés sur une expression offrent une filtrage plus puissant et plus complexe que les filtres basés sur chaîne.  Les filtres basés sur chaîne et sur une expression s'excluent mutuellement.  Lorsque le <xref:System.Data.DataView.RowFilter%2A> basé sur chaîne est défini après la création d'un <xref:System.Data.DataView> à partir d'une requête, le filtre basé sur une expression déduit de la requête est supprimé.  
  
> [!NOTE]
>  Dans la plupart des cas, les expressions utilisées pour le filtrage ne doivent pas avoir d'effets secondaires et doivent être déterministes.  De plus, les expressions ne doivent pas contenir de logique dépendant d'un nombre défini d'exécutions, parce que les opérations de filtrage doivent pouvoir être exécutées de façon illimitée.  
  
### Exemple  
 L'exemple suivant interroge la table SalesOrderDetail pour extraire les commandes de quantité supérieure à 2 et inférieure à 6 ; crée un <xref:System.Data.DataView> à partir de cette requête, et lie le <xref:System.Data.DataView> à une <xref:System.Windows.Forms.BindingSource> :  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere)]  
  
### Exemple  
 L'exemple suivant crée un <xref:System.Data.DataView> à partir d'une requête correspondant aux commandes passées après le 6 juin 2001 :  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere3)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere3)]  
  
### Exemple  
 Le filtrage peut également être combiné avec le tri.  L'exemple suivant crée un <xref:System.Data.DataView> à partir d'une requête pour les contacts dont le nom commence par la lettre « S » et trié par nom, puis par prénom :  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhereorderbythenby)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhereorderbythenby)]  
  
### Exemple  
 L'exemple suivant utilise l'algorithme SoundEx pour rechercher des contacts dont le nom est semblable à « Zhu ».  L'algorithme SoundEx est implémenté dans la méthode SoundEx.  
  
 [!code-csharp[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvsoundexfilter)]
 [!code-vb[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvsoundexfilter)]  
  
 SoundEx est un algorithme phonétique qui sert à indexer les noms par son, tels qu'ils sont prononcés en anglais, qui a été développé à l'origine par le Bureau  de recensement des États\-Unis.  La méthode SoundEx retourne un code à quatre caractères pour un nom comprenant une lettre alphabétique suivie de trois chiffres.  La lettre est la première du nom et les chiffres encodent les consonnes restantes du nom.  Les noms de consonance similaire ont le même code SoundEx.  L'implémentation SoundEx utilisée dans la méthode SoundEx de l'exemple précédent est illustrée ici :  
  
 [!code-csharp[DP DataView Samples#SoundEx](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#soundex)]
 [!code-vb[DP DataView Samples#SoundEx](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#soundex)]  
  
## Utilisation de la propriété RowFilter  
 La fonctionnalité de filtrage basé sur chaîne existante de <xref:System.Data.DataView> fonctionne toujours dans le contexte de [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].   Pour plus d'informations sur le filtrage <xref:System.Data.DataView.RowFilter%2A> basé sur chaîne, voir [Tri et filtrage de données](../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md).  
  
 L'exemple suivant crée une table <xref:System.Data.DataView> à partir de la table Contact, puis définit la propriété <xref:System.Data.DataView.RowFilter%2A> pour retourner les lignes où le nom du contact est « Zhu » :  
  
 [!code-csharp[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvrowfilter)]
 [!code-vb[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvrowfilter)]  
  
 Une fois qu'un <xref:System.Data.DataView> a été créé à partir d'une requête <xref:System.Data.DataTable> or [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], vous pouvez utiliser la propriété <xref:System.Data.DataView.RowFilter%2A> pour spécifier des sous\-ensembles de lignes basés sur leurs valeurs de colonne.  Les filtres basés sur chaîne et sur une expression s'excluent mutuellement.  La définition de la propriété <xref:System.Data.DataView.RowFilter%2A> efface l'expression de filtre déduite de la requête [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], et l'expression de filtre ne peut pas être réinitialisée.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywheresetrowfilter)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywheresetrowfilter)]  
  
 Si vous souhaitez retourner les résultats d'une requête particulière exécutée sur les données, vous pouvez, au lieu de fournir une vue dynamique d'un sous\-ensemble des données, utiliser l'une des méthodes <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> du <xref:System.Data.DataView>, plutôt que de définir la propriété <xref:System.Data.DataView.RowFilter%2A>.  L'utilisation de la propriété <xref:System.Data.DataView.RowFilter%2A> est optimale dans une application de liaison de données où un contrôle lié affiche des résultats filtrés.  Le paramétrage de la propriété <xref:System.Data.DataView.RowFilter%2A> entraîne une nouvelle génération de l'index des données, ce qui accroît la charge sur votre application et, par voie de conséquence, fait baisser les performances.  Les méthodes <xref:System.Data.DataView.Find%2A> et <xref:System.Data.DataView.FindRows%2A> utilisent l'index en cours sans qu'il soit nécessaire de le reconstruire.  Si vous ne souhaitez appeler <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> qu'une seule fois, il est préférable d'utiliser le <xref:System.Data.DataView> existant.  Si vous souhaitez appeler <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> plusieurs fois, vous devez créer un nouveau <xref:System.Data.DataView> pour reconstruire l'index sur la colonne où vous voulez effectuer la recherche, pour appeler la méthode <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A>.  Pour plus d'informations sur les méthodes <xref:System.Data.DataView.Find%2A> et <xref:System.Data.DataView.FindRows%2A>, voir [Recherche de lignes](../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md) et [Performances des DataView](../../../../docs/framework/data/adonet/dataview-performance.md).  
  
## Suppression du filtre  
 Le filtre d'un <xref:System.Data.DataView> peut être supprimé une fois le filtrage défini à l'aide de la propriété <xref:System.Data.DataView.RowFilter%2A>.  Le filtre sur un <xref:System.Data.DataView> peut être supprimé de deux manières différentes :  
  
-   Affectez à la propriété <xref:System.Data.DataView.RowFilter%2A> la valeur `null`.  
  
-   Définissez la propriété <xref:System.Data.DataView.RowFilter%2A> en tant que chaîne vide.  
  
### Exemple  
 L'exemple suivant crée un <xref:System.Data.DataView> à partir d'une requête, puis supprime le filtre en définissant la propriété <xref:System.Data.DataView.RowFilter%2A> sur `null` :  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter2)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter2)]  
  
### Exemple  
 L'exemple suivant crée un <xref:System.Data.DataView> à partir d'une table, définit la propriété <xref:System.Data.DataView.RowFilter%2A>, puis supprime le filtre en définissant la propriété <xref:System.Data.DataView.RowFilter%2A> en tant que chaîne vide :  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter)]  
  
## Voir aussi  
 [Liaison de données et LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)   
 [Tri avec DataView](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)