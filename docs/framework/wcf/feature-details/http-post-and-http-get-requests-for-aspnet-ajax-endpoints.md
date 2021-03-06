---
title: "C&#243;mo elegir entre solicitudes HTTP POST y HTTP GET para extremos AJAX de ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# C&#243;mo elegir entre solicitudes HTTP POST y HTTP GET para extremos AJAX de ASP.NET
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] le permite crear un servicio que expone un extremo de ASP.NET con AJAX habilitado al que se puede llamar desde JavaScript de un sitio web del cliente.  Los procedimientos básicos para crear tales servicios se discuten en [Uso de la configuración para agregar un extremo AJAX de ASP.NET](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) y [Cómo agregar un extremo AJAX de ASP.NET sin usar la configuración](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).  
  
 AJAX de ASP.NET admite operaciones que utilizan verbos HTTP POST y HTTP GET, donde HTTP POST es el valor predeterminado.  Si crea una operación que no tiene efectos secundarios y devuelve datos que raramente o nunca cambian, utilice HTTP GET en su lugar.  Los resultados de operaciones GET pueden almacenarse en memoria caché, lo que significa que varias llamadas a la misma operación solo pueden producir una solicitud a su servicio.  El almacenamiento en caché no se hace a través de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], sino que tiene lugar en cualquier nivel \(en el explorador de un usuario, en un servidor proxy, y en otros niveles.\) El almacenamiento  en memoria caché es ventajoso si desea aumentar el rendimiento del servicio, pero puede que no sea aceptable si los datos cambian con frecuencia o si la operación realiza alguna acción.  
  
 Por ejemplo, si está diseñando un servicio para administrar la biblioteca de música de un usuario, una operación que busca al artista basándose en el título del álbum, se beneficia del uso de GET, pero una operación que agrega un álbum a la colección personal del usuario debe utilizar POST.  
  
 Para controlar la duración de la caché, utilice el tipo <xref:System.ServiceModel.Web.OutgoingWebResponseContext>.  Por ejemplo, al diseñar un servicio que devuelve los boletines de previsión meteorológica actualizados cada hora, utilizaría GET pero limitar la duración del almacenamiento en caché a una hora o menos para evitar que los usuarios del servicio tengan acceso a datos obsoletos.  
  
 Al utilizar los servicios en una página AJAX de ASP.NET que utiliza el control del administrador de scripts, no hay diferencia si la operación usa GET o POST, el mecanismo del administrador de scripts se asegurara de que se emita el tipo de petición correcto.  
  
 Las operaciones GET y HTTP utilizan cualquier parámetro de entrada admitido por operaciones POST, incluso los datos complejos como los tipos de contrato.  Sin embargo, en la mayoría de los casos se recomienda evitar demasiados parámetros o parámetros que son demasiado complejos en operaciones GET, porque se reduce la eficacia de almacenamiento en caché.  
  
 En este tema se muestra cómo elegir entre GET y POST agregando atributos <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> a las operaciones pertinentes en el contrato de servicios.  Los otros pasos \(implementar, configurar y hospedar el servicio\) que se requieren para poner en marcha el servicio son similares a aquellos utilizados con el servicio de AJAX de ASP.NET en [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Una operación marcada con <xref:System.ServiceModel.Web.WebGetAttribute> siempre usa una solicitud GET.  Una operación marcada con <xref:System.ServiceModel.Web.WebInvokeAttribute> o no marcada con ninguno de los dos atributos, usa una solicitud POST.  <xref:System.ServiceModel.Web.WebInvokeAttribute> permite el uso de otros verbos HTTP, distintos de GET y POST \(como PUT y DELETE\) mediante la propiedad <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.  AJAX de ASP.NET no admite, sin embargo, estos verbos.  Si piensa utilizar el servicio desde páginas ASP.NET utilizando el control del administrador de scripts, no utilice la propiedad <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.  
  
 Para obtener un ejemplo práctico del cambio a GET, consulte el ejemplo [Servicio AJAX básico](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
 Para obtener un ejemplo que utiliza POST, consulte el ejemplo[Servicio AJAX mediante HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
### Creación de un servicio WCF que responda a solicitudes HTTP GET o HTTP POST  
  
1.  Defina un contrato de servicios de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] básico con una interfaz marcada con el atributo <xref:System.ServiceModel.ServiceContractAttribute>.  Marque cada operación con el <xref:System.ServiceModel.OperationContractAttribute>.  Agregue el atributo <xref:System.ServiceModel.Web.WebGetAttribute> para estipular que una operación debería responder a las solicitudes HTTP GET.  También puede agregar el atributo <xref:System.ServiceModel.Web.WebInvokeAttribute> para especificar explícitamente HTTP POST o no especificar un atributo, que tiene como valor predeterminado HTTP POST.  
  
    ```  
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  Implemente el contrato de servicios `IMusicService` con un `MusicService`.  
  
    ```  
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3.  Cree un nuevo archivo denominado servicio con una extensión .svc en la aplicación.  Modifique este archivo agregando la información de directiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) apropiada para el servicio.  Especifique que el <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> se ha de utilizar en la directiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) para configurar automáticamente un extremo de AJAX de ASP.NET.  
  
    ```  
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
### Realización de llamadas al servicio  
  
1.  Puede probar las operaciones GET de su servicio sin código de cliente, utilizando el examinador.  Por ejemplo, si su servicio se configura en la dirección "http:\/\/example.com\/service.svc", escribiendo "http:\/\/example.com\/service.svc\/LookUpArtist? album\=SomeAlbum" en la barra de dirección del explorador invoca al servicio y provoca la respuesta que se va a descargar o que se va a mostrar.  
  
2.  Puede utilizar los servicios con operaciones GET de la misma manera que cualquier otro servicio de AJAX de ASP.NET: escribiendo la URL de servicio en la colección Scripts del control del administrador de scripts de AJAX de ASP.NET..  Para obtener un ejemplo, consulte [Servicio AJAX básico](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
## Vea también  
 [Creación de servicios WCF para AJAX de ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [Cómo migrar servicios web de ASP.NET con AJAX habilitado a WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)