---
title: Moderniser du cycle de vie de votre application avec l’élément de configuration/CD pipelines et les outils DevOps dans le cloud
description: Moderniser des applications .NET existantes avec des conteneurs de Cloud Azure et Windows | Moderniser du cycle de vie de votre application avec l’élément de configuration/CD pipelines et les outils DevOps dans le cloud
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 63907a1911b4c95f0dbecb2af33964225cf3e7b1
ms.sourcegitcommit: 88f251b08bf0718ce119f3d7302f514b74895038
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2018
---
# <a name="modernize-your-apps-lifecycle-with-cicd-pipelines-and-devops-tools-in-the-cloud"></a>Moderniser du cycle de vie de votre application avec l’élément de configuration/CD pipelines et les outils DevOps dans le cloud

Les entreprises d’aujourd'hui doivent innover à un rythme rapide pour être concurrentiel sur le marché. Fourniture de haute qualité, des applications modernes requiert les outils DevOps et processus critiques pour implémenter ce cycle constant d’innovation. Avec les outils DevOps appropriés, les développeurs peuvent simplifier le déploiement continu et obtenir plus rapidement des applications innovantes dans les mains d’utilisateurs.

Bien que les pratiques de déploiement et d’intégration continues sont bien établies, l’introduction de conteneurs introduit considérations relatives à la nouvelle, en particulier lorsque vous travaillez avec des applications de conteneur multiples.

Visual Studio Team Services prend en charge l’intégration continue et déploiement d’applications de conteneur multiples à une variété d’environnements à travers les tâches de déploiement officiels Team Services :

-   [Déployer à la version autonome de machine virtuelle d’hôte Docker](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-docker-windowsvm) (Linux ou Windows Server 2016 ou version ultérieure)

-   [Déployer sur l’infrastructure de Service](https://docs.microsoft.com/azure/service-fabric/service-fabric-tutorial-deploy-app-with-cicd-vsts)

-   [Déployer sur le Service de conteneur Azure – Kubernetes](https://docs.microsoft.com/vsts/build-release/apps/cd/azure/deploy-container-kubernetes)

Mais vous pouvez également déployer sur [Docker Swarm](https://blogs.msdn.microsoft.com/jcorioland/2016/11/29/full-ci-cd-pipeline-to-deploy-multi-containers-application-on-azure-container-service-docker-swarm-using-visual-studio-team-services/) ou contrôleur de domaine/système d’exploitation à l’aide de tâches de script basé sur Team Services.

Pour continuer à faciliter l’agilité de déploiement, ces outils fournissent excellent développement-test-production déploiement expériences pour les charges de travail conteneur, avec un choix de développement et des solutions de l’élément de configuration/CD.

Figure 4-12 montre un pipeline de déploiement continu qui se déploie sur un cluster Kubernetes dans le Service de conteneur Azure.

![Pipeline d’un déploiement continu Visual Studio Team Services, déploiement vers un cluster Kubernetes](./media/image12.png)

> **Figure 4-12.** Pipeline d’un déploiement continu Visual Studio Team Services, déploiement vers un cluster Kubernetes

>[!div class="step-by-step"]
[Précédent](modernize-your-apps-with-monitoring-and-telemetry.md)
[Suivant](migrate-to-hybrid-cloud-scenarios.md)