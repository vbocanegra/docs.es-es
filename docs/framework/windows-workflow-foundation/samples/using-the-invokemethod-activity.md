---
title: "Uso de la actividad InvokeMethod | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6643550-d043-4ac7-8069-9c55ebbb4233
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Uso de la actividad InvokeMethod
En este ejemplo se muestra cómo utilizar la actividad <xref:System.Activities.Statements.InvokeMethod%601> para invocar métodos públicos en clases públicas.La actividad <xref:System.Activities.Statements.InvokeMethod%601> permite a un flujo de trabajo llamar a métodos contra objetos, pasar parámetros, obtener el valor devuelto, especificar tipos para métodos genéricos e indicar si el método es sincrónico o asincrónico.  
  
 Hay una versión no genérica de la actividad <xref:System.Activities.Statements.InvokeMethod> donde el valor devuelto se establece en la propiedad <xref:System.Activities.Statements.InvokeMethod.Result%2A> y una versión genérica de la actividad <xref:System.Activities.Statements.InvokeMethod%601> donde el valor se devuelve a través de la propiedad <xref:System.Activities.Statements.InvokeMethod.Result%601.Result%2A> de tipo `TResult`.  
  
 En este ejemplo se muestra cómo llamar a varios tipos de método.La siguiente lista detalla los tipos de método mostrados en este ejemplo:  
  
-   Invoque un método de instancia sin parámetros.  
  
-   Invoque un método de instancia con dos parámetros \(System.String y System.Int32\).  
  
-   Invoque un método de instancia con dos parámetros \(System.String y System.Int32\) y una matriz de parámetros de tipo System.String \[\].  
  
-   Invoque un método de instancia con dos parámetros \(dos números de System.Int32\) y un resultado de tipo System.Int32.  
  
     El valor devuelto se enlaza a una variable y se imprime en la consola mediante la actividad <xref:System.Activities.Statements.WriteLine>.  
  
-   Invoque un método estático con dos parámetros \(System.String y System.Int32\).  
  
-   Invoque un método de instancia con un parámetro genérico \(System.String\).  
  
-   Invoque un método estático con dos parámetros genéricos \(System.String y System.Int32\).  
  
-   Invoque un método de instancia que tenga un parámetro pasado por referencia \(System.String\).  
  
     El parámetro al que se hace referencia se enlaza a una variable y se imprime en la consola utilizando la actividad <xref:System.Activities.Statements.WriteLine>.  
  
-   Invoque un método de instancia asincrónico.  
  
## Para utilizar este ejemplo  
  
1.  Abra el archivo de solución InvokeMethodUsage.sln con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Para compilar la solución, presione Ctrl\+MAYÚS\+B.  
  
3.  Para ejecutar la solución, presione CTRL\+F5.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Basic\Built-InActivities\InvokeMethod`  
  
## Vea también