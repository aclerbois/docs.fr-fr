---
title: "Sécurisation des applications ADO.NET"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 005a1d43-6ee5-471e-ad98-1d30a44d49d5
caps.latest.revision: "4"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 143447020f41368a3553a0c8cda78e80806b75ba
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="securing-adonet-applications"></a>Sécurisation des applications ADO.NET
L'écriture d'une application ADO.NET sécurisée ne se limite pas à éviter les pièges de codage courants, tels que la non validation des entrées d'utilisateur. Une application qui accède à des données présente de nombreux points de défaillance possibles qu'un agresseur peut exploiter pour extraire, manipuler ou détruire des données sensibles. Il est donc important de comprendre tous les aspects de la sécurité, depuis le processus de modélisation de menace durant la phase de conception de votre application, jusqu'à son déploiement éventuel et sa maintenance en cours.  
  
 Le .NET Framework fournit de nombreux services, classes et outils utiles permettant de sécuriser et d'administrer des applications de base de données. Le Common Language Runtime (CLR) fournit un environnement de type sécurisé pour l'exécution du code, avec une sécurité d'accès du code pour restreindre les autorisations de code managé. L'adoption des procédés de codage sécurisés pour l'accès aux données permet de réduire les dommages infligés par un intrus potentiel.  
  
 L'écriture d'un code sécurisé ne protège pas contre les défaillances de sécurité volontaires lors de l'utilisation de ressources non managées telles que des bases de données. La plupart des bases de données de serveur, telles que SQL Server, possèdent leurs propres systèmes de sécurité qui renforcent la sécurité si ceux-ci sont correctement implémentés. Cependant, même une source de données équipée d'un système de sécurité robuste peut faire l'objet d'une attaque si elle n'est pas configurée de manière appropriée.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Vue d’ensemble de la sécurité](../../../../docs/framework/data/adonet/security-overview.md)  
 Fournit des recommandations pour la conception d'applications ADO.NET sécurisées.  
  
 [Sécuriser l’accès aux données](../../../../docs/framework/data/adonet/secure-data-access.md)  
 Décrit comment utiliser des données à partir d'une source de données sécurisée.  
  
 [Sécuriser les Applications clientes](../../../../docs/framework/data/adonet/secure-client-applications.md)  
 Décrit des considérations sur la sécurité pour les applications clientes.  
  
 [Sécurité d’accès du code et ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)  
 Décrit comment utiliser la sécurité d'accès du code (CAS) pour protéger le code ADO.NET. Explique également comment travailler avec une confiance partielle.  
  
 [Confidentialité et sécurité des données](../../../../docs/framework/data/adonet/privacy-and-data-security.md)  
 Décrit les options de chiffrement pour les applications ADO.NET.  
  
## <a name="related-sections"></a>Rubriques connexes  
 [Sécurité SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)  
 Décrit les fonctionnalités de sécurité SQL Server du point de vue d’un développeur.  
  
 [Considérations sur la sécurité](../../../../docs/framework/data/adonet/ef/security-considerations.md)  
 Décrit la sécurité des applications reposant sur Entity Framework.  
  
 [Sécurité](../../../../docs/standard/security/index.md)  
 Contient des liens vers des rubriques qui décrivent tous les aspects de la sécurité dans le .NET Framework.  
  
 [Outils de sécurité](http://msdn.microsoft.com/en-us/2a3eb98a-2de6-4fba-b41c-01a74d354c11)  
 Outils .NET Framework pour la sécurisation et l'administration de la stratégie de sécurité.  
  
 [Ressources pour la création d’Applications sécurisées](http://msdn.microsoft.com/en-us/0ebf5f69-76f2-498a-a2df-83cf3443e132)  
 Fournit des liens vers des rubriques pour la création d'applications sécurisées.  
  
 [Bibliographie relative à la sécurité](/visualstudio/ide/security-bibliography)  
 Fournit des liens vers des ressources externes disponibles en ligne et sous forme de documentation.  
  
## <a name="see-also"></a>Voir aussi  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 [Fournisseurs managés ADO.NET et centre de développement DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)
