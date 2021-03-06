---
title: "&lt;localIssuer&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26bdd0df-0e7d-4b9e-bbeb-f28c53769385
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;localIssuer&gt;
Especifica la dirección y el enlace del emisor local que se van a usar para obtener un token de seguridad.  
  
## Sintaxis  
  
```  
  
<localIssuer address="string"  
      binding="string"  
      bindingConfiguration="string" />  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|address|Cadena necesaria.  Especifica el URI del emisor local.|  
|enlace|Cadena opcional.  Uno de los enlaces proporcionados por el sistema.  Para obtener una lista, vea [Enlaces proporcionados por el sistema](../../../../../docs/framework/wcf/system-provided-bindings.md).|  
|bindingConfiguration|Cadena opcional.  Especifica una configuración de enlace situada en el archivo de configuración.|  
  
### Elementos secundarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<identidad\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Especifica la información de identidad para el emisor local.|  
|[\<encabezados\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|Colección de encabezados de dirección necesaria para poder direccionar el emisor local correctamente.  Puede utilizar la palabra clave `add` para agregar un encabezado a esta colección.|  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<issuedToken\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)|Especifica un token personalizado usado para autenticar un cliente en un servicio.|  
  
## Comentarios  
 Al obtener un token emitido de un Servicio de token de seguridad  \(STS\), la aplicación cliente se debe configurar con el enlace y la dirección que se van a usar para comunicarse con el STS.  Cuando <xref:System.ServiceModel.WSFederationHttpBinding> no proporciona una dirección URL para el servicio de token de seguridad, o cuando la dirección del emisor de un enlace aliado es http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous o `null`, el canal de [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] del cliente utiliza los valores especificados por `address` y `binding` para comunicarse con STS y obtener el token emitido.  Para obtener más información sobre cómo configurar un emisor local, vea [Cómo: Configurar un emisor local](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
## Ejemplo  
 El ejemplo siguiente establece `address`, `binding`y atributos `bindingConfiguration` de un elemento `localIssuer`.  
  
```  
<system.serviceModel>  
 <behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <issuedToken cacheIssuedTokens="false"   
                 defaultKeyEntropyMode="ClientEntropy">  
     <localIssuer address="net.tcp://cohowinery/tokens"   
                  binding="netTcpBinding"  
                  bindingConfiguration="myTcpBindingConfig" />  
    </issuedToken>  
   </clientCredentials>  
  </behavior>  
  </endpointBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.LocalIssuer%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>   
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>   
 [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Cómo: Configurar un emisor local](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)   
 [Identidad del servicio y autenticación](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Protección de clientes](../../../../../docs/framework/wcf/securing-clients.md)   
 [Cómo crear un cliente federado](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Federación y tokens emitidos](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)