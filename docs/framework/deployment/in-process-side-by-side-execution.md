---
title: "Exécution côte à côte in-process"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- in-process side-by-side execution
- side-by-side execution, in-process
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
caps.latest.revision: "25"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: fa65be2eee481e20231bacb5d0861fa3d2c03f92
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="in-process-side-by-side-execution"></a>Exécution côte à côte in-process
Depuis [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], vous pouvez utiliser l’hébergement côte à côte in-process pour exécuter plusieurs versions du CLR (Common Language Runtime) dans un processus unique. Par défaut, les composants COM managés s’exécutent avec la version du .NET Framework avec laquelle ils ont été générés, indépendamment de la version du .NET Framework chargée pour le processus.  
  
## <a name="background"></a>Présentation  
 Le .NET Framework a toujours fourni un hébergement côte à côte pour les applications de code managé, mais avant [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], il ne fournissait pas cette fonctionnalité pour les composants COM managés. Dans le passé, les composants COM managés chargés dans un processus étaient exécutés avec la version du runtime déjà chargée ou avec la version installée la plus récente du .NET Framework. Si cette version n’était pas compatible avec le composant COM, le composant échouait.  
  
 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] fournit une nouvelle approche de l’hébergement côte à côte qui s’assure des éléments suivants :  
  
-   L’installation d’une nouvelle version du .NET Framework n’a aucun effet sur les applications existantes.  
  
-   Les applications sont exécutées avec la version du .NET Framework avec laquelle elles ont été générées. Elles n’utilisent pas la nouvelle version du .NET Framework, à moins que cela ne leur soit expressément demandé. Il est toutefois plus facile pour les applications de passer à une nouvelle version du .NET Framework.  
  
## <a name="effects-on-users-and-developers"></a>Effets sur les utilisateurs et les développeurs  
  
-   **Utilisateurs finaux et administrateurs système**. Ces utilisateurs savent désormais que, quand ils installent une nouvelle version du runtime, soit indépendamment soit avec une application, cela n’aura aucun impact sur leurs ordinateurs. Les applications existantes continueront de fonctionner comme auparavant.  
  
-   **Développeurs d’applications**. L’hébergement côte à côte n’a presque aucun effet sur les développeurs d’applications. Par défaut, les applications sont toujours exécutées avec la version du .NET Framework avec laquelle elles ont été créées. Cela n’a pas changé. Toutefois, les développeurs peuvent substituer ce comportement et demander à l’application de s’exécuter sous une version plus récente du .NET Framework (consultez le [scénario 2](#scenarios)).  
  
-   **Consommateurs et développeurs de bibliothèques**. L’hébergement côte à côte ne résout pas les problèmes de compatibilité rencontrés par les développeurs de bibliothèques. Une bibliothèque chargée directement par une application, soit via une référence directe soit via un appel <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>, continue d’utiliser le runtime du <xref:System.AppDomain> dans lequel elle est chargée. Vous devez tester vos bibliothèques sur toutes les versions du .NET Framework que vous souhaitez prendre en charge. Si une application est compilée à l’aide du runtime [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] mais inclut une bibliothèque créée à l’aide d’un runtime antérieur, cette bibliothèque utilisera également le runtime [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Toutefois, si vous possédez une application générée à l’aide d’un runtime antérieur et une bibliothèque créée à l’aide de [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], vous devez forcer votre application à utiliser également [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] (consultez le [scénario 3](#scenarios)).  
  
-   **Développeurs de composants COM managés**. Dans le passé, les composants COM managés étaient automatiquement exécutés à l’aide de la version la plus récente du runtime installée sur l’ordinateur. Vous pouvez maintenant exécuter les composants COM avec la version du runtime avec laquelle ils ont été créés.  
  
     Comme indiqué dans le tableau suivant, les composants générés avec .NET Framework version 1.1 peuvent s’exécuter côte à côte avec les composants de la version 4, mais ils ne peuvent pas s’exécuter avec les composants de la version 2.0, 3.0 ni 3.5, car l’hébergement côte à côte n’est pas disponible pour ces versions.  
  
    |Version du .NET Framework|1.1|2.0 - 3.5|4|  
    |----------------------------|---------|----------------|-------|  
    |1.1|Non applicable|Non|Oui|  
    |2.0 - 3.5|Non|Non applicable|Oui|  
    |4|Oui|Oui|Non applicable|  
  
> [!NOTE]
>  Les versions 3.0 et 3.5 du .NET Framework sont générées de façon incrémentielle sur la version 2.0 et n’ont pas besoin de fonctionner côte à côte. Il s’agit fondamentalement de la même version.  
  
<a name="scenarios"></a>   
## <a name="common-side-by-side-hosting-scenarios"></a>Scénarios d’hébergement côte à côte courants  
  
-   **Scénario 1 :** application native qui utilise des composants COM créés avec des versions antérieures du .NET Framework.  
  
     Versions du .NET Framework installées : [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] et toutes les autres versions du .NET Framework utilisées par les composants COM.  
  
     Que faire : dans ce scénario, ne faites rien. Les composants COM s’exécuteront avec la version du .NET Framework avec laquelle ils ont été inscrits.  
  
-   **Scénario 2 :** application managée créée avec [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] que vous préféreriez exécuter avec [!INCLUDE[dnprdnext](../../../includes/dnprdnext-md.md)], mais que vous voulez bien exécuter sur [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] si la version 2.0 est absente.  
  
     Versions du .NET Framework installées : une version antérieure du .NET Framework et [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Que faire : dans le [fichier de configuration de l’application](../../../docs/framework/configure-apps/index.md) dans le répertoire de l’application, utilisez l’[élément \<startup>](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) et l’[élément \<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) défini comme suit :  
  
    ```xml  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
-   **Scénario 3 :** application native qui utilise des composants COM créés avec des versions antérieures du .NET Framework que vous souhaitez exécuter avec [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Versions du .NET Framework installées : [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
     Que faire : dans le fichier de configuration de l’application dans le répertoire de l’application, utilisez l’élément `<startup>` avec l’attribut `useLegacyV2RuntimeActivationPolicy` défini sur `true` et l’élément `<supportedRuntime>` défini comme suit :  
  
    ```xml  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## <a name="example"></a>Exemple  
 L’exemple suivant montre un hôte COM non managé qui exécute un composant COM managé à l’aide de la version du .NET Framework dans laquelle le composant a été compilé.  
  
 Pour exécuter l’exemple suivant, compilez et inscrivez le composant COM managé suivant avec [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)]. Pour inscrire le composant, dans le menu **Projet**, cliquez sur **Propriétés**, sur l’onglet **Générer**, puis cochez la case **Inscrire pour COM Interop**.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 Compilez l’application C++ non managée suivante, ce qui active l’objet COM créé par l’exemple précédent.  
  
```  
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");   
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
```  
  
## <a name="see-also"></a>Voir aussi  
 [\<démarrage > élément](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)  
 [\<supportedRuntime>, élément](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)
