---
title: COLLECTION (Entity SQL)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 03228bfa-be3a-4ccc-82f8-eee429f85cf1
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8d078749d20740cdade323edab975ce221e72cfa
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="collection-entity-sql"></a>COLLECTION (Entity SQL)
Le mot clé COLLECTION est utilisé uniquement dans la définition d'une fonction incluse. Les fonctions de collection sont des fonctions qui fonctionnent sur une collection de valeurs et produisent une sortie scalaire.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
COLLECTION(type_definition)   
```  
  
## <a name="arguments"></a>Arguments  
 `type_definition`  
 Expression qui retourne une collection de types, lignes ou références pris en charge.  
  
## <a name="remarks"></a>Remarques  
 Pour plus d’informations sur le mot clé COLLECTION, consultez [Type Definitions](../../../../../../docs/framework/data/adonet/ef/language-reference/type-definitions-entity-sql.md).  
  
## <a name="example"></a>Exemple  
 L'exemple suivant montre comment utiliser le mot clé COLLECTION pour déclarer une collection de décimales en tant qu'argument pour une fonction de requête incluse.  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]  
  
## <a name="see-also"></a>Voir aussi  
 [Référence Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
