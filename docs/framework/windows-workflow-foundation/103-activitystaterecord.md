---
title: "103 - ActivityStateRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57636a9a-561e-44aa-aef9-1f1894aaa6dd
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 103 - ActivityStateRecord
## Propiedades  
  
|||  
|-|-|  
|Id.|103|  
|Palabras clave|EndToEndMonitoring, Troubleshooting, HealthMonitoring, WFTracking|  
|Nivel|Información|  
|Canal|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descripción  
 El participante de seguimiento de ETW emite este evento cuando una actividad en una instancia de flujo de trabajo emite ActivityStateRecord.  
  
## Mensaje  
 TrackRecord \= ActivityStateRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, State \= %4, Name\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Arguments\=%9, Variables\=%10, Annotations\=%11, ProfileName \= %12  
  
## Detalles  
  
|Nombre del elemento de datos|Tipo del elemento de datos|Descripción|  
|----------------------------------|--------------------------------|-----------------|  
|InstanceId|xs:GUID|El id. de instancia del flujo de trabajo.|  
|RecordNumber|xs:long|El número de secuencia del registro emitido.|  
|EventTime|xs:dateTime|La hora en UTC cuando se emitió el evento.|  
|State|xs:string|El estado de la actividad.|  
|Name|xs:string|El nombre para mostrar de la actividad que emitió el evento.|  
|ActivityId|xs:string|El id. de actividad de la actividad que se emite.|  
|ActivityInstanceId|xs:string|El id. de instancia de la actividad de la actividad que se emite.|  
|ActivityTypeName|xs:string|El nombre del tipo de la actividad que se emite.|  
|Arguments|xs:string|Los argumentos a los que se realizó el seguimiento con este evento.Los valores se almacenan en un elemento xml en el formato \<items\>\< item  name \= "argumentName" type\="System.String"\>argumentValue\<\/item\>\<\/items\>.Si no se realizó ningún seguimiento del argumento, la cadena contiene \<items\/\>.El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW.Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de anotación con \<items\>...\<\/items.\>Los tipos siguientes están almacenados como valores posibles ya que los devuelve ToString\(\); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.Todos los demás tipos se serializan con System.Runtime.Serialization.NetDataContractSerializer.|  
|Variables|xs:string|Las variables a las que se realizó el seguimiento con este evento.Los valores se almacenan en un elemento xml en el formato \<items\>\< item  name \= "variableName" type\="System.String"\>variableValue\<\/item\>\<\/items\>.Si no se realizaron seguimientos a variables, la cadena contiene \<items\/\>.El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW.Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de las variables con \<items\>...\<\/items.\>Los tipos siguientes están almacenados como valores posibles ya que los devuelve ToString\(\); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.Todos los demás tipos se serializan con System.Runtime.Serialization.NetDataContractSerializer.|  
|Annotations|xs:string|Las anotaciones que se agregaron a este evento.Los valores se almacenan en un elemento xml con el formato\<items\>\< item  name \= "annotationName" type\="System.String"\>annotationValue\<\/item\>\<\/items\>.Si no se especifica ninguna anotación, la cadena contendrá \<items\/\>.El tamaño del evento ETW está limitado por el tamaño de búfer de ETW o la carga útil máxima para un evento ETW.Si el tamaño del evento supera los límites de ETW, el evento se trunca quitando las anotaciones y reemplazando el valor de anotación con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|El nombre o el perfil de seguimiento que dio como resultado que se emitiera este evento.|  
|HostReference|xs:string|En el caso de los servicios hospedados en web, este campo identifica de manera única el servicio en la jerarquía web.Su formato se define como 'Ruta de acceso virtual de la aplicación del nombre del sitio web&#124;Ruta de acceso virtual del servicio&#124;NombreServicio' Ejemplo: 'Sitio web predeterminado\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|xs:string|La cadena devuelta por AppDomain.CurrentDomain.FriendlyName.|