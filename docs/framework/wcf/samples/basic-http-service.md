---
title: "Servicio HTTP b&#225;sico | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27048b43-8a54-4f2a-9952-594bbfab10ad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Servicio HTTP b&#225;sico
En este ejemplo se muestra cómo implementar un servicio basado en HTTP y en RPC, al que se suele hacer referencia como servicio "POX" \(Plain Old XML o de XML antiguo y sin formato\)", utilizando el modelo de programación REST de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Este ejemplo consta de dos componentes: un servicio HTTP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] autohospedado \(Service.cs\) y una aplicación de consola \(Program.cs\) que crea el servicio y le llama.  
  
## Detalles del ejemplo  
 El servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] expone dos operaciones, `EchoWithGet` y `EchoWithPost`, que devuelven la cadena que se les pasa como entrada.  
  
 La operación `EchoWithGet` se anota con <xref:System.ServiceModel.Web.WebGetAttribute>, que indica que la operación procesa las solicitudes `GET` de HTTP.Dado que el <xref:System.ServiceModel.Web.WebGetAttribute> no especifica un objeto <xref:System.UriTemplate> explícitamente, la operación espera a que se pase la cadena de entrada con un parámetro de cadena de consulta con el nombre `s`.Observe que el formato del URI que el servicio espera se puede personalizar utilizando la propiedad <xref:System.ServiceModel.Web.WebGetAttribute.UriTemplate%2A>.  
  
 La operación `EchoWithPost` se anota con <xref:System.ServiceModel.Web.WebInvokeAttribute>, que indica que no es una operación `GET` \(tiene efectos secundarios\).Dado que el <xref:System.ServiceModel.Web.WebInvokeAttribute> no especifica un `Method` explícitamente, la operación procesa las solicitudes `POST` de HTTP que tienen la cadena en el cuerpo de la solicitud \(en el formato XML, por ejemplo\).Observe que el método HTTP y el formato del URI para la solicitud se pueden personalizar utilizando las propiedades <xref:System.ServiceModel.Web.WebInvokeAttribute.UriTemplate> y <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>, respectivamente.  
  
 El archivo App.config configura el servicio WCF con un <xref:System.ServiceModel.Description.WebHttpEndpoint> predeterminado que tiene la propiedad <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> establecida en `true`.Como resultado, la infraestructura de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea una página de Ayuda automática y basada en HTML en `http://localhost:8000/Customers/help` que proporciona información acerca de cómo construir las solicitudes HTTP para el servicio y cómo utilizar la respuesta HTTP del servicio.  
  
 El archivo Program.cs muestra el modo en que se puede usar un generador de canales de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] para realizar llamadas a las respuestas de proceso y servicio.Observe que se trata simplemente de una manera de tener acceso a un servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].También es posible tener acceso al servicio utilizando otras clases de .NET Framework como <xref:System.Net.HttpWebRequest> y <xref:System.Net.WebClient>.Otros ejemplos del SDK \(como [Selección de formato automática](../../../../docs/framework/wcf/samples/automatic-format-selection.md) y [Servicio de recurso básico](../../../../docs/framework/wcf/samples/basic-resource-service.md)\) muestran cómo utilizar estas clases para comunicarse con un servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 El ejemplo consta de un servicio autohospedado y un cliente que se ejecutan ambos dentro de una aplicación de consola.A medida que se ejecuta la aplicación de consola, el cliente realiza solicitudes al servicio y escribe la información pertinente de las respuestas en la ventana de la consola.  
  
#### Para utilizar este ejemplo  
  
1.  Abra la solución del ejemplo de servicio HTTP básico.Al iniciar [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], debe ejecutarlo como administrador para que el ejemplo se ejecute correctamente.Para ello, haga clic con el botón secundario en el icono de [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] y seleccione **Ejecutar como administrador** en el menú contextual.  
  
2.  Presione CTRL\+MAYÚS\+B para compilar la solución y, a continuación, presione Ctrl\+F5 para ejecutar la aplicación de consola sin depurar.La ventana de la consola aparece y proporciona el URI del servicio en ejecución y el URI de la página de Ayuda HTML para este.Puede ver la página de Ayuda HTML en cualquier momento escribiendo su URI en un explorador.A medida que el ejemplo se ejecuta, el cliente escribe el estado de la actividad actual.  
  
3.  Presione cualquier tecla para terminar el ejemplo.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WCF\Basic\Web\BasicHttpService`  
  
## Vea también  
 [Selección de formato automática](../../../../docs/framework/wcf/samples/automatic-format-selection.md)   
 [Servicio de recurso básico](../../../../docs/framework/wcf/samples/basic-resource-service.md)