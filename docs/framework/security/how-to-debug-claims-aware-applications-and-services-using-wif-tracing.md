---
title: "Guide pratique pour déboguer les applications prenant en charge les revendications et les services utilisant le suivi WIF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d51ba59-3adb-4ca4-bd33-5027531af687
caps.latest.revision: "7"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.openlocfilehash: 36cb961345cb724597d8e48ec3be6cbb84df4632
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-debug-claims-aware-applications-and-services-using-wif-tracing"></a>Guide pratique pour déboguer les applications prenant en charge les revendications et les services utilisant le suivi WIF
## <a name="applies-to"></a>S'applique à  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   Service Trace Viewer Tool (SvcTraceViewer.exe)  
  
-   Dépannage et débogage des applications WIF  
  
## <a name="summary"></a>Résumé  
 Cette procédure décrit les étapes à suivre pour configurer le suivi WIF, collecter les journaux de suivi et analyser ceux-ci à l'aide de l'outil Trace Viewer. Elle établit une correspondance générale entre les entrées de suivi et les mesures nécessaires pour résoudre les problèmes liés à WIF.  
  
## <a name="contents"></a>Sommaire  
  
-   Objectifs  
  
-   Résumé des étapes  
  
-   Étape 1 : configurer le suivi WIF à l'aide du fichier de configuration Web.config  
  
-   Étape 2 : analyser les fichiers de suivi WIF à l'aide de l'outil Trace Viewer  
  
-   Étape 3 : identifier les solutions pour corriger les problèmes liés à WIF  
  
-   Éléments associés  
  
## <a name="objectives"></a>Objectifs  
  
-   Configurer le suivi WIF.  
  
-   Consulter les journaux de suivi dans l'outil Trace Viewer.  
  
-   Identifier les problèmes liés à WIF dans les journaux de suivi.  
  
-   Prendre des mesures correctives pour les problèmes liés à WIF décelés dans les journaux de suivi.  
  
## <a name="summary-of-steps"></a>Résumé des étapes  
  
-   Étape 1 : configurer le suivi WIF à l'aide du fichier de configuration Web.config  
  
-   Étape 2 : analyser les fichiers de suivi WIF à l'aide de l'outil Trace Viewer  
  
-   Étape 3 : identifier les solutions pour corriger les problèmes liés à WIF  
  
## <a name="step-1--configure-wif-tracing-using-webconfig-configuration-file"></a>Étape 1 : configurer le suivi WIF à l'aide du fichier de configuration Web.config  
 Dans cette étape, vous allez apporter des modifications aux sections de configuration du fichier *Web.config* pour permettre à WIF de suivre ses événements et les stocker dans un journal de suivi.  
  
#### <a name="to-configure-wif-tracing-using-webconfig-configuration-file"></a>Pour configurer le suivi WIF à l'aide du fichier de configuration Web.config  
  
1.  Ouvrez le fichier de configuration racine **Web.config** ou **App.config** dans l’éditeur Visual Studio en double-cliquant dessus dans l’**Explorateur de solutions**. Si votre solution n’a pas de fichier de configuration **Web.config** ou **App.config**, ajoutez-le en cliquant avec le bouton droit sur la solution dans l’**Explorateur de solutions** et en cliquant sur **Ajouter**, puis sur **Nouvel élément...**. Dans la boîte de dialogue **Nouvel élément**, sélectionnez **Fichier de configuration de l’application** pour **App.config** ou **Fichier de configuration web** pour **Web.config** dans la liste, puis cliquez sur **OK**.  
  
2.  Ajoutez les entrées de configuration similaires aux suivantes au fichier de configuration dans le nœud **\<configuration>** à la fin du fichier de configuration :  
  
    ```xml  
    <system.diagnostics>  
        <sources>  
            <source name="System.IdentityModel" switchValue="Verbose">  
                <listeners>  
                    <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="WIFTrace.e2e"/>  
                </listeners>  
            </source>  
        </sources>  
        <trace autoflush="true"/>  
    </system.diagnostics>  
    ```  
  
