---
title: "Asignaci&#243;n del modelo de objetos de distribuci&#243;n de WCF a Atom y RSS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0365eb37-98cc-4b13-80fb-f1e78847a748
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Asignaci&#243;n del modelo de objetos de distribuci&#243;n de WCF a Atom y RSS
Al desarrollar un servicio de distribución de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], se crean fuentes y elementos mediante las siguientes clases:  
  
-   <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
-   <xref:System.ServiceModel.Syndication.TextSyndicationContent>  
  
-   <xref:System.ServiceModel.Syndication.UrlSyndicationContent>  
  
-   <xref:System.ServiceModel.Syndication.XmlSyndicationContent>  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> se puede serializar en cualquier formato para redifusión web para el que está definido un formateador.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se distribuye con dos formateadores: <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> y <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>.  
  
 El modelo de objetos alrededor de <xref:System.ServiceModel.Syndication.SyndicationFeed> y <xref:System.ServiceModel.Syndication.SyndicationItem> está alineado más estrechamente con la especificación Atom 1.0 que con la especificación RSS 2.0.Esto se debe a que Atom 1.0 es una especificación más sustancial que define elementos que son ambiguos o que se han omitido de la especificación RSS 2.0.Debido a esto, muchos elementos en el modelo de objetos de distribución de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] no tienen ninguna representación directa en la especificación RSS 2.0.Al serializar los objetos <xref:System.ServiceModel.Syndication.SyndicationFeed> y <xref:System.ServiceModel.Syndication.SyndicationItem> en RSS 2.0, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le permite serializar elementos de datos específicos de Atom como elementos de extensión de espacios de nombres completos que cumplen la especificación Atom.Esto se puede controlar mediante un parámetro pasado al constructor <xref:System.ServiceModel.Syndication.Rss20FeedFormatter>.  
  
 Los ejemplos de código de este tema usan uno de los dos métodos definidos aquí para realizar la serialización real.  
  
 `SerializeFeed` serializa una fuente de distribución.  
  
 [!code-csharp[SyndicationMapping#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#10)]
 [!code-vb[SyndicationMapping#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#10)]  
  
 `SerializeItem` serializa un elemento de distribución.  
  
 [!code-csharp[SyndicationMapping#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#11)]
 [!code-vb[SyndicationMapping#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#11)]  
  
## SyndicationFeed  
 El siguiente ejemplo de código muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.SyndicationFeed> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#0)]
 [!code-vb[SyndicationMapping#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#0)]  
  
 El siguiente XML muestra cómo se serializa la fuente <xref:System.ServiceModel.Syndication.SyndicationFeed> en Atom 1.0.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<feed xml:lang="EN-US" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">My Feed Title</title>  
  <subtitle type="text">My Feed Description</subtitle>  
  <id>FeedID</id>  
  <rights type="text">Copyright 2007</rights>  
  <updated>2007-08-29T13:57:17-07:00</updated>  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <logo>http://server/image.jpg</logo>  
  <generator>Sample Code</generator>  
  <link rel="alternate" href="http://myfeeduri/" />  
  <entry>  
    <id>ItemID</id>  
    <title type="text">Item Title</title>  
    <summary type="text">Item Summary</summary>  
    <published>2007-08-29T00:00:00-07:00</published>  
    <updated>2007-08-29T13:57:17-07:00</updated>  
    <author>  
      <name>Jesper Aaberg</name>  
      <uri>http://Jesper/Aaberg</uri>  
      <email>Jesper@Aaberg.com</email>  
    </author>  
    <contributor>  
      <name>Lene Aaling</name>  
      <uri>http://Lene/Aaling</uri>  
      <email>Lene@Aaling.com</email>  
    </contributor>  
    <link rel="alternate" href="http://myitemuri/" />  
    <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
    <content type="text">Item Content</content>  
    <rights type="text">Copyright 2007</rights>  
    <source>  
      <title type="text">My Feed Title</title>  
      <subtitle type="text">My Feed Description</subtitle>  
      <id>FeedID</id>  
      <rights type="text">Copyright 2007</rights>  
      <updated>2007-08-29T13:57:17-07:00</updated>  
      <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
      <logo>http://server/image.jpg</logo>  
      <generator>Sample Code</generator>  
      <link rel="alternate" href="http://myfeeduri/" />  
    </source>  
  </entry>  
</feed>  
```  
  
 El siguiente XML muestra cómo la <xref:System.ServiceModel.Syndication.SyndicationFeed> se serializa a RSS 2.0.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<rss xmlns:a10="http://www.w3.org/2005/Atom" version="2.0">  
  <channel>  
    <title>My Feed Title</title>  
    <link>http://myfeeduri/</link>  
    <description>My Feed Description</description>  
    <language>EN-US</language>  
    <copyright>Copyright 2007</copyright>  
    <lastBuildDate>Wed, 29 Aug 2007 13:57:17 -0700</lastBuildDate>  
    <category domain="categoryScheme">categoryName</category>  
    <generator>Sample Code</generator>  
    <image>  
      <url>http://server/image.jpg</url>  
      <title>My Feed Title</title>  
      <link>http://myfeeduri/</link>  
    </image>  
    <a10:id>FeedID</a10:id>  
    <item>  
      <guid isPermaLink="false">ItemID</guid>  
      <link>http://myitemuri/</link>  
      <author>Jesper@Aaberg.com</author>  
      <category domain="categoryScheme">categoryName</category>  
      <title>Item Title</title>  
      <description>Item Summary</description>  
      <source>My Feed Title</source>  
      <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
      <a10:updated>2007-08-29T13:57:17-07:00</a10:updated>  
      <a10:rights type="text">Copyright 2007</a10:rights>  
      <a10:content type="text">Item Content</a10:content>  
      <a10:contributor>  
        <a10:name>Lene Aaling</a10:name>  
        <a10:uri>http://Lene/Aaling</a10:uri>  
        <a10:email>Lene@Aaling.com</a10:email>  
      </a10:contributor>  
    </item>  
  </channel>  
</rss>  
```  
  
## SyndicationItem  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.SyndicationItem> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#1)]
 [!code-vb[SyndicationMapping#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#1)]  
  
 El siguiente fragmento XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationItem> a Atom 1.0.  
  
```  
<entry xmlns="http://www.w3.org/2005/Atom">  
  <id>ItemID</id>  
  <title type="text">Item Title</title>  
  <summary type="text">Item Summary</summary>  
  <published>2007-08-29T00:00:00-07:00</published>  
  <updated>2007-08-29T14:07:09-07:00</updated>  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
  <author>  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor>  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
  <link rel="alternate" href="http://myitemuri/" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <content type="text">Item Content</content>  
  <rights type="text">Copyright 2007</rights>  
  <source>  
    <title type="text">My Feed Title</title>  
    <subtitle type="text">My Feed Description</subtitle>  
    <link rel="alternate" href="http://myfeeduri/" />  
  </source>  
</entry>  
```  
  
 El siguiente fragmento XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationItem> a RSS 2.0.  
  
```  
<item>  
  <guid isPermaLink="false">ItemID</guid>  
  <link>http://myitemuri/</link>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Jesper Aaberg</name>  
    <uri>http://Jesper/Aaberg</uri>  
    <email>Jesper@Aaberg.com</email>  
  </author>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <category domain="categoryScheme">categoryName</category>  
  <category domain="categoryScheme">categoryName</category>  
  <title>Item Title</title>  
  <description>Item Summary</description>  
  <source>My Feed Title</source>  
  <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
  <updated xmlns="http://www.w3.org/2005/Atom">2007-08-29T14:07:09-07:00</updated>  
  <rights type="text" xmlns="http://www.w3.org/2005/Atom">Copyright 2007</rights>  
  <content type="text" xmlns="http://www.w3.org/2005/Atom">Item Content</content>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
</item>  
```  
  
## SyndicationPerson  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.SyndicationPerson> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#2)]
 [!code-vb[SyndicationMapping#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#2)]  
  
 El siguiente fragmento XML muestra cómo <xref:System.ServiceModel.Syndication.SyndicationPerson> se serializa a Atom 1.0.  
  
```  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
<contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
```  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.SyndicationPerson> a RSS 2.0 si solo existe una <xref:System.ServiceModel.Syndication.SyndicationPerson> en las colecciones `Authors` o `Contributors`, respectivamente.  
  
```  
<author>Jesper.Aaberg@contoso.com</author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
```  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.SyndicationPerson> a RSS 2.0 si existe más de una <xref:System.ServiceModel.Syndication.SyndicationPerson> en las colecciones `Authors` o `Contributors`, respectivamente.  
  
```  
<a10:author>  
    <a10:name>Jesper Aaberg</a10:name>  
    <a10:uri>http://Contoso/Aaberg</a10:uri>  
    <a10:email>Jesper.Aaberg@contoso.com</a10:email>  
</a10:author>  
<a10:author>  
    <a10:name>Syed Abbas</a10:name>  
    <a10:uri>http://Contoso/Abbas</a10:uri>  
    <a10:email>Syed.Abbas@contoso.com</a10:email>  
</a10:author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
<a10:contributor>  
    <a10:name>Kim Abercrombie</a10:name>  
    <a10:uri>http://Contoso/Abercrombie</a10:uri>  
    <a10:email>Kim.Abercrombie@contoso.com</a10:email>  
</a10:contributor>  
```  
  
## SyndicationLink  
 El siguiente ejemplo de código muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.SyndicationLink> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#3)]
 [!code-vb[SyndicationMapping#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#3)]  
  
 El siguiente XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationLink> a Atom 1.0.  
  
 `<link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
 El siguiente XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationLink>a RSS 2.0.  
  
 `<a10:link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
## SyndicationCategory  
 El siguiente ejemplo de código muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.SyndicationCategory> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#4)]
 [!code-vb[SyndicationMapping#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#4)]  
  
 El siguiente XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationCategory> a Atom 1.0.  
  
 `<category term="categoryName" label="categoryLabel" scheme="categoryScheme" />`  
  
 El siguiente XML muestra cómo se serializa <xref:System.ServiceModel.Syndication.SyndicationCategory> a RSS 2.0.  
  
 `<category domain="categoryScheme">categoryName</category>`  
  
## TextSyndicationContent  
 El siguiente ejemplo de código muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> a Atom 1.0 y RSS 2.0 cuando <xref:System.ServiceModel.Syndication.TextSyndicationContent> se crea con contenido HTML.  
  
 [!code-csharp[SyndicationMapping#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#5)]
 [!code-vb[SyndicationMapping#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#5)]  
  
 El siguiente XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de HTML a Atom 1.0.  
  
 `<content type="html"><html> some html </html></content>`  
  
 El siguiente XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de HTML a RSS 2.0.  
  
 `<description><html> some html </html></description>`  
  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> a Atom 1.0 y RSS 2.0 cuando se crea <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de texto sin formato.  
  
 [!code-csharp[SyndicationMapping#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#6)]
 [!code-vb[SyndicationMapping#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#6)]  
  
 El siguiente XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de texto sin formato a Atom 1.0.  
  
 `<content type="text">Some Plain Text</content>`  
  
 El siguiente XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de texto sin formato a RSS 2.0.  
  
 `<description>Some Plain Text</description>`  
  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> a Atom 1.0 y RSS 2.0 cuando se crea <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido XHTML.  
  
 [!code-csharp[SyndicationMapping#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#7)]
 [!code-vb[SyndicationMapping#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#7)]  
  
 El siguiente XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido de XHTML a Atom 1.0.  
  
 `<content type="xhtml">`  
  
 `<html> some xhtml </html>`  
  
 `</content>`  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.TextSyndicationContent> con contenido XHTML a RSS 2.0.  
  
 `<description><html> some xhtml </html></description>`  
  
## UrlSyndicationContent  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.UrlSyndicationContent> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#8)]
 [!code-vb[SyndicationMapping#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#8)]  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.UrlSyndicationContent> a Atom 1.0.  
  
 `<content type="audio" src="http://someurl/" />`  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.UrlSyndicationContent> con contenido XHTML a RSS 2.0.  
  
 `<description />`  
  
 `<content type="audio" src="http://Contoso/someurl/" xmlns="http://www.w3.org/2005/Atom" />`  
  
## XmlSyndicationContent  
 El siguiente código de ejemplo muestra cómo serializar la clase <xref:System.ServiceModel.Syndication.XmlSyndicationContent> a Atom 1.0 y RSS 2.0.  
  
 [!code-csharp[SyndicationMapping#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#9)]
 [!code-vb[SyndicationMapping#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#9)]  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.XmlSyndicationContent> a Atom 1.0.  
  
 `<content type="mytype">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
 El siguiente fragmento XML muestra cómo se serializa la clase <xref:System.ServiceModel.Syndication.XmlSyndicationContent> con contenido XHTML a RSS 2.0.  
  
 `<content type="mytype" xmlns="http://www.w3.org/2005/Atom">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
## Vea también  
 [Información general de distribución de WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)   
 [Arquitectura de distribución](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)   
 [Creación de una fuente RSS básica](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-rss-feed.md)   
 [Creación de una fuente básica de Atom](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-atom-feed.md)   
 [Cómo: Exponer una fuente como Atom y RSS](../../../../docs/framework/wcf/feature-details/how-to-expose-a-feed-as-both-atom-and-rss.md)