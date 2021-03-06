---
title: "C&#243;mo: Llamar a funciones de base de datos personalizadas | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4354e5eb-dd45-469d-97fb-1c495705ee59
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# C&#243;mo: Llamar a funciones de base de datos personalizadas
En este tema se describe cómo llamar a las funciones personalizadas definidas en la base de datos desde consultas LINQ to Entities.  
  
 Las funciones de base de datos llamadas desde LINQ to Entities se ejecutan en la base de datos.  La ejecución de funciones en la base de datos puede mejorar el rendimiento de la aplicación.  
  
 El procedimiento siguiente proporciona un esquema general para llamar a una función de base de datos personalizada.  El ejemplo que sigue proporciona más detalles sobre los pasos del procedimiento.  
  
### Para llamar a funciones personalizadas definidas en la base de datos  
  
1.  Cree una función personalizada en la base de datos.  
  
     Para obtener más información sobre cómo crear funciones personalizadas en SQL Server, vea [CREATE FUNCTION \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=139871).  
  
2.  Declare una función en el lenguaje de definición de esquemas de almacenamiento \(SSDL\) del archivo .edmx.  El nombre de la función debe coincidir con el nombre de la función declarada en la base de datos.  
  
     Para obtener más información, consulta [Function Element \(SSDL\)](http://msdn.microsoft.com/es-es/b60cfc3d-8b93-423e-8c99-b867256640a4).  
  
3.  Agregue un método correspondiente a una clase del código de la aplicación y aplique un atributo <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> al método. Tenga en cuenta que los parámetros <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> y <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> de dicho atributo son el nombre del espacio de nombres del modelo conceptual y el nombre de la función en el modelo conceptual, respectivamente.  La resolución del nombre de la función para LINQ distingue entre mayúsculas y minúsculas.  
  
4.  Llame al método en una consulta LINQ to Entities.  
  
## Ejemplo  
 En el ejemplo siguiente se muestra cómo llamar a una función de base de datos personalizada desde una consulta LINQ to Entities.  En el ejemplo se usa el modelo School.  Para obtener información sobre el modelo School, vea [Creating the School Sample Database](http://msdn.microsoft.com/es-es/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0) y [Generating the School .edmx File](http://msdn.microsoft.com/es-es/c48b3907-a8be-4fe6-884c-e95af1852758).  
  
 El código siguiente agrega la función `AvgStudentGrade` a la base de datos de ejemplo School.  
  
> [!NOTE]
>  Los pasos para llamar a una función de base de datos personalizada son los mismos, independientemente del servidor de bases de datos.  Sin embargo, el código siguiente es específico para crear una función en una base de datos de SQL Server.  El código para crear una función personalizada en otros servidores de bases de datos puede variar.  
  
 [!code-sql[DP L2E MapToDBFunction#1](../../../../../../samples/snippets/tsql/VS_Snippets_Data/dp l2e maptodbfunction/tsql/create_avgstudentgrade.sql#1)]  
  
## Ejemplo  
 A continuación, declare una función en el lenguaje de definición de esquemas de almacenamiento \(SSDL\) del archivo .edmx.  El código siguiente declara la función `AvgStudentGrade` en SSDL:  
  
 [!code-xml[DP L2E MapToDBFunction#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/school.edmx#2)]  
  
## Ejemplo  
 Ahora cree un método y asígneselo a la función declarada en SSDL.  El método de la clase siguiente se asigna a dicha función usando un atributo <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>.  Cuando se llama a este método, se ejecuta la función correspondiente en la base de datos.  
  
 [!code-csharp[DP L2E MapToDBFunction#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#3)]
 [!code-vb[DP L2E MapToDBFunction#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#3)]  
  
## Ejemplo  
 Por último, llame al método en una consulta LINQ to Entities.  El código siguiente muestra en la consola los apellidos de los alumnos y sus notas medias:  
  
 [!code-csharp[DP L2E MapToDBFunction#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#4)]
 [!code-vb[DP L2E MapToDBFunction#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#4)]  
  
## Vea también  
 [.edmx File Overview](http://msdn.microsoft.com/es-es/f4c8e7ce-1db6-417e-9759-15f8b55155d4)   
 [Consultas en LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)