---
title: "Esquema de configuraci&#243;n de WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: c282aeb5-91f0-4522-8e2f-704c1ef3651f
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Esquema de configuraci&#243;n de WCF
Los elementos de configuración de [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] le permiten configurar el servicio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] y aplicaciones cliente.  Puede usar el [Herramienta del editor de configuración \(SvcConfigEditor.exe\)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) para crear y modificar los archivos de configuración para clientes y servicios.  Puesto que los archivos de certificado tiene el formato como XML, debe familiarizarse con XML si desea modificarlos manualmente con un editor de texto.  De lo contrario, puede encontrarse con problemas como no encontrar un atributo o una etiqueta de elemento XML.  Esto se debe a que los atributos y las etiquetas del elemento XML distinguen entre mayúsculas y minúsculas.  
  
 El sistema de configuración de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] se basa en el espacio de nombres <xref:System.Configuration>.  Por consiguiente, puede usar todas las características estándar proporcionadas por el espacio de nombres <xref:System.Configuration>, como el bloqueo de configuración, el cifrado y la combinación para aumentar la seguridad de su aplicación y su configuración.  Para obtener más información acerca del uso de estos conceptos, consulte los temas siguientes.  
  
 [Cifrar información de configuración mediante una configuración protegida](http://go.microsoft.com/fwlink/?LinkId=95337)  
  
 [Bloquear opciones de configuración](http://go.microsoft.com/fwlink/?LinkId=95338)  
  
 En esta sección se describen todos los valores posibles de cada elemento de configuración y cómo interactúa con otros elementos de configuración de WCF.  El siguiente mapa muestra el esquema de configuración de WCF.  
  
 ![Esquema de configuración de WCF](../../../../../docs/framework/configure-apps/file-schema/wcf/media/orcasconfigschema.gif "OrcasConfigSchema")  
  
> [!CAUTION]
>  Debería proteger las secciones de configuración de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] en sus archivos de configuración de la aplicación \(app.config\) con listas de control de acceso \(ACL\) adecuadas para evitar cualquier posible amenaza a la seguridad.  Por ejemplo, debería asegurarse de que sólo las personas adecuadas pueden tener acceso o modificar la configuración de seguridad en enlaces de la aplicación, o la sección modelo de servicio del archivo de configuración de un servicio.  
  
## En esta sección  
 [\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)  
 Describe el elemento `ServiceModel`.  
  
 [\<system.serviceModel.activation\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel-activation.md)  
 Configura la herramienta SMSvcHost.exe.  
  
 [\<system.runtime.serialization\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md)  
 El elemento de nivel superior para establecer opciones al usar serializadores como <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
## Secciones relacionadas  
 [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/es-es/13cb368e-88d4-4c61-8eed-2af0361c6d7a)  
 Describe cómo configurar los clientes y servicios de [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].