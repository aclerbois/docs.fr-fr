---
title: Getting Started, exemple
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: basic samples [WCF], getting started
ms.assetid: 967a3d94-0261-49ff-b85a-20bb07f1af20
caps.latest.revision: "60"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: a5ff6af234fabf278c84a3487b9f65217d84f6e4
ms.sourcegitcommit: ce279f2d7fe2220e6ea0a25a8a7a5370ddf8d9f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2017
---
# <a name="getting-started-sample"></a>Getting Started, exemple
Cet exemple montre comment implémenter un service et un client standard à l'aide de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. Cet exemple constitue la base de tous les autres exemples de technologie de base.  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\GettingStarted\GettingStarted`  
  
 Le service décrit les opérations qu'il effectue dans un contrat de service qu'il expose publiquement sous forme de métadonnées. Le service contient également le code pour implémenter les opérations.  
  
 Le client contient une définition du contrat de service et une classe proxy permettant d'accéder au service. Le code proxy est généré dans les métadonnées de service à l’aide de la [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
 Sur [!INCLUDE[wv](../../../../includes/wv-md.md)], le service est hébergé dans le service d'activation de processus de Windows (WAS). Sur [!INCLUDE[wxp](../../../../includes/wxp-md.md)] et [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], il est hébergé par les services IIS (Internet Information Services) et ASP.NET. L'hébergement d'un service dans les services IIS ou WAS lui permet d'être activé automatiquement lorsqu'il est accédé pour la première fois.  
  
> [!NOTE]
>  Si vous préférez commencer avec un exemple qui héberge le service dans une application de console au lieu d’IIS, consultez la [auto-hébergement](../../../../docs/framework/wcf/samples/self-host.md) exemple.  
  
 Le service et le client spécifient les détails d'accès dans les paramètres du fichier de configuration, qui fournissent la souplesse au moment du déploiement. Cela inclut une définition de point de terminaison qui spécifie une adresse, une liaison et un contrat. La liaison spécifie des détails de sécurité et de transport sur la manière dont le service doit être accédé.  
  
 Le service configure un comportement au moment de l'exécution pour publier ses métadonnées.  
  
 Le service implémente un contrat qui définit un modèle de communication demande-réponse. Le contrat est défini par l'interface `ICalculator`, laquelle expose les opérations mathématiques suivantes : addition, soustraction, multiplication et division. Le client adresse des demandes à une opération mathématique donnée et le service répond avec le résultat. Le service implémente un contrat `ICalculator` qui est défini dans le code suivant.  
  
```vb  
' Define a service contract.  
    <ServiceContract(Namespace:="http://Microsoft.Samples.GettingStarted")>  
     Public Interface ICalculator  
        <OperationContract()>  
        Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double  
        <OperationContract()>  
        Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double  
    End Interface  
```  
  
```csharp  
// Define a service contract.  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
```  
  
 L'implémentation de service calcule et retourne le résultat approprié, tel qu'indiqué dans l'exemple de code suivant.  
  
```vb  
' Service class which implements the service contract.  
Public Class CalculatorService  
Implements ICalculator  
Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add  
Return n1 + n2  
End Function  
  
Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract  
Return n1 - n2  
End Function  
  
Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply  
Return n1 * n2  
End Function  
  
Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide  
Return n1 / n2  
End Function  
End Class  
```  
  
```csharp  
// Service class that implements the service contract.  
public class CalculatorService : ICalculator  
{  
    public double Add(double n1, double n2)  
    {  
        return n1 + n2;  
    }  
    public double Subtract(double n1, double n2)  
    {  
        return n1 - n2;  
    }  
    public double Multiply(double n1, double n2)  
    {  
        return n1 * n2;  
    }  
    public double Divide(double n1, double n2)  
    {  
        return n1 / n2;  
    }  
}  
```  
  
 Le service expose un point de terminaison permettant de communiquer avec le service, défini à l'aide d'un fichier de configuration (Web.config), tel qu'indiqué dans l'exemple de configuration suivant.  
  
```xaml  
<services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- ICalculator is exposed at the base address provided by  
         host: http://localhost/servicemodelsamples/service.svc.  -->  
       <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
       ...  
    </service>  
</services>  
```  
  
 Le service expose le point de terminaison au niveau de l'adresse de base fournie par l'hôte IIS ou WAS. La liaison est configurée avec un <xref:System.ServiceModel.WSHttpBinding> standard, qui fournit la communication HTTP et les protocoles de service Web standard pour l'adressage et la sécurité. Le contrat correspond au `ICalculator` implémenté par le service.  
  
 Tel qu'il est configuré, le service est accessible à l'adresse http://localhost/servicemodelsamples/service.svc par un client sur le même ordinateur. Pour que les clients installés sur des ordinateurs distants puissent accéder au service, un nom de domaine complet doit être spécifié au lieu de localhost.  
  
 Par défaut, l'infrastructure n'expose pas de métadonnées. Par conséquent, le serveur active <xref:System.ServiceModel.Description.ServiceMetadataBehavior> et expose un point de terminaison d'échange de métadonnées (MEX) à l'adresse http://localhost/servicemodelsamples/service.svc/mex. La configuration suivante montre comment procéder.  
  
