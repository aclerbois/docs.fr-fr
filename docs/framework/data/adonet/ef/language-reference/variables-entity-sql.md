---
title: Variables (Entity SQL)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3eed222a-f8f6-46b6-9cd5-220cc0e4e5d8
caps.latest.revision: "2"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 551b6d6feab6829c9a2f6f2e89e1918acf463411
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="variables-entity-sql"></a>Variables (Entity SQL)
## <a name="variable"></a>Variable  
 Une expression de variable est une référence à une expression nommée dans la portée actuelle. Une référence de variable doit être un [!INCLUDE[esql](../../../../../../includes/esql-md.md)] identificateur, tel que défini dans [identificateurs](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md).  
  
 L'exemple suivant montre l'utilisation d'une variable dans l'expression. Le `c` dans la clause FROM représente la définition de la variable. Le `c` dans la clause SELECT représente la référence à la variable.  
  
```  
select c   
from LOB.customers as c  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Identificateurs](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)  
 [Paramètres](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)  
 [Vue d’ensemble de Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)
