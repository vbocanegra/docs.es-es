---
title: "Publicaci&#243;n de extremos de metadatos | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29cd8a60-dfb7-460c-bf5a-c2b31b782671
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Publicaci&#243;n de extremos de metadatos
Los servicios de [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] publican metadatos mediante la publicación de uno o más extremos de metadatos.La publicación de metadatos de servicio pone los metadatos a disposición mediante protocolos estandarizados, como WS\-MetadataExchange \(MEX\) y solicitudes HTTP\/GET.Los extremos de metadatos son similares a otros extremos de servicio en cuanto que tienen una dirección, un enlace y un contrato, y se pueden agregar a un host del servicio mediante configuración o código.Para habilitar la publicación de extremos de metadatos, debe agregar el comportamiento de servicio <xref:System.ServiceModel.Description.ServiceMetadataBehavior> al servicio.  
  
## En esta sección  
 [Cómo publicar metadatos para un servicio mediante un archivo de configuración](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 Muestra cómo configurar un servicio de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] para publicar metadatos de tal modo que los clientes puedan recuperar los metadatos mediante una solicitud HTTP\/GET o WS\-MetadataExchange mediante la cadena de consulta `?wsdl`.  
  
 [Publicación de metadatos para un servicio mediante código](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 Muestra cómo habilitar la publicación de metadatos para un servicio de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] en código de tal modo que los clientes puedan recuperar los datos mediante una solicitud HTTP\/GET o WS\-MetadataExchange mediante la cadena de consulta `?wsdl`.  
  
## Vea también  
 [Publicación de metadatos](../../../docs/framework/wcf/feature-details/publishing-metadata.md)