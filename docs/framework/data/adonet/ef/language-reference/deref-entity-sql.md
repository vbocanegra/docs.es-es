---
title: "DEREF (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 4c78e833-b260-453d-9bf4-eb39857dd0fa
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DEREF (Entity SQL)
Desreferencia un valor de referencia y genera el resultado de dicha desreferenciación.  
  
## Sintaxis  
  
```  
  
SELECT DEREF ( o.expression) from Table as o;  
```  
  
## Argumentos  
 `expression`  
 Expresión de consulta válida que devuelve una colección.  
  
## Valor devuelto  
 El valor de la entidad a la que se hace referencia.  
  
## Comentarios  
 El operador DEREF desreferencia un valor de referencia y genera el resultado de dicha desreferenciación. Por ejemplo, si `r` es una referencia de tipo ref\<T\>, `Deref` `(r)` es una expresión de tipo `T` que obtiene la entidad a la que `r` hace referencia. Si el valor de referencia es NULL, o está pendiente \(es decir, el destino de la referencia no existe\), el resultado del operador DEREF es NULL.  
  
## Ejemplo  
 La consulta [!INCLUDE[esql](../../../../../../includes/esql-md.md)] utiliza el operador DEREF para desreferenciar un valor de referencia y generar el resultado de dicha desreferenciación. La consulta se basa en el modelo AdventureWorks Sales. Para compilar y ejecutar esta consulta, siga estos pasos:  
  
1.  Siga el procedimiento de [Ejecutar una consulta que devuelve resultados PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Pase la consulta siguiente como argumento al método ExecutePrimitiveTypeQuery:  
  
 [!code-csharp[DP EntityServices Concepts 2#DEREF](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#deref)]  
  
## Vea también  
 [Referencia de Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)   
 [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)   
 [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)   
 [Tipos estructurados que aceptan valores NULL](../../../../../../docs/framework/data/adonet/ef/language-reference/nullable-structured-types-entity-sql.md)