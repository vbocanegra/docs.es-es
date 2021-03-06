---
title: "C&#243;mo: Controlar la cantidad de datos relacionados que se recuperan | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efdc203e-3da9-4477-815e-54f10c3d7c6c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# C&#243;mo: Controlar la cantidad de datos relacionados que se recuperan
Utilice el método <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> para especificar qué datos relacionados con el destino principal deben recuperarse al mismo tiempo.  Por ejemplo, si sabe que va a necesitar información sobre los pedidos de los clientes, puede utilizar <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> para asegurarse de que la información de los pedidos se va a recuperar al mismo tiempo que la información de los clientes.  Con este enfoque, sólo se requiere un viaje a la base de datos para ambos conjuntos de información.  
  
> [!NOTE]
>  Puede recuperar datos relacionados con el destino principal de la consulta recuperando un producto cruzado como una gran proyección; por ejemplo, puede recuperar los pedidos cuando el destino de la consulta son los clientes.  Sin embargo, este enfoque a menudo tiene desventajas.  Por ejemplo, los resultados son simples proyecciones, no entidades que se puedan cambiar y conservar mediante [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Además, podría recuperar una gran cantidad de datos que no necesita.  
  
## Ejemplo  
 En el siguiente ejemplo, se recuperan todos los `Orders` de todos los `Customers` de Londres cuando se ejecuta la consulta.  En consecuencia, el acceso posterior a la propiedad `Orders` de un objeto `Customer` no desencadena una nueva consulta de base de datos.  
  
 [!code-csharp[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.dataloadoptions/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.dataloadoptions/vb/module1.vb#2)]  
  
## Vea también  
 [Consultar la base de datos](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)