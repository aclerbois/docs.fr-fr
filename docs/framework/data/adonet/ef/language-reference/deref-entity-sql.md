---
title: DEREF (Entity SQL)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c78e833-b260-453d-9bf4-eb39857dd0fa
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 49ae645baccf877a8e9c0f80ac8827823b9d6c34
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="deref-entity-sql"></a>DEREF (Entity SQL)
Déréférence une valeur de référence et génère le résultat de ce déréférencement.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
SELECT DEREF ( o.expression ) from Table as o;  
```  
  
## <a name="arguments"></a>Arguments  
 `expression`  
 Toute expression de requête valide qui retourne une collection.  
  
## <a name="return-value"></a>Valeur de retour  
 Valeur de l'entité référencée.  
  
## <a name="remarks"></a>Remarques  
 L'opérateur DEREF déréférence une valeur de référence et génère le résultat de ce déréférencement. Par exemple, si `r` est une référence de type ref\<T >, `Deref``(r)` est une expression de type `T` qui génère l’entité référencée par `r`. Si la valeur de référence est null ou non résolue (autrement dit, la cible de la référence n'existe pas), le résultat de l'opérateur DEREF est null.  
  
## <a name="example"></a>Exemple  
 La requête [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ci-dessous utilise l'opérateur DEREF pour déréférencer une valeur de référence et générer le résultat de ce déréférencement. Cette requête est basée sur le modèle de vente AdventureWorks Sales Model. Pour compiler et exécuter cette requête, procédez comme suit :  
  
1.  Suivez la procédure de [Comment : exécuter une requête qui retourne des résultats PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passez à la méthode ExecutePrimitiveTypeQuery la requête suivante en tant qu'argument :  
  
 [!code-csharp[DP EntityServices Concepts 2#DEREF](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#deref)]  
  
## <a name="see-also"></a>Voir aussi  
 [Référence Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)  
 [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)  
 [CLÉ](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)  
 [Types structurés Nullable](../../../../../../docs/framework/data/adonet/ef/language-reference/nullable-structured-types-entity-sql.md)
