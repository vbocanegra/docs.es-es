---
title: "Utilizar XML en un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Utilizar XML en un DataSet
Con ADO.NET es posible llenar un <xref:System.Data.DataSet> a partir de una secuencia o un documento XML.  Se puede utilizar la secuencia o el documento XML para suministrar datos al <xref:System.Data.DataSet>, información de esquema o ambas cosas.  La información suministrada desde la secuencia o el documento XML puede combinarse con datos o información de esquema existente ya presente en el <xref:System.Data.DataSet>.  
  
 ADO.NET también permite crear una representación XML de un <xref:System.Data.DataSet>, con o sin su esquema, para transportar el <xref:System.Data.DataSet> a través de HTTP con el fin de que lo utilice otra aplicación u otra plataforma compatible con XML.  En una representación XML de un <xref:System.Data.DataSet>, los datos se escriben en XML y el esquema, si está incluido alineado en la representación, se escribe utilizando el lenguaje de definición de esquemas XML \(XSD\).  XML y el esquema XML proporcionan un formato cómodo para transferir el contenido de un <xref:System.Data.DataSet> a y desde clientes remotos.  
  
## En esta sección  
 [DiffGrams](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)  
 Proporciona detalles acerca de DiffGram, un formato XML utilizado para leer y escribir el contenido de un <xref:System.Data.DataSet>.  
  
 [Cargar DataSet desde XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)  
 Describe las distintas opciones que hay que tener en cuenta al cargar el contenido de un <xref:System.Data.DataSet> desde un documento XML.  
  
 [Escribir contenido de DataSet como datos XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)  
 Describe cómo generar el contenido de un <xref:System.Data.DataSet> como datos XML y las distintas opciones de formato XML que se pueden utilizar.  
  
 [Cargar la información de esquema de DataSet desde XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)  
 Describe los métodos <xref:System.Data.DataSet> utilizados para cargar el esquema de un <xref:System.Data.DataSet> desde XML.  
  
 [Escribir la información de esquema de DataSet como XSD](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)  
 Describe los usos de un esquema XML y cómo generar uno a partir de un <xref:System.Data.DataSet>.  
  
 [Sincronización de DataSet y XmlDataDocument](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)  
 Describe la posibilidad existente en .NET Framework de tener acceso sincrónicamente a las vistas relacional y jerárquica de un único conjunto de datos, a la vez que muestra cómo crear una relación sincrónica entre un <xref:System.Data.DataSet> y un <xref:System.Xml.XmlDataDocument>.  
  
 [Anidar DataRelations](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 Explica la importancia de los objetos <xref:System.Data.DataRelation> anidados al representar el contenido de un <xref:System.Data.DataSet> como datos XML y describe cómo crearlos.  
  
 [Derivar la estructura relacional de DataSet desde la definición de esquema XML \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Describe la estructura relacional, o esquema, de un <xref:System.Data.DataSet> creado a partir de un esquema XML.  
  
 [Deducir la estructura relacional de DataSet de XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)  
 Describe la estructura relacional, o esquema, resultante de un <xref:System.Data.DataSet> que se crea por inferencia a partir de elementos XML.  
  
## Secciones relacionadas  
 [Información general sobre ADO.NET](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 Describe la arquitectura y los componentes de ADO.NET, así como su uso para tener acceso a orígenes de datos existentes y administrar los datos de aplicación.  
  
## Vea también  
 [DataSets, DataTables y DataViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)