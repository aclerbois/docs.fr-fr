---
title: "Acc&#232;s concurrentiel optimiste | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e380edac-da67-4276-80a5-b64decae4947
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Acc&#232;s concurrentiel optimiste
Dans un environnement multi\-utilisateur, il existe deux modèles pour la mise à jour de données dans une base de données : l'accès simultané optimiste et l'accès simultané pessimiste.  L'objet <xref:System.Data.DataSet> est conçu pour privilégier l'utilisation de l'accès simultané optimiste pour les activités longues, comme lors de la communication à distance de données ou de l'interaction avec ces dernières.  
  
 L'accès simultané pessimiste implique le verrouillage de lignes à la source de données pour empêcher que d'autres utilisateurs modifient des données d'une manière affectant l'utilisateur actuel.  Dans un modèle pessimiste, lorsqu'un utilisateur effectue une action entraînant l'application d'un verrou, les autres utilisateurs ne peuvent pas effectuer d'actions qui créeraient un conflit avec le verrou tant que le propriétaire de ce dernier ne l'a pas libéré.  Ce modèle est principalement utilisé dans les environnements où les conflits relatifs aux données sont fréquents, de sorte que le coût de la protection des données par verrous est inférieur à celui de la restauration des transactions en cas de conflits d'accès simultané.  
  
 Par conséquent, dans un modèle d'accès simultané pessimiste, un utilisateur qui met à jour une ligne crée un verrou.  Jusqu'à ce que cet utilisateur ait terminé sa mise à jour et libéré le verrou, personne d'autre ne peut modifier cette ligne.  C'est pourquoi il est préférable d'implémenter l'accès simultané pessimiste lorsque les temps de verrouillage sont courts, comme c'est le cas pour le traitement d'enregistrements par programme.  L'accès simultané pessimiste ne constitue pas la solution la plus adaptée lorsque des utilisateurs interagissent avec les données, ce qui entraîne le verrouillage d'enregistrements pendant des laps de temps relativement longs.  
  
> [!NOTE]
>  Si vous devez mettre à jour plusieurs lignes en une même opération, la création d'une transaction constitue une option plus adaptée que l'utilisation du verrouillage pessimiste.  
  
 Au contraire, les utilisateurs qui ont recours à un accès simultané optimiste ne verrouillent pas une ligne lorsqu'ils la lisent.  Lorsqu'un utilisateur souhaite mettre à jour une ligne, l'application doit déterminer si un autre utilisateur a modifié cette ligne depuis sa dernière lecture.  L'accès simultané optimiste est généralement utilisé dans les environnements où les conflits relatifs aux données sont rares.  L'accès simultané optimiste améliore les performances, dans la mesure où aucun verrouillage des enregistrements n'est requis et où le verrouillage d'enregistrements nécessite des ressources serveur supplémentaires.  Il faut également savoir que la gestion des verrous d'enregistrements requiert une connexion permanente au serveur de base de données.  Parce que ce n'est pas le cas dans un modèle d'accès simultané optimiste, les connexions au serveur sont disponibles pour traiter plus rapidement un nombre important de clients.  
  
 Dans un modèle d'accès simultané optimiste, une violation est réputée avoir eu lieu si, après réception par un utilisateur d'une valeur provenant de la base de données, un autre utilisateur modifie cette valeur avant que le premier n'ait tenté de le faire.  La manière dont le serveur résout une violation de l'accès simultané est bien illustrée par l'exemple suivant.  
  
 Les tableaux ci\-après suivent un exemple d'accès simultané optimiste.  
  
 À 13h00, l'utilisateur 1 lit une ligne de la base de données contenant les valeurs suivantes :  
  
 **CustID     LastName     FirstName**  
  
 101          Smith             Bob  
  
|Nom de la colonne|Valeur d'origine|Valeur actuelle|Valeur dans la base de données|  
|-----------------------|----------------------|---------------------|------------------------------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|Bob|Bob|  
  
 À 13h01, l'utilisateur 2 lit la même ligne.  
  
 À 13h03, l'utilisateur 2 modifie la valeur de **FirstName** pour remplacer « Bob » par « Robert » et met à jour la base de données.  
  
|Nom de la colonne|Valeur d'origine|Valeur actuelle|Valeur dans la base de données|  
|-----------------------|----------------------|---------------------|------------------------------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|Robert|Bob|  
  
 La mise à jour réussit car les valeurs de la base de données au moment de la mise à jour correspondent aux valeurs d'origine dont dispose l'utilisateur 2.  
  
 À 13h05, l'utilisateur 1 modifie la valeur de prénom pour remplacer « Bob » par « James » et tente de mettre à jour la base de données.  
  
|Nom de la colonne|Valeur d'origine|Valeur actuelle|Valeur dans la base de données|  
|-----------------------|----------------------|---------------------|------------------------------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|James|Robert|  
  
 À ce stade, l'utilisateur 1 est confronté à une violation d'accès simultané optimiste, car la valeur de la base de données \(« Robert »\) ne correspond plus à la valeur d'origine qu'attendait l'utilisateur 1 \(« Bob »\).  La violation d'accès concurrentiel vous indique simplement que la mise à jour a échoué.  Il convient maintenant de décider si les modifications apportées par l'utilisateur 2 devront être remplacées par celles de l'utilisateur 1 ou si ces dernières devront être annulées.  
  
