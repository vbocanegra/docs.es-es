---
title: "Trabajar con NAT y firewalls | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "firewalls [WCF]"
  - "NAT [WCF]"
ms.assetid: 74db0632-1bf0-428b-89c8-bd53b64332e7
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Trabajar con NAT y firewalls
Frecuentemente, el cliente y servidor de una conexión de red no tienen una ruta de acceso directa y abierta para la comunicación.Los paquetes se filtran, enrutan, analizan y transforman tanto en los equipos de extremo como en equipos intermedios de la red.Las traducciones de direcciones de red \(NATs\) y los firewalls son ejemplos comunes de aplicaciones intermedias que pueden participar en la comunicación de redes.  
  
 Los transportes de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y los patrones de intercambio de mensajes \(MEP\) reaccionan de manera diferente ante la presencia de NAT y firewalls.En este tema se describe cómo las NAT y los firewalls funcionan en topologías de redes comunes.Se proporcionan recomendaciones para combinaciones concretas de MEP y transportes de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] que ayudan a hacer aplicaciones más robustas frente a NAT y firewalls en la red.  
  
## Cómo afectan las NAT a la comunicación  
 NAT se creó para permitir a varios equipos compartir una dirección IP externa única.Una NAT de reasignación de puertos asigna una dirección IP interna y un puerto para una conexión a una dirección IP externa con un nuevo número de puerto.El nuevo número de puerto le permite a la NAT correlacionar el tráfico del retorno con la comunicación original.Muchos usuarios domésticos tienen una dirección IP que solo es enrutable de manera privada y confían en una NAT para que proporcione el enrutamiento global de paquetes.  
  
 Una NAT no proporciona un límite de seguridad.Sin embargo, las configuraciones NAT comunes evitan que se direccionen los equipos internos directamente.Esto protege los equipos internos de algunas conexiones no deseadas y dificulta la escritura de aplicaciones de servidor que deben devolver de forma asincrónica datos al cliente.La NAT reescribe las direcciones en paquetes para hacer parecer que se están originando conexiones en el equipo NAT.Esto hace que el servidor obtenga un error al intentar abrir una conexión de vuelta al cliente.Si el servidor utiliza la dirección percibida del cliente, se produce un error porque no se puede enrutar la dirección del cliente públicamente.Si el servidor utiliza la dirección NAT, no puede conectarse porque ninguna aplicación está realizando escuchas en ese equipo.  
  
 Algunas NAT admiten la configuración de reglas de reenvío para permitir a los equipos externos que se conecten a un equipo interno determinado.Las instrucciones para configurar las reglas de reenvío varían entre NAT diferentes y no se recomienda para la mayoría de las aplicaciones el pedir a los usuarios finales que cambien su configuración NAT.Muchos usuarios finales no pueden o no quieren cambiar su configuración de NAT para una aplicación determinada.  
  
## Cómo afectan los firewalls a la comunicación  
 Un *firewall* es un software o dispositivo de hardware que aplica las reglas al tráfico que pasa para decidir si permitir o negar el paso.Puede configurar los firewalls para examinar secuencias de tráfico entrantes o salientes.El firewall proporciona un límite de seguridad para la red en el borde de la red o en el host del extremo.Los usuarios de empresas han mantenido tradicionalmente sus servidores tras un firewall para evitar ataques malintencionados.Desde la introducción del firewall personal en [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)], el número de usuarios domésticos tras un firewall también ha aumentado en gran medida.Esto hace probable que uno o ambos extremos de una conexión tengan un firewall que examine los paquetes.  
  
 Los firewalls varían en gran medida en cuanto a su complejidad y capacidad para examinar los paquetes.Los firewalls simples aplican reglas basadas en las direcciones de origen y destino y los puertos en los paquetes.Los firewalls inteligentes también pueden examinar el contenido de paquetes para tomar decisiones.Estos firewalls vienen en muchas configuraciones diferentes y se utilizan a menudo para aplicaciones especializadas.  
  
 Una configuración común para un firewall del usuario doméstico consiste en prohibir las conexiones entrantes a menos que se haya realizado una conexión de salida previamente a ese equipo.Una configuración común para un firewall de usuario empresarial consiste en prohibir las conexiones entrantes en todos los puertos exceptuando un grupo identificado específicamente.Un ejemplo es un firewall que prohíbe las conexiones en todos los puertos salvo el puerto 80 y 443 para proporcionar servicio HTTP y HTTPS.Los firewalls administrados existen tanto para usuarios domésticos como para usuarios empresariales, y permiten a un usuario o proceso de confianza del equipo cambiar la configuración del firewall.Los firewalls administrados son más comunes para usuarios domésticos donde no hay ninguna directiva corporativa que controle el uso de la red.  
  
