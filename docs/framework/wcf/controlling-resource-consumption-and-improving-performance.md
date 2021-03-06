---
title: "Control del consumo de recursos y mejora del rendimiento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a829669-5f76-4c88-80ec-92d0c62c0660
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Control del consumo de recursos y mejora del rendimiento
En este tema se describen varias propiedades en diferentes áreas de la arquitectura [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] que trabajan para controlar el consumo de recursos y que afectan a las mediciones del rendimiento.  
  
## Propiedades que restringen el consumo de recursos en WCF  
 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] aplica las restricciones en ciertos tipos de procesos con fines de seguridad o rendimiento.Estas restricciones adquieren dos formas básicas: cuotas y aceleradores.*Las cuotas* son los límites que cuando se alcanzan o superan desencadenan una excepción inmediata en algún punto del sistema.*Los aceleradores* son límites que no producen inmediatamente una excepción.En su lugar, cuando se alcanza el límite del acelerador, el procesamiento continúa pero dentro de los límites establecidos por ese valor.Este procesamiento limitado puede activar una excepción en otra parte, pero esto depende de la aplicación.  
  
 Además de la distinción entre cuotas y aceleradores, algunas propiedades de restricción se encuentran en el nivel de serialización, algunas en el nivel de transporte y algunas en el nivel de aplicación.Por ejemplo, la cuota <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=fullName>, que implementan todos los elementos de enlace de transporte proporcionados por el sistema, está establecida de forma predeterminada en 65.536 bytes para impedir que los clientes malintencionados emprendan ataques de denegación de servicio contra un servicio provocando el consumo excesivo de memoria.\(Normalmente, puede aumentar el rendimiento bajando este valor.\)  
  
 Un ejemplo de una cuota de la serialización es la propiedad <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=fullName>, que especifica el número máximo de objetos que el serializador serializa o deserializa en una única llamada al método <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A>.Un ejemplo de un acelerador en el nivel de aplicación es la propiedad <xref:System.ServiceModel.Dispatcher.ServiceThrottle.MaxConcurrentSessions%2A?displayProperty=fullName>, que de forma predeterminada restringe el número de conexiones de canal con sesión simultáneas a 10.\(A diferencia de las cuotas, si se alcanza este valor de acelerador, la aplicación continúa con el procesamiento pero no acepta nuevos canales con sesión, lo que significa que los nuevos clientes no se pueden conectar hasta que uno de los otros canales con sesión haya finalizado.\)  
  
 Estos controles están diseñados para proporcionar una mitigación rápida contra ciertos tipos de ataques o para mejorar métrica de rendimiento tal como el consumo de memoria, el tiempo de inicio, etc.Sin embargo, dependiendo de la aplicación, estos controles pueden impedir el rendimiento de la aplicación del servicio o evitar que la aplicación funcione.Por ejemplo, una aplicación diseñada para transmitir secuencias de vídeo puede superar con facilidad la propiedad <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=fullName> predeterminada.En este tema se proporciona un resumen de los diferentes controles aplicados a las aplicaciones en todos los niveles de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], describe varias maneras para obtener más información sobre si un valor está entorpeciendo su aplicación, y describe maneras de corregir varios problemas.La mayoría de los aceleradores y algunas cuotas están disponibles en el nivel de aplicación, incluso cuando la propiedad base es una serialización o una restricción de transporte.Por ejemplo, puede establecer la propiedad <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=fullName> utilizando la propiedad <xref:System.ServiceModel.ServiceBehaviorAttribute.MaxItemsInObjectGraph%2A?displayProperty=fullName> en la clase de servicio.  
  
> [!NOTE]
>  Si tiene un problema determinado, debería leer primero [Inicio rápido de solución de problemas de WCF](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md) para ver si su problema \(y una solución\) aparecen en la lista.  
  
 Las propiedades que restringen los procesos de serialización están listadas en [Consideraciones de seguridad para datos](../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).Las propiedades que restringen el consumo de recursos relacionadas con transportes están listadas en [Cuotas de transporte](../../../docs/framework/wcf/feature-details/transport-quotas.md).Las propiedades que restringen el consumo de recursos en el nivel de aplicación son los miembros de la clase <xref:System.ServiceModel.Dispatcher.ServiceThrottle>.  
  
