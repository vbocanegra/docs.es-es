---
title: "Elemento &lt;authentication&gt; de &lt;serviceCertificate&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 733b67b4-08a1-4d25-9741-10046f9357ef
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Elemento &lt;authentication&gt; de &lt;serviceCertificate&gt;
Especifica la configuración utilizada por el proxy del cliente para autenticar certificados del servicio que se obtienen utilizando la negociación de SSL\/TLS.  
  
## Sintaxis  
  
```  
  
<authentication customCertificateValidatorType="String" certificateValidationMode="None/PeerTrust/ChainTrust/PeerOrChainTrust/Custom"  
revocationMode="NoCheck/Online/Offline"   
trustedStoreLocation="LocalMachine/CurrentUser" />  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|customCertificateValidatorType|Cadena.  Tipo y ensamblado utilizados para validar un tipo personalizado.|  
|certificateValidationMode|Especifica uno de los tres modos utilizados para validar las credenciales.  Si se establece en `Custom`, también debe proporcionarse un customCertificateValidator.  De manera predeterminada, es `ChainTrust`.|  
|revocationMode|Uno de los modos utilizados para comprobar listas de certificados revocadas \(CRL\).  De manera predeterminada, es `Online`.|  
|trustedStoreLocation|Una de las dos ubicaciones de almacenamiento del sistema: `LocalMachine` o `CurrentUser`.  Se utiliza este valor cuando un certificado del servicio se negocia al cliente.  La validación se realiza contra el **Personas de confianza** almacén en la ubicación del almacén especificada.  De manera predeterminada, es `CurrentUser`.|  
  
## Atributo customCertificateValidator  
  
|Valor|Descripción|  
|-----------|-----------------|  
|String|Especifica el nombre de tipo y el ensamblado y otros datos utilizados para buscar el tipo.|  
  
## Atributo certificateValidationMode  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los valores siguientes: None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom.<br /><br /> Para obtener más información, consulta [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Atributo revocationMode  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los valores siguientes: NoCheck, Online, Offline.<br /><br /> Para obtener más información, consulta [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Atributo trustedStoreLocation  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Enumeración|Uno de los valores siguientes: LocalMachine o CurrentUser.  El valor predeterminado es CurrentUser.  Si la aplicación cliente se está ejecutando bajo una cuenta del sistema, entonces el certificado está normalmente en LocalMachine.  Si la aplicación cliente se está ejecutando en una cuenta de usuario, entonces el certificado se encuentra normalmente en CurrentUser.|  
  
### Elementos secundarios  
 Ninguno.  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)|Especifica el certificado que se va a utilizar al autenticar un servicio al cliente.|  
  
## Comentarios  
 El atributo `certificateValidationMode` de este elemento de configuración especifica el nivel de confianza utilizado para autenticar certificados.  De forma predeterminada, el nivel se establece en `ChainTrust`, que especifica que cada certificado debe encontrarse en una jerarquía de certificados que finalizan en una entidad emisora de certificados de confianza en la parte superior de la cadena.  Este es el modo más seguro.  También puede establecer el valor en `PeerOrChainTrust`, que especifica que los certificados autoemitidos \(confianza del mismo nivel\) se aceptan, así como los certificados que están en una cadena de confianza.  Se utiliza este valor cuando se desarrollan y depuran clientes y servicios porque los certificados autoemitidos no necesitan adquirirse desde una autoridad de confianza.  Al implementar un cliente, utilice en su lugar el valor `ChainTrust`.  También puede establecer el valor como `Custom` o `None`.  Para utilizar el valor `Custom`, también debe establecer el atributo `customCertificateValidator` en un ensamblado y tipo utilizado para validar el certificado.  Para crear su propio validador personalizado, debe heredar a partir de la clase abstracta X509CertificateValidator.  Para obtener más información, consulta [Cómo crear un servicio que emplee un validador de certificado personalizado](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
 El atributo `revocationMode` especifica cómo se comprueba la revocación de los certificados.  El valor predeterminado es `online` que indica que se comprobará automáticamente la revocación de los certificados.  Para obtener más información, consulta [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## Ejemplo  
 El siguiente ejemplo realiza dos tareas:  Especifica primero un certificado del servicio para que el cliente lo utilice al comunicarse con extremos cuyo nombre de dominio es www.contoso.com sobre el protocolo HTTP.  En segundo lugar, especifica el modo de revocación y ubicación del almacén utilizado durante la autenticación.  
  
```  
<serviceCertificate>  
  <defaultCertificate findValue="www.contoso.com"   
                      storeLocation="LocalMachine"  
                      storeName="TrustedPeople"   
                      x509FindType="FindByIssuerDistinguishedName" />  
  <scopedCertificates>  
     <add targetUri="http://www.contoso.com"   
          findValue="www.contoso.com" storeLocation="LocalMachine"  
                  storeName="Root" x509FindType="FindByIssuerName" />  
  </scopedCertificates>  
  <authentication revocationMode="Online"   
   trustedStoreLocation="LocalMachine" />  
</serviceCertificate>  
```  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.Authentication%2A>   
 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>   
 [Comportamientos de seguridad](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Trabajar con certificados](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Cómo crear un servicio que emplee un validador de certificado personalizado](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)   
 [\<authentication\>](../../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)   
 [Protección de clientes](../../../../../docs/framework/wcf/securing-clients.md)   
 [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)