## Uso de Teredo  
 Teredo es una tecnología de transición de IPv6 que habilita la direccionabilidad directa de equipos detrás de una NAT.Teredo se basa en el uso de un servidor que se puede enrutar de manera pública y global para anunciar conexiones potenciales.El servidor de Teredo da al servidor y cliente de la aplicación un punto de reunión común en el que pueden intercambiar información de conexión.Los equipos solicitan a continuación una dirección Teredo temporal y los paquetes se pasan mediante túneles a través de la red existente.La compatibilidad con Teredo en [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] necesita habilitar la compatibilidad con IPv6 y Teredo en el sistema operativo.[!INCLUDE[wxp](../../../../includes/wxp-md.md)] y los sistemas operativos posteriores admiten Teredo.[!INCLUDE[wv](../../../../includes/wv-md.md)] y los sistemas operativos posteriores admiten IPv6 de forma predeterminada y solo el usuario necesita habilitar Teredo.[!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] y [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] necesitan que el usuario habilite IPv6 y Teredo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Información general sobre Teredo](http://go.microsoft.com/fwlink/?LinkId=87571).  
  
## Elección de un patrón de intercambio de mensajes y transporte  
 La selección de un transporte y MEP es un proceso de tres pasos:  
  
1.  Analice la direccionabilidad de los equipos de extremo.Los servidores de empresas tienen normalmente direccionabilidad directa, mientras que los usuarios finales tienen normalmente la direccionabilidad bloqueada mediante NAT.Si ambos extremos están detrás de una NAT, como en escenarios punto a punto entre usuarios finales, podría necesitar una tecnología como Teredo para proporcionar direccionabilidad.  
  
2.  Analice el protocolo y las restricciones de puertos de los equipos de extremos.Los servidores de empresa están generalmente detrás de firewalls fuertes que bloquean muchos puertos.Sin embargo, el puerto 80 se abre con frecuencia para permitir el tráfico HTTP, y el puerto 443 se abre para permitir el tráfico HTTPS.Es menos probable que los usuarios finales tengan restricciones de puertos, pero puede que estén detrás de un firewall que solo permita conexiones de salida.Algunos firewalls permiten la administración mediante aplicaciones en el extremo para abrir conexiones de manera selectiva.  
  
3.  Calcule los transportes y MEP que permiten la direccionabilidad y las restricciones de puertos de la red.  
  
 Una topología común para las aplicaciones cliente\-servidor consiste en tener clientes que estén detrás de un NAT sin Teredo con un firewall solo de salida y un servidor que sea direccionable de manera directa con un firewall fuerte.En este escenario, el transporte TCP con un MEP dúplex y un transporte HTTP con un MEP de solicitud\-respuesta funcionan bien.Una topología común para las aplicaciones punto a punto consiste en tener ambos extremos detrás de NAT y firewalls.En este escenario y en escenarios donde la topología de red sea desconocida, considere las recomendaciones siguientes:  
  
-   No utilice transportes duales.Un transporte dual abre más conexiones, lo que reduce la oportunidad de realizar correctamente una conexión.  
  
-   Permita establecer canales secundarios a través de la conexión originaria.Utilizar canales secundarios, como en TCP dúplex, abre menos conexiones, lo que aumenta la oportunidad de realizar correctamente una conexión.  
  
-   Emplee un servicio alcanzable para registrar extremos o la retransmisión de tráfico.El uso de un servicio de conexión alcanzable globalmente, como un servidor Teredo, aumenta en gran medida la probabilidad de realizar correctamente una conexión cuando la topología de red es restrictiva o desconocida.  
  
 Las siguientes tablas examinan los transportes MEP unidireccionales, de solicitud\-respuesta y dúplex; los transportes estándar TCP y TCP con Teredo; así como los transportes HTTP estándar y duales en [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
|Direccionabilidad|Servidor directo|Servidor directo con transversal NAT|Servidor NAT|Servidor NAT con transversal NAT|  
|-----------------------|----------------------|------------------------------------------|------------------|--------------------------------------|  
|Cliente directo|Cualquier transporte y MEP.|Cualquier transporte y MEP.|No se admite.|No se admiten.|  
|Cliente directo con transversal NAT|Cualquier transporte y MEP.|Cualquier transporte y MEP.|No se admiten.|TCP con Teredo y cualquier MEP.[!INCLUDE[wv](../../../../includes/wv-md.md)] tiene una opción de configuración de equipo para admitir HTTP con Teredo.|  
|NAT cliente|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|No se admiten.|No se admiten.|  
|NAT cliente con transversal NAT|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Todos menos HTTP dual y cualquier MEP.Un MEP dúplex requiere transporte TCP.El transporte TCP dual necesita Teredo.[!INCLUDE[wv](../../../../includes/wv-md.md)] tiene una opción de configuración de equipo para admitir HTTP con Teredo.|No se admiten.|TCP con Teredo y cualquier MEP.[!INCLUDE[wv](../../../../includes/wv-md.md)] tiene una opción de configuración de equipo para admitir HTTP con Teredo.|  
  
|Restricciones del firewall|Servidor abierto|Servidor con firewall administrado|Servidor con firewall solo HTTP|Servidor con firewall solo de salida|  
|--------------------------------|----------------------|----------------------------------------|-------------------------------------|------------------------------------------|  
|Cliente abierto|Cualquier transporte y MEP.|Cualquier transporte y MEP.|Cualquier transporte HTTP y MEP.|No se admiten.|  
|Cliente con firewall administrado|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Cualquier transporte HTTP y MEP.|No se admiten.|  
|Cliente con firewall solo HTTP|Cualquier transporte HTTP y MEP.|Cualquier transporte HTTP y MEP.|Cualquier transporte HTTP y MEP.|No se admiten.|  
|Cliente con firewall solo de salida|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Cualquier transporte no dual y MEP.Un MEP dúplex requiere transporte TCP.|Cualquier transporte HTTP y cualquier MEP no dúplex.|No se admiten.|