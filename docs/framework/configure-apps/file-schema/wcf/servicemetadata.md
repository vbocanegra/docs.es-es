---
title: "&lt;serviceMetadata&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 2b4c3b4c-31d4-4908-a9b7-5bb411c221f2
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# &lt;serviceMetadata&gt;
Especifica la publicación de metadatos e información asociada del servicio.  
  
## Sintaxis  
  
```  
  
<serviceMetadata   
    externalMetadataLocation="String"  
    httpGetBinding=”String”  
    httpGetBindingConfiguration=”String”  
    httpGetEnabled="Boolean"   
    httpGetUrl="String"  
    httpsGetBinding=”String”  
    httpsGetBindingConfiguration=”String”  
    httpsGetEnabled="Boolean"   
    httpsGetUrl="String"  
    policyVersion="Policy12/Policy15"/>  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|externalMetadataLocation|Un URI que contiene la ubicación de un archivo WSDL que se devuelve al usuario en respuesta a las solicitudes WSDL y MEX en lugar del WSDL generado automáticamente.  Cuando no se establece este atributo, se devuelve el WSDL predeterminado.  El valor predeterminado es una cadena vacía.|  
|httpGetBinding|Cadena que especifica el tipo de enlace que se usará para la recuperación de metadatos a través de HTTP GET.  Este valor es opcional.  Si no se especifica, se usarán los enlaces predeterminados.<br /><br /> Solo se admitirán los enlaces con elementos de enlace internos que admiten <xref:System.ServiceModel.Channels.IReplyChannel>.  Además, la propiedad <xref:System.ServiceModel.Channels.MessageVersion%2A> del enlace debe ser <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.|  
|httpGetBindingConfiguration|Cadena que establece el nombre del enlace que se especifica en el atributo `httpGetBinding`, que hace referencia a la información de configuración adicional de este enlace.  El mismo nombre se debe definir en la sección `<bindings>`.|  
|httpGetEnabled|Un valor boolenao que especifica si publicar los metadatos del servicio para la recuperación utilizando un HTTP\/Obtener solicitud.  De manera predeterminada, es `false`.<br /><br /> Si no se especifica el atributo httpGetUrl, la dirección en la que se publican los metadatos es la dirección de servicio más un "? wsdl."  Por ejemplo, si la dirección de servicio es "http:\/\/localhost:8080\/CalculatorService", la dirección de los metadatos de HTTP\/Get es "http:\/\/localhost:8080\/CalculatorService?wsdl."<br /><br /> Si esta propiedad es `false` o la dirección del servicio no se basa en HTTP o HTTPS, “?wsdl” se omite.|  
|httpGetUrl|URI que especifica la dirección en la que se publican los metadatos para la recuperación mediante una solicitud HTTP\/Get.  Si se especifica un URI relativo, se tratará como relativo a la dirección base del servicio.|  
|httpsGetBinding|Cadena que especifica el tipo de enlace que se usará para la recuperación de metadatos a través de HTTPS GET.  Este valor es opcional.  Si no se especifica, se usarán los enlaces predeterminados.<br /><br /> Solo se admitirán los enlaces con elementos de enlace internos que admiten <xref:System.ServiceModel.Channels.IReplyChannel>.  Además, la propiedad <xref:System.ServiceModel.Channels.MessageVersion%2A> del enlace debe ser <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.|  
|httpsGetBindingConfiguration|Cadena que establece el nombre del enlace que se especifica en el atributo `httpsGetBinding`, que hace referencia a la información de configuración adicional de este enlace.  El mismo nombre se debe definir en la sección `<bindings>`.|  
|httpsGetEnabled|Un valor boolenao que especifica si se van a publicar los metadatos del servicio para la recuperación mediante una solicitud HTTP\/Get.  De manera predeterminada, es `false`.<br /><br /> Si no se especifica el atributo httpsGetUrl, la dirección en la que se publican los metadatos es la dirección de servicio más un "? wsdl."  Por ejemplo, si la dirección de servicio es "https:\/\/localhost:8080\/CalculatorService", la dirección de los metadatos de HTTP\/Get es "https:\/\/localhost:8080\/CalculatorService?wsdl."<br /><br /> Si esta propiedad es `false` o la dirección del servicio no se basa en HTTP o HTTPS, “?wsdl” se omite.|  
|httpsGetUrl|URI que especifica la dirección en la que se publican los metadatos para la recuperación mediante una solicitud HTTPS\/Get.|  
|policyVersion|Una cadena que especifica la versión de la especificación WS\-Policy que se va a usar.  Este atributo es del tipo <xref:System.ServiceModel.Description.PolicyVersion>.|  
  
### Elementos secundarios  
 Ninguna  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<comportamiento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Especifica un elemento de comportamiento.|  
  
## Comentarios  
 Este elemento de configuración permite controlar los metadatos que publican características de un servicio.  Para evitar la divulgación involuntaria de metadatos de servicio con información confidencial potencial, la configuración predeterminada para los servicios [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] deshabilita la publicación de metadatos.  Este comportamiento es seguro de forma predeterminada, pero también quiere decir que no puede usar una herramienta de importación de metadatos \(como Svcutil.exe\) Para compilar el código de cliente necesario para llamar al servicio a menos que el comportamiento de publicación de metadatos del servicio se habilite de manera explícita en la configuración.  Con este elemento de configuración, puede habilitar este comportamiento de publicación para su servicio.  
  
 Para obtener un ejemplo detallado del código para configurar este comportamiento, vea [Comportamiento de publicación de metadatos](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md).  
  
 Los atributos `httpsGetBinding` y `httpGetBinding` opcionales le permiten configurar los enlaces utilizados para la recuperación de metadatos a través de HTTP GET \(o HTTPS GET\).  Si no se especifican, los enlaces predeterminados \(`HttpTransportBindingElement`, en el caso de HTTP y `HttpsTransportBindingElement`, en el caso de HTTPS\) se utilizan según corresponda para la recuperación de metadatos.  Observe que no puede utilizar estos atributos con los enlaces WCF integrados.  Solo se admitirán los enlaces con elementos de enlace internos que admiten <xref:System.ServiceModel.Channels.IReplyChannel>.  Además, la propiedad <xref:System.ServiceModel.Channels.MessageVersion%2A> del enlace debe ser <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.  
  
 Para reducir la exposición de un servicio a los usuarios malintencionados, es posible proteger la transferencia mediante el mecanismo SSL sobre HTTP \(HTTPS\).  Para realizar esto, debe enlazar primero un certificado X.509 adecuado a un puerto concreto en el equipo que esté hospedando el servicio.  \([!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).\) Segundo, agregue este elemento a la configuración de servicio y establezca el atributo `httpsGetEnabled` en `true`.  Finalmente, establezca el atributo `httpsGetUrl` en la dirección URL del extremo de metadatos del servicio, tal y como se muestra en el ejemplo siguiente.  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## Ejemplo  
 El ejemplo siguiente configura un servicio para exponer los metadatos mediante el elemento \<serviceMetadata\>.  También configura un extremo para exponer el contrato `IMetadataExchange` como una implementación de un protocolo WS\-MetadataExchange \(MEX\).  El ejemplo usa `mexHttpBinding`, que es un enlace estándar de conveniencia equivalente a `wsHttpBinding` con el modo de seguridad establecido en `None`.  Se utiliza una dirección relativa de "mex" en el extremo que, cuando se resuelve con los resultados de la dirección base de los servicios resulta en una dirección de extremo de http:\/\/localhost\/servicemodelsamples\/service.svc\/mex.  
  
```  
<configuration>  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc  -->  
      <endpoint address=""  
                binding="wsHttpBinding"  
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex   
           To expose the IMetadataExchange contract, you   
           must enable the serviceMetadata behavior as demonstrated below -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <!-- The serviceMetadata behavior publishes metadata through   
             the IMetadataExchange contract. When this behavior is   
             present, you can expose this contract through an endpoint   
             as shown above. Setting httpGetEnabled to true publishes   
             the service's WSDL at the <baseaddress>?wsdl  
             eg. http://localhost/servicemodelsamples/service.svc?wsdl -->  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
</configuration>  
```  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.ServiceMetadataPublishingElement>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Comportamiento de publicación de metadatos](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)