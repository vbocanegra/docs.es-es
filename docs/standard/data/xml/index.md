---
title: "Documentos y datos XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Documentos y datos XML
.NET Framework proporciona un conjunto de clases completo e integrado que permiten crear, de forma sencilla, aplicaciones preparadas para XML.  Las clases de los espacios de nombres siguientes admiten análisis y escritura XML, edición de datos XML en memoria, validación de datos y transformación XSLT.  
  
-   <xref:System.Xml>  
  
-   <xref:System.Xml.XPath>  
  
-   <xref:System.Xml.Xsl>  
  
-   <xref:System.Xml.Schema>  
  
-   <xref:System.Xml.Linq>  
  
 Para obtener una lista completa, vea la página web de [espacios de nombres System.Xml](http://msdn.microsoft.com/library/gg145036.aspx).  
  
 Las clases de estos espacios de nombres admiten las recomendaciones del World Wide Web Consortium \(W3C\).  Por ejemplo:  
  
-   La clase <xref:System.Xml.XmlDocument?displayProperty=fullName> implementa las recomendaciones del [nivel 1 principal del Modelo de objetos de documento \(DOM\)](http://www.w3.org/TR/REC-DOM-Level-1/) y del [nivel 2 principal de DOM](http://www.w3.org/TR/DOM-Level-2-Core/).  
  
-   Las clases <xref:System.Xml.XmlReader?displayProperty=fullName> y <xref:System.Xml.XmlWriter?displayProperty=fullName> son compatibles con [W3C XML 1.0](http://www.w3.org/TR/2006/REC-xml-20060816/) y los [espacios de nombres XML](http://www.w3.org/TR/REC-xml-names/).  
  
-   Los esquemas de la clase <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=fullName> son compatibles con el [esquema XML de W3C XML, parte 1: estructuras](http://www.w3.org/TR/xmlschema-1/) y el [esquema XML, parte 2: tipos de datos](http://www.w3.org/TR/xmlschema-2/).  
  
-   Las clases del espacio de nombres <xref:System.Xml.Xsl?displayProperty=fullName> admiten transformaciones XSLT que sean compatibles con las recomendaciones de [W3C XSLT 1.0](http://www.w3.org/TR/xslt).  
  
 Las clases XML de .NET Framework proporcionan estas ventajas:  
  
-   **Productividad.** Gracias a [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) resulta más sencillo programar con XML y proporciona una experiencia de consulta similar a SQL.  
  
-   **Extensibilidad.**Las clases XML en .NET Framework se pueden ampliar mediante el uso de clases base abstractas y métodos virtuales.  Por ejemplo, puede crear una clase derivada de la clase <xref:System.Xml.XmlUrlResolver> que almacene el flujo caché en el disco local.  
  
-   **Arquitectura conectable.** .NET Framework proporciona una arquitectura en la que los componentes se pueden usar unos con otros y se puede hacer streaming de los datos entre componentes.  Por ejemplo, un almacén de datos, como un objeto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument>, se puede transformar con la clase <xref:System.Xml.Xsl.XslCompiledTransform> y, posteriormente, se pueden hacer streaming de los resultados a otro almacén o devolverse como flujo desde un servicio web.  
  
-   **Rendimiento.** Para obtener un mejor rendimiento de la aplicación, algunas de las clases XML de .NET Framework admiten un modelo basado en streaming con las características siguientes:  
  
    -   Almacenamiento en caché mínimo para el análisis de modelos de extracción solo hacia delante \(<xref:System.Xml.XmlReader>\).  
  
    -   Validación solo hacia delante con \(<xref:System.Xml.XmlReader>\).  
  
    -   Navegación al estilo de cursores que reduce la creación de nodos a un único nodo virtual, a la vez que proporciona acceso aleatorio al documento \(<xref:System.Xml.XPath.XPathNavigator>\).  
  
     Para obtener un mejor rendimiento cuando se requiera un procesamiento XSLT, puede usar la clase <xref:System.Xml.XPath.XPathDocument>, que es un almacén optimizado de solo lectura para consultas XPath diseñadas para funcionar, de forma eficiente, con la clase <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   **Integración con ADO.NET.** Las clases XML y [ADO.NET](../../../../docs/framework/data/adonet/index.md) están estrechamente integradas para reunir datos relacionales y XML.  La clase <xref:System.Data.DataSet> es una caché almacenada en memoria de datos devueltos desde una base de datos.  La clase <xref:System.Data.DataSet> puede leer y escribir XML mediante las clases <xref:System.Xml.XmlReader> y <xref:System.Xml.XmlWriter>, con el fin de almacenar su estructura de esquema relacional interna como esquemas XML \(XSD\) y para deducir la estructura de esquema de un documento XML.  
  
## En esta sección  
 [Opciones de procesamiento XML](../../../../docs/standard/data/xml/xml-processing-options.md)  
 Trata sobre las opciones disponibles para procesar datos XML.  
  
 [Procesamiento de datos XML en memoria](../../../../docs/standard/data/xml/processing-xml-data-in-memory.md)  
 Trata acerca de los tres modelos para procesar datos XML en memoria.  [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md), la clase <xref:System.Xml.XmlDocument> \(basada en el Modelo de objetos de documento del W3C\) y la clase <xref:System.Xml.XPath.XPathDocument> \(basada en el modelo de datos XPath\).  
  
 [Transformaciones XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)  
 Describe cómo utilizar el procesador XSLT.  
  
 [Modelo de objetos de esquema XML \(SOM\)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)  
 Describe las clases que se usan para crear y tratar esquemas XML \(XSD\) mediante una clase <xref:System.Xml.Schema.XmlSchema> que carga y modifica un esquema.  
  
 [Integración de XML con datos relacionales y ADO.NET](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)  
 Describe cómo habilita .NET Framework el acceso sincrónico en tiempo real a las representaciones relacional y jerárquica de los datos mediante los objetos <xref:System.Data.DataSet> y <xref:System.Xml.XmlDataDocument>.  
  
 [Administrar espacios de nombres en un documento XML](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)  
 Describe cómo se usa la clase <xref:System.Xml.XmlNamespaceManager> para almacenar y mantener la información sobre espacios de nombres.  
  
 [Compatibilidad de tipos en las clases System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)  
 Describe cómo se asignan los tipos de datos XML a los tipos CLR, cómo se convierten los tipos de datos XML y otras características de compatibilidad de tipos de las clases <xref:System.Xml>.  
  
## Secciones relacionadas  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 Proporciona información sobre cómo acceder a los datos mediante ADO.NET.  
  
 [Security](../../../../docs/standard/security/index.md)  
 Ofrece información general sobre todo el sistema de seguridad de .NET Framework.  
  
 [Centro para desarrolladores de XML](http://go.microsoft.com/fwlink/?linkid=42458)  
 Proporciona información técnica adicional, descargas, grupos de noticias y otros recursos para desarrolladores de XML.