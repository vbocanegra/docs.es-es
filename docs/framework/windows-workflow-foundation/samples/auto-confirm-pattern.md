---
title: "Modelo de autoconfirmaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 668aec65-78d3-4636-9c7b-deed643a18f9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Modelo de autoconfirmaci&#243;n
Este ejemplo consta de tres escenarios que se ejecutan para mostrar una actividad `AutoConfirmScope` personalizada.En el primer ejemplo se muestra la ejecución correcta de una secuencia de cuatro actividades de compensación, donde las actividades segunda y tercera están anidadas en una actividad `AutoConfirmScope`.En el segundo ejemplo se muestra la misma secuencia, con una excepción que se produce después de la ejecución de la cuarta actividad <xref:System.Activities.Statements.CompensableActivity>.En el tercer escenario se muestra la misma secuencia, con una excepción que se produce en la actividad `AutoConfirmScope` después de que se complete la segunda actividad <xref:System.Activities.Statements.CompensableActivity>.  
  
 El ejemplo muestra el modelo de autoconfirmación, donde todas las actividades de compensación secundarias se confirman al completarse correctamente el ámbito.Este modelo define la duración de todas las actividades de compensación secundarias, puesto que ya no se pueden compensar ni confirmar.  
  
 El ámbito consta de una clase <xref:System.Activities.Statements.TryCatch> donde la propiedad <xref:System.Activities.Statements.TryCatch.Try%2A> es una actividad <xref:System.Activities.Statements.CompensableActivity> interna.El cuerpo especificado por el usuario de la actividad `AutoConfirmScope` es el cuerpo de la actividad <xref:System.Activities.Statements.CompensableActivity> interna.Cuando esta actividad <xref:System.Activities.Statements.CompensableActivity> interna se completa, genera una clase <xref:System.Activities.Statements.CompensationToken> como argumento de salida.`AutoConfirmScope` utiliza una propiedad <xref:System.Activities.Statements.TryCatch.Finally%2A> para comprobar si se ha generado el token y, si es así, confirma la actividad <xref:System.Activities.Statements.CompensableActivity> interna.La actividad <xref:System.Activities.Statements.CompensableActivity> interna invoca la compensación predeterminada para cualquier actividad de compensación que pueda existir en su cuerpo.  
  
 En el primer escenario se muestra la ejecución correcta del flujo de trabajo y se demuestra que las actividades de compensación segunda y tercera ya están confirmadas cuando se completa el flujo de trabajo y se confirman la primera y la cuarta.Esto genera un orden de confirmación de tres, dos, cuatro y uno.  
  
 En el segundo escenario se muestra una excepción una vez que se han completado las cuatro actividades de compensación.Dado que las actividades de compensación dos y tres ya están confirmadas, no se ven afectadas, pero las actividades primera y cuarta se compensan.Esto genera la confirmación de tres, la confirmación de dos, la compensación de cuatro y la compensación de uno.  
  
 El último escenario muestra la ejecución incorrecta de la actividad `AutoConfirmScope`.En este escenario, se produce una excepción después de que se complete la segunda actividad <xref:System.Activities.Statements.CompensableActivity>.Dado que las actividades de compensación tercera y cuarta no se han ejecutado, no se ven afectadas.Dado que el ámbito no se completó correctamente, la segunda actividad <xref:System.Activities.Statements.CompensableActivity> no se confirma.Esto genera un orden de compensación de dos y uno.  
  
#### Para utilizar este ejemplo  
  
1.  Con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], abra el archivo de solución AutoConfirmSample.sln.  
  
2.  Para compilar la solución, presione Ctrl\+MAYÚS\+B.  
  
3.  Para ejecutar la solución, presione CTRL\+F5.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Scenario\Compensation\AutoConfirm`  
  
## Vea también