---
title: "Enlaces de Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "enlaces [WCF]"
  - "WCF [WCF], enlaces"
  - "Windows Communication Foundation [WCF], enlaces"
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Enlaces de Windows Communication Foundation
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] separa cómo se escribe el software para una aplicación de cómo se comunica con otro software.Los enlaces se usan para especificar el transporte, la codificación y los detalles de protocolo necesarios para que los clientes y los servicios se comuniquen entre sí.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa enlaces para generar la representación subyacente de conexión del extremo, por lo que la mayoría de los detalles de enlace se deben acordar entre las partes que están en comunicación.La manera más sencilla de lograrlo es que los clientes de un servicio usen el mismo enlace que emplea el extremo para el servicio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] cómo hacerlo, consulte [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/es-es/bd8b277b-932f-472f-a42a-b02bb5257dfb).  
  
 Un enlace se compone de una colección de elementos de enlace.Cada elemento describe algún aspecto de cómo el extremo se comunica con los clientes.Un enlace debe incluir por lo menos un elemento de enlace del transporte, por lo menos un elemento de enlace de la codificación de mensajes \(que el elemento de enlace del transporte puede proporcionar de forma predeterminada\), y cualquier número de otros elementos de enlace de protocolo.El proceso que compila un tiempo de ejecución a partir de esta descripción permite a cada elemento de enlace contribuir en el código a ese tiempo de ejecución.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] proporciona enlaces que contienen selecciones comunes de elementos de enlace.Éstos se pueden utilizar con su configuración predeterminada o puede modificar esos valores predeterminados según los requisitos del usuario.Estos enlaces proporcionados por el sistema tienen propiedades que permiten el control directo sobre los elementos de enlace y sus valores.También puede trabajar fácilmente y en paralelo con varias versiones de un enlace dando a cada versión del enlace un nombre propio.Para obtener información detallada, consulte [Configuración de enlaces proporcionados por el sistema](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md).  
  
 Si necesita una colección de elementos de enlace no proporcionada por uno de estos enlaces proporcionados por el sistema, puede crear un enlace personalizado que esté compuesto de la colección de elementos de enlace requeridos.Estos enlaces personalizados son fáciles de crear y no requieren una nueva clase, pero no proporcionan las propiedades para controlar los elementos de enlace o sus valores.Puede obtener acceso a los elementos de enlace y modificar sus valores a través de la colección que los contiene.Para obtener información detallada, consulte [Enlaces personalizados](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## En esta sección  
 [Configuración de enlaces proporcionados por el sistema](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 Describe cómo utilizar y modificar los enlaces que [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] proporciona para admitir los escenarios comunes.  
  
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/es-es/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 Describe cómo definir los enlaces [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] para los servicios y clientes de forma imperativa en código y de forma declarativa utilizando la configuración.  
  
 [Enlaces personalizados](../../../../docs/framework/wcf/extending/custom-bindings.md)  
 Describe qué es <xref:System.ServiceModel.Channels.CustomBinding> y cuándo se utiliza.  
  
## Referencia  
 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## Secciones relacionadas  
 [Extensión de enlaces](../../../../docs/framework/wcf/extending/extending-bindings.md)