## Recherche des violations d'accès simultané optimiste  
 Il existe plusieurs techniques qui permettent de déceler la présence d'une violation d'accès simultané optimiste.  L'une d'entre elles consiste à inclure une colonne horodateur dans la table.  Les bases de données proposent généralement une fonctionnalité d'horodatage qui peut être utilisée pour connaître la date et l'heure de la dernière mise à jour d'un enregistrement.  En utilisant cette technique, une colonne horodateur est incluse dans la définition de la table.  Chaque fois que l'enregistrement est mis à jour, l'horodatage est également mis à jour en fonction de la date et de l'heure actuelles.  Dans un test visant à déceler la présence de violations d'accès simultané optimiste, la colonne horodateur est retournée avec toute requête liée au contenu de la table.  Lors d'une tentative de mise à jour, la valeur d'horodatage figurant dans la base de données est comparée à la valeur d'origine contenue dans la ligne modifiée.  Si les valeurs correspondent, la modification est apportée et la colonne horodateur est mise à jour en fonction de la date et de l'heure actuelles afin de refléter la modification.  Si elles ne correspondent pas, une violation d'accès simultané optimiste s'est produite.  
  
 Une autre technique de recherche des violations d'accès simultané optimiste consiste à vérifier que toutes les valeurs de colonne d'origine d'une ligne correspondent toujours à celles qui figurent dans la base de données.  Examinons, par exemple, la requête suivante :  
  
```  
SELECT Col1, Col2, Col3 FROM Table1  
```  
  
 Pour savoir s'il y a eu violation d'accès simultané optimiste lors de la mise à jour d'une ligne de **Table1**, vous pouvez écrire l'instruction UPDATE suivante :  
  
```  
UPDATE Table1 Set Col1 = @NewCol1Value,  
              Set Col2 = @NewCol2Value,  
              Set Col3 = @NewCol3Value  
WHERE Col1 = @OldCol1Value AND  
      Col2 = @OldCol2Value AND  
      Col3 = @OldCol3Value  
```  
  
 Tant que les valeurs d'origine correspondent à celles qui figurent dans la base de données, la mise à jour est effectuée.  Si une valeur a été modifiée, la mise à jour ne modifiera pas la ligne car la clause WHERE ne trouvera pas de correspondance.  
  
 Notez qu'il est recommandé de toujours retourner une valeur de clé primaire unique dans votre requête.  Sinon, l'instruction UPDATE précédente risque de mettre à jour plusieurs lignes, ce qui n'est pas nécessairement dans vos intentions.  
  
 Si une colonne de votre source de données accepte les valeurs null, vous devrez peut\-être étendre votre clause WHERE pour vérifier s'il existe une référence null dans votre table locale et sa correspondance dans votre source de données.  Par exemple, l'instruction UPDATE suivante vérifie qu'une référence null dans la ligne locale correspond toujours à une référence null dans la source de données, ou si la valeur dans la ligne locale correspond toujours à celle de la source de données.  
  
```  
UPDATE Table1 Set Col1 = @NewVal1  
  WHERE (@OldVal1 IS NULL AND Col1 IS NULL) OR Col1 = @OldVal1  
```  
  
 Vous pouvez aussi choisir d'appliquer des critères moins restrictifs lorsque vous utilisez un modèle d'accès simultané optimiste.  Par exemple, utiliser uniquement les colonnes de clé primaire dans la clause WHERE aboutit au remplacement des données, que les autres colonnes aient ou non subi une mise à jour depuis la dernière requête.  Vous pouvez aussi appliquer une clause WHERE à certaines colonnes uniquement, ce qui aura pour effet de remplacer les données, sauf si des champs spécifiques ont été mis à jour depuis la dernière requête les concernant.  
  
### Événement DataAdapter.RowUpdated  
 L'événement **RowUpdated** de l'objet <xref:System.Data.Common.DataAdapter> peut être utilisé avec les techniques précédemment décrites, afin d'avertir votre application en cas de violation d'accès simultané optimiste.  **RowUpdated** intervient après chaque tentative de mise à jour d'une ligne **Modified** provenant d'un **DataSet**.  Cela vous permet d'ajouter un code de gestion spécial, qui traitera les exceptions le cas échéant, ajoutera des informations d'erreur personnalisées, ajoutera une logique pour les nouvelles tentatives, etc.  L'objet <xref:System.Data.Common.RowUpdatedEventArgs> retourne une propriété **RecordsAffected** contenant le nombre de lignes affectées par une commande de mise à jour donnée pour une ligne modifiée dans une table.  En configurant la commande de mise à jour de sorte qu'elle teste l'accès simultané optimiste, la propriété **RecordsAffected** retourne la valeur 0 si une violation d'accès simultané optimiste s'est produite, puisque aucun enregistrement n'a été mis à jour.  Dans ce cas, une exception est levée.  L'événement **RowUpdated** vous permet de gérer ce cas de figure et d'éviter l'exception en définissant une valeur **RowUpdatedEventArgs.Status** appropriée, telle que **UpdateStatus.SkipCurrentRow**.  Pour plus d'informations sur l'événement **RowUpdated**, voir [Gestion des événements DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md).  
  
 Vous pouvez éventuellement définir **DataAdapter.ContinueUpdateOnError** à **true**, avant d'appeler **Update**, et répondre aux informations d'erreur stockées dans la propriété **RowError** d'une ligne donnée lorsque **Update** est terminée.  Pour plus d'informations, consultez [Informations sur les erreurs de ligne](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-error-information.md).  
  
