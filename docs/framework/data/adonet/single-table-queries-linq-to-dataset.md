---
title: "Consultas de tabla &#250;nica (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b74bcf8-3f87-449f-bff7-6bcb0d69d212
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Consultas de tabla &#250;nica (LINQ to DataSet)
Las consultas [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] operan en orígenes de datos que implementan la interfaz <xref:System.Collections.Generic.IEnumerable%601> o la interfaz <xref:System.Query.IQueryable%601>.  La clase <xref:System.Data.DataTable> no se implementa en ninguna de estas interfaces, por lo que se debe llamar al método <xref:System.Data.DataTableExtensions.AsEnumerable%2A> si desea utilizar <xref:System.Data.DataTable> como un origen en la cláusula `From` de una consulta [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)].  
  
 En el ejemplo siguiente se obtienen todos los pedidos en línea desde la tabla SalesOrderHeader y se envían los resultados de id., fecha y número de pedido a la consola.  
  
 [!code-csharp[dp linq to dataset examples#Where1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where1)]
 [!code-vb[dp linq to dataset examples#Where1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where1)]  
  
 La consulta variable local se inicializa con una expresión de consulta, la cual opera en  una o varias fuentes de información aplicando uno o varios operadores de consulta desde el operador estándar de consulta o, en el caso de [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], desde el operador específico de la clase <xref:System.Data.DataSet>.  La expresión de consulta del ejemplo anterior utiliza dos de los operadores estándar de consulta: `Where` y `Select`.  
  
 La cláusula `Where` filtra la secuencia basándose en una condición, en este caso que `OnlineOrderFlag` se establezca en `true`.  El operador `Select` asigna y devuelve un objeto enumerable que captura los argumentos pasados al operador.  En el ejemplo anterior, se crea un tipo anónimo con tres propiedades: `SalesOrderID`, `OrderDate` y `SalesOrderNumber`.  Los valores de estas tres propiedades se establecen en los valores de las columnas `SalesOrderID`, `OrderDate` y `SalesOrderNumber` a partir de la tabla `SalesOrderHeader`.  
  
 A continuación, el bucle `foreach` enumera el objeto enumerable devuelto por `Select` y produce los resultados de la consulta.  Dado que una consulta es un tipo <xref:System.Linq.Enumerable>, que implementa <xref:System.Collections.Generic.IEnumerable%601>, la evaluación de la consulta se difiere hasta que se procesa una iteración en la variable de la consulta mediante el bucle `foreach`.  La evaluación de la consulta en diferido permite que éstas se mantengan como valores que se pueden evaluar varias veces, y cada vez produciendo resultados potencialmente diferentes.  
  
 El método <xref:System.Data.DataRowExtensions.Field%2A> proporciona acceso a los valores de columna de <xref:System.Data.DataRow> y <xref:System.Data.DataRowExtensions.SetField%2A> \(que no se mostraba en el ejemplo anterior\) establece los valores de columna en <xref:System.Data.DataRow>.  Tanto el método <xref:System.Data.DataRowExtensions.Field%2A> como el método <xref:System.Data.DataRowExtensions.SetField%2A> controlan tipos que admiten valores null, por lo que no es necesario comprobar explícitamente si hay valores null.  Además, ambos son métodos genéricos, lo que significa que no es necesario convertir el tipo de valor devuelto.  Puede utilizar el descriptor de acceso de columna preexistente en <xref:System.Data.DataRow> \(por ejemplo, `o["OrderDate"]`\), pero hacerlo le exigiría convertir el objeto de valor devuelto al tipo apropiado.  Si la columna admite valores null, debe comprobar si el valor es null utilizando el método <xref:System.Data.DataRow.IsNull%2A>.  Para obtener más información, consulta [Métodos genéricos Field y SetField](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md).  
  
 Observe que el tipo de datos especificado en el parámetro `T` genérico de los métodos <xref:System.Data.DataRowExtensions.Field%2A> y <xref:System.Data.DataRowExtensions.SetField%2A> deben coincidir con el tipo del valor subyacente; en caso contrario, se producirá una <xref:System.InvalidCastException>.  El nombre de columna especificado debe también coincidir con el nombre de una columna en <xref:System.Data.DataSet>, en caso contrario, se producirá una <xref:System.ArgumentException>.  En ambos casos, la excepción se produce en tiempo de ejecución de enumeración de datos, cuando se ejecuta la consulta.  
  
## Vea también  
 [Consultas entre tablas](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)   
 [Consultar DataSets con establecimiento de tipos](../../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [Métodos genéricos Field y SetField](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md)