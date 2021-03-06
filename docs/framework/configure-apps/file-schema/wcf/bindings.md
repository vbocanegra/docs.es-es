---
title: "&lt;enlaces&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b62cd369-5409-4030-8490-9759a462dd3a
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;enlaces&gt;
Esta sección contiene una colección de enlaces estándar y personalizados.  Cada entrada es un elemento `binding` que se puede identificar por su `name` único.  Los servicios usan los enlaces vinculándose a ellos mediante `name`.  A partir de [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], no es necesario que los enlaces y los comportamientos tengan nombre.  Para obtener más información sobre la configuración predeterminada, así como sobre enlaces y comportamientos sin nombre, vea [Configuración simplificada](../../../../../docs/framework/wcf/simplified-configuration.md) y [Configuración simplificada de los servicios de WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## Enlace proporcionado por el sistema  
 Los enlaces proporcionados por el sistema ocultan la complejidad de la pila de mensajería de WCF.  Las aplicaciones que utilizan los enlaces proporcionados por el sistema no requieren el control completo sobre la pila.  Los atributos expuestos en cada enlace proporcionado por el sistema son los más apropiados para el escenario de uso de las direcciones de enlace.  
  
 La sección de configuración para cada enlace proporcionado por el sistema puede definir varias configuraciones utilizadas para configurar el enlace.  Un nombre único identifica a cada configuración.  
  
 No es posible agregar elementos o atributos a un enlace proporcionado por el sistema.  Para esto, debería implementar un enlace personalizado como se describe en la sección "Enlace personalizado" de este tema.  Es posible definir un enlace personalizado que imite perfectamente un enlace proporcionado por el sistema y agregue unos valores sobre los que la aplicación de usuario desee tener el control.  
  
 Para obtener una lista de enlaces proporcionados por el sistema, vea [Enlaces proporcionados por el sistema](../../../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Enlace personalizado  
 Los enlaces personalizados proporcionan el control completo sobre la pila de mensajería WCF.  Un enlace individual define la pila de mensajes mediante la especificación de los elementos de configuración para los elementos de la pila en el orden que aparecen en la pila.  Cada elemento define y configura un elemento de la pila.  Debe haber un único elemento de `transport` en cada enlace personalizado.  Sin este elemento, la pila de la mensajería está incompleta.  
  
 El orden de aparición de los elementos en la pila es importante, porque es el orden en el que las operaciones se aplican al mensaje.  El orden requerido de elementos de pila es el siguiente:  
  
1.  Transacciones \(opcional\)  
  
2.  Mensajería de confianza \(opcional\)  
  
3.  Seguridad \(opcional\)  
  
4.  Codificador  
  
5.  Transporte  
  
 Los enlaces personalizados se identifican mediante su atributo `name`.  Para obtener más información sobre enlaces personalizados, vea [Enlaces personalizados](../../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.BindingsSection>   
 <xref:System.ServiceModel.Channels.Binding>   
 <xref:System.ServiceModel.Channels.BindingElement>   
 [Enlaces](../../../../../docs/framework/wcf/bindings.md)   
 [Enlaces personalizados](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [\<enlace\>](../../../../../docs/framework/misc/binding.md)