3.  La configuration ci-dessus indique à WIF de générer des événements de suivi détaillés et de les consigner dans le fichier *WIFTrace.e2e*. Pour obtenir la liste complète des valeurs du commutateur **switchValue**, consultez le tableau Niveau de suivi dans la rubrique suivante : [Configuration du suivi](http://msdn.microsoft.com/library/ms733025.aspx).  
  
## <a name="step-2--analyze-wif-trace-files-using-trace-viewer-tool"></a>Étape 2 : analyser les fichiers de suivi WIF à l'aide de l'outil Trace Viewer  
 Dans cette étape, vous allez utiliser l'outil Trace Viewer (SvcTraceViewer.exe) pour analyser les journaux de suivi WIF.  
  
#### <a name="to-analyze-wif-trace-logs-using-trace-viewer-tool-svctraceviewerexe"></a>Pour analyser les journaux de suivi WIF à l'aide de l'outil Trace Viewer (SvcTraceViewer.exe)  
  
1.  L'outil Trace Viewer (SvcTraceViewer.exe) est fourni avec le Kit de développement logiciel (SDK) Windows. Si vous n’avez pas déjà installé le kit SDK Windows, vous pouvez le télécharger ici : [SDK Windows](http://www.microsoft.com/download/en/details.aspx?id=8279).  
  
2.  Exécutez l'outil Trace Viewer (SvcTraceViewer.exe). Celui-ci se trouve généralement dans le dossier **Bin** du chemin d’installation.  
  
3.  Ouvrez le fichier journal de suivi WIF, par exemple WIFTrace.e2e, en sélectionnant l’option **Fichier**, **Ouvrir...** du menu ou en utilisant le raccourci **Ctrl+O**. Le fichier journal de suivi s'ouvre dans l'outil Trace Viewer.  
  
4.  Examinez les entrées sous l’onglet **Activité**. Chaque entrée doit contenir un numéro d'activité, le nombre de suivis qui ont été consignés, la durée de l'activité et ses horodateurs de début et de fin.  
  
5.  Cliquez sur l’onglet **Activité**. Des entrées de suivi détaillées doivent s'afficher dans la zone principale de l'outil. Utilisez la liste déroulante **Niveau** du menu pour filtrer un niveau spécifique de suivi, par exemple : **Tout**, **Avertissement**, **Erreurs**, **Informations**, etc.  
  
6.  Cliquez sur des entrées de suivi spécifiques pour les examiner dans le détail dans la zone inférieure de l’outil. Les détails peuvent être visualisés dans la vue **Mis en forme** ou **XML** en choisissant les onglets correspondants.  
  
## <a name="step-3--identify-solutions-to-fix-wif-related-issues"></a>Étape 3 : identifier les solutions pour corriger les problèmes liés à WIF  
 Dans cette étape, vous pouvez identifier des solutions pour les problèmes liés à WIF identifiés à l'aide du journal de suivi WIF et de l'outil Trace Viewer. Elle établit une correspondance générale entre les exceptions liées à WIF et les solutions potentielles ou les mesures à prendre pour résoudre les problèmes.  
  
#### <a name="to-identify-solutions-to-fix-wif-related-issues"></a>Pour identifier les solutions en vue de corriger les problèmes liés WIF  
  
1.  Consultez ci-dessous le tableau des exceptions WIF et des mesures à prendre pour corriger les problèmes.  
  
|**ID d’erreur**|**Message d'erreur**|**Mesure à prendre pour corriger l’erreur**|  
|-|-|-|  
|ID4175|L'émetteur du jeton de sécurité n'a pas été reconnu par IssuerNameRegistry.  Pour accepter les jetons de sécurité en provenance de cet émetteur, configurez IssuerNameRegistry pour qu'il retourne un nom valide pour cet émetteur.|Cette erreur peut être provoquée par la copie d’une empreinte numérique à partir du composant logiciel enfichable MMC et par son collage dans le fichier *Web.config*. Plus précisément, vous pouvez obtenir un caractère non imprimable supplémentaire dans la chaîne de texte en effectuant une copie à partir de la fenêtre de propriétés du certificat. Ce caractère supplémentaire entraîne l’échec de la correspondance de l’empreinte numérique. La procédure correcte de copie de l’empreinte numérique se trouve ici : [http://msdn.microsoft.com/library/ff359102.aspx](http://msdn.microsoft.com/library/ff359102.aspx)|  
  
## <a name="related-items"></a>Éléments associés  
  
-   [Utilisation de Service Trace Viewer pour afficher les suivis corrélés et résoudre les problèmes](http://msdn.microsoft.com/library/aa751795.aspx)
