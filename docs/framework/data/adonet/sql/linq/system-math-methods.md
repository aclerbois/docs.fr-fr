---
title: "System.Math, méthodes"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0f299521-6f41-4720-bd70-67c93fc50948
caps.latest.revision: "2"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: af5e18b9c4334cfab26c9a84ac647bb433391ef1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="systemmath-methods"></a>System.Math, méthodes
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ne prend pas en charge les méthodes <xref:System.Math> suivantes.  
  
-   <xref:System.Math.DivRem%28System.Int32%2CSystem.Int32%2CSystem.Int32%40%29?displayProperty=nameWithType>  
  
-   <xref:System.Math.DivRem%28System.Int64%2CSystem.Int64%2CSystem.Int64%40%29?displayProperty=nameWithType>  
  
-   <xref:System.Math.IEEERemainder%28System.Double%2CSystem.Double%29?displayProperty=nameWithType>  
  
## <a name="differences-from-net"></a>Différences par rapport à .NET  
 Le .NET Framework présente une sémantique d'arrondi différente de SQL Server. Le <xref:System.Math.Round%2A> méthode dans le .NET Framework exécute *l’arrondi bancaire*, où les nombres qui se terminant par.5 sont arrondies à la plus proche de chiffre pair et non au chiffre supérieur suivant. Par exemple, 2,5 est arrondi à 2 et 3,5 à 4. Cette technique permet d'éviter les écarts systématiques vers des valeurs supérieures dans les transactions de données importantes.  
  
 Dans SQL, la fonction `ROUND` arrondit toujours vers le chiffre supérieur. Ainsi, 2,5 est arrondi à 3 (contre 2 dans le .NET Framework).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] passe par la sémantique `ROUND` de SQL et ne tente pas d'implémenter l'arrondi bancaire.  
  
## <a name="see-also"></a>Voir aussi  
 [Fonctions et Types de données](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