## Exemple d'accès simultané optimiste  
 L'exemple qui suit définit le **UpdateCommand** d'un **DataAdapter** pour tester l'accès simultané optimiste, puis utilise l'événement **RowUpdated** pour déceler la présence de violations d'accès simultané optimiste.  En cas de violation d'accès simultané optimiste, l'application définit le **RowError** de la ligne pour laquelle la mise à jour a été demandée afin de refléter une violation d'accès simultané optimiste.  
  
 Notez que les valeurs de paramètre passées à la clause WHERE de la commande UPDATE sont mappées aux valeurs **Original** de leur colonne.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers ORDER BY CustomerID", _  
  connection)  
  
' The Update command checks for optimistic concurrency violations  
' in the WHERE clause.  
adapter.UpdateCommand = New SqlCommand("UPDATE Customers " &  
  "(CustomerID, CompanyName) VALUES(@CustomerID, @CompanyName) " & _  
  "WHERE CustomerID = @oldCustomerID AND CompanyName = " &  
  "@oldCompanyName", connection)  
adapter.UpdateCommand.Parameters.Add( _  
  "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
adapter.UpdateCommand.Parameters.Add( _  
  "@CompanyName", SqlDbType.NVarChar, 30, "CompanyName")  
  
' Pass the original values to the WHERE clause parameters.  
Dim parameter As SqlParameter = dataSet.UpdateCommand.Parameters.Add( _  
  "@oldCustomerID", SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
parameter = adapter.UpdateCommand.Parameters.Add( _  
  "@oldCompanyName", SqlDbType.NVarChar, 30, "CompanyName")  
parameter.SourceVersion = DataRowVersion.Original  
  
' Add the RowUpdated event handler.  
AddHandler adapter.RowUpdated, New SqlRowUpdatedEventHandler( _  
  AddressOf OnRowUpdated)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Customers")  
  
' Modify the DataSet contents.  
adapter.Update(dataSet, "Customers")  
  
Dim dataRow As DataRow  
  
For Each dataRow In dataSet.Tables("Customers").Rows  
    If dataRow.HasErrors Then   
       Console.WriteLine(dataRow (0) & vbCrLf & dataRow.RowError)  
    End If  
Next  
  
Private Shared Sub OnRowUpdated( _  
  sender As object, args As SqlRowUpdatedEventArgs)  
   If args.RecordsAffected = 0  
      args.Row.RowError = "Optimistic Concurrency Violation!"  
      args.Status = UpdateStatus.SkipCurrentRow  
   End If  
End Sub  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers ORDER BY CustomerID",  
  connection);  
  
// The Update command checks for optimistic concurrency violations  
// in the WHERE clause.  
adapter.UpdateCommand = new SqlCommand("UPDATE Customers Set CustomerID = @CustomerID, CompanyName = @CompanyName " +  
   "WHERE CustomerID = @oldCustomerID AND CompanyName = @oldCompanyName, connection);  
adapter.UpdateCommand.Parameters.Add(  
  "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
adapter.UpdateCommand.Parameters.Add(  
  "@CompanyName", SqlDbType.NVarChar, 30, "CompanyName");  
  
// Pass the original values to the WHERE clause parameters.  
SqlParameter parameter = adapter.UpdateCommand.Parameters.Add(  
  "@oldCustomerID", SqlDbType.NChar, 5, "CustomerID");  
parameter.SourceVersion = DataRowVersion.Original;  
parameter = adapter.UpdateCommand.Parameters.Add(  
  "@oldCompanyName", SqlDbType.NVarChar, 30, "CompanyName");  
parameter.SourceVersion = DataRowVersion.Original;  
  
// Add the RowUpdated event handler.  
adapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Customers");  
  
// Modify the DataSet contents.  
  
adapter.Update(dataSet, "Customers");  
  
foreach (DataRow dataRow in dataSet.Tables["Customers"].Rows)  
{  
    if (dataRow.HasErrors)  
       Console.WriteLine(dataRow [0] + "\n" + dataRow.RowError);  
}  
  
protected static void OnRowUpdated(object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.RecordsAffected == 0)   
  {  
    args.Row.RowError = "Optimistic Concurrency Violation Encountered";  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## Voir aussi  
 [Extraction et modification de données dans ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Mise à jour de sources de données avec des DataAdapters](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Informations sur les erreurs de ligne](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-error-information.md)   
 [Transactions et concurrence](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [Fournisseurs managés ADO.NET et Centre de développement de DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)