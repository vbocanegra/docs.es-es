---
title: "Inclusi&#243;n o importaci&#243;n de esquemas XML | Microsoft Docs"
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
ms.assetid: fe1b4a11-37f4-4e1a-93c9-239f4fe736c0
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Inclusi&#243;n o importaci&#243;n de esquemas XML
Un esquema XML puede contener elementos `<xs:import />`, `<xs:include />` y `<xs:redefine />`.  Estos elementos de esquema hacen referencia a otros esquemas XML que se pueden utilizar para complementar la estructura del esquema que los incluye o importa.  Las clases <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> y <xref:System.Xml.Schema.XmlSchemaRedefine> se asignan estos elementos en la API del modelo de objetos de esquema \(SOM\).  
  
## Inclusión o importación de un esquema XML  
 En el siguiente ejemplo de código se complementa el esquema del cliente que se creó en el tema [Compilar esquemas XML](../../../../docs/standard/data/xml/building-xml-schemas.md) con el esquema de direcciones.  Al complementar el esquema del cliente con el esquema de direcciones, los tipos de direcciones están disponibles en el esquema del cliente.  
  
 El esquema de direcciones se puede incorporar utilizando los elementos `<xs:include />` o `<xs:import />` para utilizar los componentes del esquema de direcciones tal y como están, o utilizando un elemento `<xs:redefine />` para modificar cualquiera de sus componentes con el fin de satisfacer la necesidad del esquema del cliente.  Puesto que el esquema de direcciones tiene un `targetNamespace` que es diferente del que tiene el esquema del cliente, se utiliza el elemento `<xs:import />` y, por tanto, la semántica de importación.  
  
 El código de ejemplo incluye el esquema de direcciones en los siguientes pasos.  
  
1.  Agrega el esquema del cliente y el esquema de direcciones a un objeto <xref:System.Xml.Schema.XmlSchemaSet> nuevo y luego los compila.  Cualquier error y advertencia de validación de esquemas que se encuentre durante la lectura o compilación de los esquemas se controla por medio del delegado <xref:System.Xml.Schema.ValidationEventHandler>.  
  
2.  Recupera los objetos <xref:System.Xml.Schema.XmlSchema> compilados para los esquemas del cliente y de direcciones desde <xref:System.Xml.Schema.XmlSchemaSet> iterando por la propiedad <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.  Puesto que los esquemas se compilan, las propiedades del conjunto de información posterior a la compilación del esquema son accesibles.  
  
3.  Crea un objeto <xref:System.Xml.Schema.XmlSchemaImport>, establece la propiedad <xref:System.Xml.Schema.XmlSchemaImport.Namespace%2A> de la importación en el espacio de nombres del esquema de direcciones, establece la propiedad <xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A> de la importación en el objeto <xref:System.Xml.Schema.XmlSchema> del esquema de direcciones y agrega la importación a la propiedad <xref:System.Xml.Schema.XmlSchema.Includes%2A> del esquema del cliente.  
  
4.  Vuelve a procesar y compilar el objeto <xref:System.Xml.Schema.XmlSchema> modificado del esquema del cliente utilizando los métodos <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> y <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> de la clase <xref:System.Xml.Schema.XmlSchemaSet> y lo escribe en la consola.  
  
5.  Por último, escribe de forma recursiva en la consola todos los esquemas importados al esquema del cliente utilizando la propiedad <xref:System.Xml.Schema.XmlSchema.Includes%2A> del esquema del cliente.  La propiedad <xref:System.Xml.Schema.XmlSchema.Includes%2A> proporciona acceso a todas las inclusiones, importaciones o redefiniciones agregadas a un esquema.  
  
 A continuación se ofrece el código de ejemplo completo y los esquemas de direcciones y del cliente escritos en la consola.  
  
 [!code-cpp[XmlSchemaImportExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaImportExample/CPP/XmlSchemaImportExample.cpp#1)]
 [!code-csharp[XmlSchemaImportExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaImportExample/CS/XmlSchemaImportExample.cs#1)]
 [!code-vb[XmlSchemaImportExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaImportExample/VB/XmlSchemaImportExample.vb#1)]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:import namespace="http://www.example.com/IPO" />  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="xs:string" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
      </xs:sequence>  
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /  
>  
    </xs:complexType>  
  </xs:element>  
  <xs:simpleType name="LastNameType">  
    <xs:restriction base="xs:string">  
      <xs:maxLength value="20" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
<schema targetNamespace="http://www.example.com/IPO" xmlns="http://www.w3.org/2001/XMLSchema" xmlns:ipo="http://www.example.com/IPO">  
  <annotation>  
    <documentation xml:lang="en">  
      Addresses for International Purchase order schema  
      Copyright 2000 Example.com. All rights reserved.  
    </documentation>  
  </annotation>  
  <complexType name="Address">  
    <sequence>  
      <element name="name"   type="string"/>  
      <element name="street" type="string"/>  
      <element name="city"   type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="USAddress">  
    <complexContent>  
      <extension base="ipo:Address">  
        <sequence>  
          <element name="state" type="ipo:USState"/>  
          <element name="zip"   type="positiveInteger"/>  
        </sequence>  
      </extension>  
    </complexContent>  
  </complexType>  
  <!-- other Address derivations for more countries or regions -->  
  <simpleType name="USState">  
    <restriction base="string">  
      <enumeration value="AK"/>  
      <enumeration value="AL"/>  
      <enumeration value="AR"/>  
      <!-- and so on ... -->  
    </restriction>  
  </simpleType>  
</schema>  
```  
  
 Para obtener más información sobre los elementos `<xs:import />`, `<xs:include />` y `<xs:redefine />` y sobre las clases <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> y <xref:System.Xml.Schema.XmlSchemaRedefine>, vea el [esquema XML de W3C](http://go.microsoft.com/fwlink/?LinkId=45242) y la documentación de referencia sobre las clases del espacio de nombres <xref:System.Xml.Schema?displayProperty=fullName>.  
  
## Vea también  
 [Información general sobre el Modelo de objetos de esquema XML](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [Lectura y escritura de esquemas XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [Compilar esquemas XML](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [Cómo atravesar esquemas XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [Edición de esquemas XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [XmlSchemaSet para compilación de esquemas](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)