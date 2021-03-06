---
title: "C&#243;mo quitar atributos de un nodo de elementos en el DOM | Microsoft Docs"
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
ms.assetid: 7ede6f9e-a3ac-49a4-8488-ab8360a44aa4
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# C&#243;mo quitar atributos de un nodo de elementos en el DOM
Existen muchas formas de quitar atributos.  Una de estas técnicas consiste en quitarlos de la colección de atributos.  Para ello, hay que realizar los siguientes pasos:  
  
1.  Obtenga la colección de atributos del elemento utilizando `XmlAttributeCollection attrs = elem.Attributes;`.  
  
2.  Quite el atributo de la colección de atributos utilizando uno de estos tres métodos:  
  
    -   Utilice <xref:System.Xml.XmlAttributeCollection.Remove%2A> para quitar un atributo específico.  
  
    -   Utilice <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A> para quitar todos los atributos de la colección y deje el elemento sin atributos.  
  
    -   Utilice <xref:System.Xml.XmlAttributeCollection.RemoveAt%2A> para quitar un atributo de la colección de atributos utilizando su número de índice.  
  
 Los siguientes métodos sirven para quitar atributos del nodo de elementos.  
  
-   Utilice <xref:System.Xml.XmlElement.RemoveAllAttributes%2A> para quitar la colección de atributos.  
  
-   Utilice <xref:System.Xml.XmlElement.RemoveAttribute%2A> para quitar un solo atributo por el nombre de la colección.  
  
-   Utilice <xref:System.Xml.XmlElement.RemoveAttributeAt%2A> para quitar un solo atributo por el número de índice de la colección.  
  
 Otra alternativa es obtener el elemento, obtener el atributo de la colección de atributos y quitar directamente el nodo de atributos.  Para obtener el atributo de la colección de atributos, puede utilizar un nombre, `XmlAttribute attr = attrs["attr_name"];`, un índice `XmlAttribute attr = attrs[0];` o certificar por completo el nombre con el espacio de nombres `XmlAttribute attr = attrs["attr_localName", "attr_namespace"]`.  
  
 Con independencia del método que se utilice para quitar atributos, existen unas limitaciones especiales para quitar atributos que se hayan definido como predeterminados en la definición de tipo de documento \(DTD\).  Los atributos predeterminados no se pueden quitar a menos que se quite el elemento al que pertenecen.  Siempre hay atributos predeterminados para los elementos que los tengan declarados.  Al quitar un atributo predeterminado de <xref:System.Xml.XmlAttributeCollection> o de <xref:System.Xml.XmlElement>, se inserta un atributo que lo reemplaza en el <xref:System.Xml.XmlAttributeCollection> del elemento, que se inicializa con el valor predeterminado que se ha declarado.  Si ha definido un elemento como `<book att1="1" att2="2" att3="3"></book>`, tendrá un elemento `book` con tres atributos predeterminados declarados.  La implementación del Modelo de objetos de documento \(DOM\) XML garantiza que, siempre y cuando exista este elemento `book` , tendrá tres atributos predeterminados de `att1`, `att2` y `att3`.  
  
 Al llamarlo con un <xref:System.Xml.XmlAttribute>, el método <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A> establece el valor del atributo en String.Empty, ya que no puede haber un atributo sin un valor.  
  
## Vea también  
 [Modelo de objetos de documento XML \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)