---
title: "ReliableSessionBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# ReliableSessionBindingElement
ReliableSessionBindingElement  
  
## Sintaxis  
  
```  
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## Métodos  
 La clase ReliableSessionBindingElement no define ningún método.  
  
## Propiedades  
 La clase ReliableSessionBindingElement posee las siguientes propiedades:  
  
### AcknowledgementInterval  
 Tipo de datos: datetime  
  
 Tipo de acceso: solo lectura  
  
 Intervalo de tiempo que un destino espera antes de enviar una confirmación al origen del mensaje en canales de confianza creados por el que generador.  
  
### FlowControlEnabled  
 Tipo de datos: booleano  
  
 Tipo de acceso: solo lectura  
  
 Valor booleano que especifica si el control de flujo está habilitado.  
  
### InactivityTimeout  
 Tipo de datos: datetime  
  
 Tipo de acceso: solo lectura  
  
 Especifica la duración máxima durante la cual el canal permite a la otra parte de la comunicación no enviar ningún mensaje antes de que se produzca un error.  
  
### MaxPendingChannels  
 Tipo de datos: sint32  
  
 Tipo de acceso: solo lectura  
  
 Número máximo de canales que pueden esperar a ser aceptados en el agente de escucha.  
  
### MaxRetryCount  
 Tipo de datos: sint32  
  
 Tipo de acceso: solo lectura  
  
 Número máximo de veces que un canal de confianza intenta retransmitir un mensaje, para él que no ha recibido una confirmación, llamando a `Send` en su canal subyacente.  
  
### MaxTransferWindowSize  
 Tipo de datos: sint32  
  
 Tipo de acceso: solo lectura  
  
 El tamaño máximo de la ventana de transferencia para la sesión de confianza.  
  
### Por orden  
 Tipo de datos: booleano  
  
 Tipo de acceso: solo lectura  
  
 Un valor booleano que especifica si se garantiza que los mensajes lleguen en el orden en el que fueron enviados.  
  
### ReliableMessagingVersion  
 Tipo de datos: enteros  
  
 Tipo de acceso: solo lectura  
  
 Entero que especifica la versión de protocolo de WS\-ReliableMessaging utilizado en la sesión de confianza.  
  
## Requisitos  
  
|MOF|Se declara en Servicemodel.mof.|  
|---------|-------------------------------------|  
|Espacio de nombres|Se define en root\\ServiceModel|  
  
## Vea también  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>