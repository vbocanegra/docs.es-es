---
title: "Implementar un proxy de detecci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dda20e79-8df3-438e-a281-69d779d978ec
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Implementar un proxy de detecci&#243;n
Esta sección describe los pasos necesarios para implementar un proxy de detección.  Un proxy de detección es un servicio independiente que contiene un repositorio de servicios.  Los clientes pueden consultar un proxy de detección para buscar servicios reconocibles que el proxy conoce.  El modo en que un proxy se rellena con servicios depende del implementador.  Por ejemplo, un proxy de detección puede conectarse a un repositorio de servicio existente y hacer que esa información sea reconocible, un administrador puede utilizar una API de administración para agregar servicios reconocibles a un proxy, o un proxy de detección puede utilizar la funcionalidad de anuncio para actualizar su memoria caché interna.  
  
 La implementación WCF proporciona clases base que le permiten compilar un proxy con facilidad.  Puede utilizar estas API para compilar un proxy de detección encima de un repositorio existente.  
  
 El proxy de detección implementado aquí es como cualquier otro servicio de WCF y también puede hacer que el proxy de detección se pueda detectar y que los clientes busquen sus extremos.  
  
## En esta sección  
 [Cómo: Implementar un proxy de detección](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)  
 Describe cómo implementar un proxy de detección.  
  
 [Cómo: Implementar un servicio reconocible que se registra con el proxy de detección](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)  
 Describe cómo implementar un servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] reconocible que se registra con el proxy de detección.  
  
 [Cómo: Implementar una aplicación cliente que utiliza el proxy de detección para buscar un servicio](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)  
 Describe cómo implementar una aplicación cliente de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] que utiliza el proxy de detección para buscar un servicio.  
  
 [Cómo: Probar el proxy de detección](../../../../docs/framework/wcf/feature-details/how-to-test-the-discovery-proxy.md)  
 Describe cómo probar el código escrito en los tres temas los anteriores.  
  
## Vea también  
 [Detección de WCF](../../../../docs/framework/wcf/feature-details/wcf-discovery.md)   
 [Cómo: Agregar detectabilidad mediante programación a un cliente y un servicio de WCF](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)