## Detectar la aplicación y los problemas de rendimiento relacionados con los valores de cuota  
 Los valores predeterminados de los valores anteriores se han elegido para habilitar la funcionalidad de la aplicación básica en una amplia gama de tipos de aplicación proporcionando al mismo tiempo protección básica contra los problemas de seguridad comunes.Sin embargo, los diseños de las diferentes aplicaciones pueden superar uno o más valores de acelerador aunque por otro lado la aplicación sea segura y funcione como se ha diseñado.En estos casos, debe identificar qué valores de acelerador se superan y en qué nivel, y decidir la acción adecuada para aumentar el rendimiento de la aplicación.  
  
 Normalmente, al escribir la aplicación y depurarla, establece la propiedad <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> en `true` en el archivo de configuración o mediante programación.Esto indica [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] que se devuelvan marcas de traza de la pila de excepción de servicio a la aplicación cliente para analizarlas.Esta característica crea informes de la mayoría de las excepciones en el nivel de aplicación de manera que se muestran qué valores de cuota podrían estar implicados, si ése es el problema.  
  
 En tiempo de ejecución se producen algunas excepciones bajo el nivel de aplicación visible y no se devuelven por medio de este mecanismo ni pueden controlarse mediante una implementación <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=fullName> personalizada.Si está en un entorno de desarrollo como Microsoft Visual Studio, la mayoría de estas excepciones se muestran automáticamente.Sin embargo, algunas excepciones pueden ser enmascaradas por algunos valores del entorno de desarrollo como los valores [Just My Code](http://go.microsoft.com/fwlink/?LinkId=82174) en Visual Studio 2005.  
  
 Independientemente de las funciones de su entorno de desarrollo, puede utilizar las funciones de traza de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] y registro de mensajes para depurar todas las excepciones y ajustar el rendimiento de sus aplicaciones.Para obtener más información, vea [Uso del seguimiento para solucionar problemas de su aplicación](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md).  
  
## Problemas de rendimiento y XmlSerializer  
 Los servicios y las aplicaciones cliente que usan tipos de datos que son serializables mediante <xref:System.Xml.Serialization.XmlSerializer> generan y compilan el código de serialización de los tipos de datos en tiempo de ejecución, lo que se puede traducir en un rendimiento de inicio lento.  
  
> [!NOTE]
>  El código de serialización generado previamente solo puede usarse en aplicaciones cliente, no en servicios.  
  
 [Herramienta de utilidad de metadatos de ServiceModel \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) puede mejorar el rendimiento de inicio de estas aplicaciones generando el código de serialización necesario a partir de los ensamblados compilados para la aplicación.Para obtener más información, vea [Cómo: Mejorar el tiempo de inicio de las aplicaciones cliente WCF mediante XmlSerializer](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md).  
  
## Problemas de rendimiento al hospedar los servicios WCF bajo ASP.NET  
 Cuando un servicio WCF se hospeda bajo IIS y ASP.NET, la configuración de IIS y ASP.NET puede afectar al rendimiento y al consumo de memoria del servicio WCF.[!INCLUDE[crabout](../../../includes/crabout-md.md)] el rendimiento de ASP.NET, vea [Mejorar el rendimiento de ASP.NET](http://go.microsoft.com/fwlink/?LinkId=186462).Una configuración que quizá pueda tener consecuencias imprevistas es la propiedad <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A>, que es una propiedad de la clase <xref:System.Web.Configuration.ProcessModelSection>.Si la aplicación tiene un número fijo o pequeño de clientes, al establecer <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A> en 2 se podría observar un aumento del rendimiento en un equipo con varios procesadores que tenga un uso de CPU próximo al 100%.Esta mejora del rendimiento tiene su precio: aumentará también el consumo de memoria, lo que podría disminuir la escalabilidad.  
  
## Vea también  
 [Administración y diagnóstico](../../../docs/framework/wcf/diagnostics/index.md)   
 [Datos de gran tamaño y secuencias](../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)