```xaml  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      ...  
      <!-- the mex endpoint is explosed at  
       http://localhost/servicemodelsamples/service.svc/mex -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults  
   attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 Le client communique à l’aide d’un type de contrat donné à l’aide d’une classe de client qui est générée par le [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Ce client généré est contenu dans le fichier generatedClient.cs ou generatedClient.vb. Cet utilitaire récupère les métadonnées pour un service donné et génère un client destiné à être utilisé par l'application cliente pour communiquer à l'aide d'un type de contrat donné. Le service hébergé doit être disponible pour générer le code client, car il permet de récupérer les métadonnées mises à jour.  
  
 Exécutez la commande suivante à partir de l'invite de commandes du Kit de développement SDK du répertoire client pour générer le proxy typé :  
  
```  
svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
```  
  
 Pour générer le client en Visual Basic, tapez la commande suivante à partir de l'invite de commandes du Kit de développement SDK :  
  
 `Svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb`  
  
 En utilisant le client généré, le client peut accéder à un point de terminaison de service donné en configurant l’adresse et la liaison appropriées. À l'instar du service, le client utilise un fichier de configuration (App.config) pour spécifier le point de terminaison avec lequel il souhaite communiquer. La configuration de point de terminaison client se compose d'une adresse absolue pour le point de terminaison de service, de la liaison et du contrat, tel qu'indiqué dans l'exemple suivant.  
  
```xaml  
<client>  
     <endpoint  
         address="http://localhost/servicemodelsamples/service.svc"   
         binding="wsHttpBinding"   
         contract=" Microsoft.ServiceModel.Samples.ICalculator" />  
</client>  
```  
  
 L'implémentation cliente instancie le client et utilise l'interface typée pour commencer à communiquer avec le service, tel qu'indiqué dans l'exemple de code suivant.  
  
```vb  
' Create a client  
Dim client As New CalculatorClient()  
  
' Call the Add service operation.  
            Dim value1 = 100.0R  
            Dim value2 = 15.99R  
            Dim result = client.Add(value1, value2)  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)  
  
' Call the Subtract service operation.  
value1 = 145.00R  
value2 = 76.54R  
result = client.Subtract(value1, value2)  
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result)  
  
' Call the Multiply service operation.  
value1 = 9.00R  
value2 = 81.25R  
result = client.Multiply(value1, value2)  
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result)  
  
' Call the Divide service operation.  
value1 = 22.00R  
value2 = 7.00R  
result = client.Divide(value1, value2)  
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result)  
  
'Closing the client gracefully closes the connection and cleans up resources  
```  
  
```csharp  
// Create a client.  
CalculatorClient client = new CalculatorClient();  
  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
// Call the Subtract service operation.  
value1 = 145.00D;  
value2 = 76.54D;  
result = client.Subtract(value1, value2);  
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
// Call the Multiply service operation.  
value1 = 9.00D;  
value2 = 81.25D;  
result = client.Multiply(value1, value2);  
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
// Call the Divide service operation.  
value1 = 22.00D;  
value2 = 7.00D;  
result = client.Divide(value1, value2);  
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
//Closing the client releases all communication resources.  
client.Close();  
```  
  
 Lorsque vous exécutez l'exemple, les demandes et réponses d'opération s'affichent dans la fenêtre de console du client. Appuyez sur Entrée dans la fenêtre du client pour l'arrêter.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 Cet exemple présente la méthode standard utilisée pour créer un service et un client. L’autre [base](../../../../docs/framework/wcf/samples/basic-sample.md) build sur cet exemple pour illustrer les fonctionnalités de produit spécifique.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez-vous d’avoir effectué la [procédure d’installation d’à usage unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l’édition C# ou Visual Basic .NET de la solution, conformez-vous aux instructions figurant dans [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Pour exécuter l’exemple dans une configuration à un ou plusieurs ordinateurs, suivez les instructions de [en cours d’exécution les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Guide pratique pour héberger un service WCF dans une application managée](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)  
 [How to: Host a WCF Service in IIS (Comment : héberger un service WCF dans IIS)](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)
