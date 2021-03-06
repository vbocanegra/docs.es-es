---
title: "C&#243;mo: Especificar un nombre de elemento alternativo para una secuencia XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "clases, invalidar"
  - "invalidar clases"
  - "invalidar la serialización XML"
  - "serialización, invalidar"
  - "serialización XML, invalidar"
  - "secuencia XML, especificar un nombre de elemento alternativo"
ms.assetid: 5cc1c0b0-f94b-4525-9a41-88a582cd6668
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# C&#243;mo: Especificar un nombre de elemento alternativo para una secuencia XML
[Ejemplo de código](#cpconoverridingserializationofclasseswithxmlattributeoverridesclassanchor1)  
  
 Utilizando[XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx), se puede generar más de una secuencia XML con el mismo conjunto de clases.Puede que desee proceder de esta forma ya que dos servicios Web XML diferentes requieren la misma información básica, con solo ligeras diferencias.Por ejemplo, imagine dos servicios Web XML que procesan órdenes para los libros y así ambos requieren los números de ISBN.Un servicio utiliza la etiqueta \<ISBN\> mientras el segundo utiliza la etiqueta \<BookID\>.Tiene una clase denominada `Book` que contiene un campo denominado `ISBN`.Cuando se serializa una instancia de la clase `Book`, utilizará, de forma predeterminada, el nombre de miembro \(ISBN\) como el nombre de elemento de etiqueta.Para el primer servicio Web XML, esto es como esperado.Pero para enviar la secuencia XML al segundo servicio Web XML, debe invalidar la serialización para que el nombre de elemento de la etiqueta sea `BookID`.  
  
### Para crear una secuencia XML con un nombre de elemento alternativo  
  
1.  Cree una instancia de la clase [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic).  
  
2.  Establece el <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> de <xref:System.Xml.Serialization.XmlElementAttribute> a "BookID".  
  
3.  Cree una instancia de la clase [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic).  
  
4.  Agregue el objeto **XmlElementAttribute** a la colección a la que ha accedido mediante la propiedad <xref:System.Xml.Serialization.XmlAttributes.XmlElements%2A> de <xref:System.Xml.Serialization.XmlAttributes> .  
  
5.  Cree una instancia de la clase [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic).  
  
6.  Agregue **XmlAttributes** a <xref:System.Xml.Serialization.XmlAttributeOverrides>, pasando el tipo del objeto para invalidarlo y el nombre de miembro invalidado.  
  
7.  Cree una instancia de la clase **XmlSerializer** con **XmlAttributeOverrides**.  
  
8.  Cree una instancia de la clase `Book` y serialice o deserialícela.  
  
## Ejemplo  
  
```vb  
Public Class SerializeOverride()  
    ' Creates an XmlElementAttribute with the alternate name.  
    Dim myElementAttribute As XmlElementAttribute = _  
    New XmlElementAttribute()  
    myElementAttribute.ElementName = "BookID"  
    Dim myAttributes As XmlAttributes = New XmlAttributes()  
    myAttributes.XmlElements.Add(myElementAttribute)  
    Dim myOverrides As XmlAttributeOverrides = New XmlAttributeOverrides()  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes)  
    Dim mySerializer As XmlSerializer = _  
    New XmlSerializer(GetType(Book), myOverrides)  
    Dim b As Book = New Book()  
    b.ISBN = "123456789"  
    ' Creates a StreamWriter to write the XML stream to.  
    Dim writer As StreamWriter = New StreamWriter("Book.xml")  
    mySerializer.Serialize(writer, b);  
End Class  
  
```  
  
```csharp  
public class SerializeOverride()  
{  
    // Creates an XmlElementAttribute with the alternate name.  
    XmlElementAttribute myElementAttribute = new XmlElementAttribute();  
    myElementAttribute.ElementName = "BookID";  
    XmlAttributes myAttributes = new XmlAttributes();  
    myAttributes.XmlElements.Add(myElementAttribute);  
    XmlAttributeOverrides myOverrides = new XmlAttributeOverrides();  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes);  
    XmlSerializer mySerializer =   
    new XmlSerializer(typeof(Book), myOverrides)  
    Book b = new Book();  
    b.ISBN = "123456789"  
    // Creates a StreamWriter to write the XML stream to.  
    StreamWriter writer = new StreamWriter("Book.xml");  
    mySerializer.Serialize(writer, b);  
}  
```  
  
 La secuencia XML puede parecerse a lo siguiente.  
  
```  
<Book>  
    <BookID>123456789</BookID>  
</Book>  
```  
  
## Vea también  
 [Serialización de SOAP y XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic)   
 [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic)   
 [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic)   
 [Cómo: Serializar un objeto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Cómo: Deserializar un objeto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)   
 [Cómo: Deserializar un objeto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)