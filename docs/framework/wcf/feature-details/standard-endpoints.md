---
title: "Extremos est&#225;ndar | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3fcb4225-addc-44f2-935d-30e4943a8812
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Extremos est&#225;ndar
Los extremos se definen mediante la especificación de una dirección, un enlace y un contrato.Otros parámetros que se pueden establecer en un extremo incluyen la configuración del comportamiento, los encabezados y los URI de escucha.Para ciertos tipos de extremos, estos valores no cambian.Por ejemplo, los extremos de intercambio de metadatos siempre utilizan el contrato <xref:System.ServiceModel.Description.IMetadataExchange>.Otros extremos, como <xref:System.ServiceModel.Web.WebHttpEndpoint>, siempre requieren un comportamiento de extremo especificado.La utilidad de un extremo se puede mejorar teniendo extremos con valores predeterminado para las propiedades de extremo utilizadas normalmente.Los extremos estándar permiten a un desarrollador definir un extremo que tenga los valores predeterminados o en el que una o más propiedades del extremo no cambien.Estos extremos le permiten utilizar un extremo de este tipo sin tener que especificar información de tipo estático.Los extremos estándar se pueden usar para extremos de la aplicación y de la infraestructura.  
  
## Extremos de infraestructura  
 Un servicio puede exponer extremos con algunas de las propiedades no implementadas de forma explícita por el autor del servicio.Por ejemplo, el extremo del intercambio de metadatos expone el contrato <xref:System.ServiceModel.Description.IMetadataExchange> pero, como autor del servicio, no implementa esa interfaz, pues la implementa WCF.Estos extremos de infraestructura tienen valores predeterminados para una o más propiedades de extremo, algunos de los cuales pueden ser inalterables.La propiedad <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A> del extremo del intercambio de metadatos debe ser <xref:System.ServiceModel.Description.IMetadataExchange>, mientras que el desarrollador puede proporcionar otras propiedades, como el enlace.Los extremos de la infraestructura se identifican estableciendo la propiedad <xref:System.ServiceModel.Description.ServiceEndpoint.IsSystemEndpoint%2A> en `true`.  
  
## Extremos de la aplicación  
 Los desarrolladores de la aplicación pueden definir sus propios extremos estándar que especifican los valores predeterminados para la dirección, el enlace o el contrato.Defina un extremo estándar derivando una clase de <xref:System.ServiceModel.Description.ServiceEndpoint> y estableciendo las propiedades de extremo adecuadas.Puede proporcionar valores predeterminados a propiedades que se pueden cambiar.Otras propiedades tendrán valores estáticos que no podrán cambiar.En el siguiente ejemplo, se muestra cómo implementar un extremo estándar.  
  
```  
public class CustomEndpoint : ServiceEndpoint  
    {  
        public CustomEndpoint()  
            : this(string.Empty)  
        {  
        }  
  
        public CustomEndpoint(string address)  
            : this(address, ContractDescription.GetContract(typeof(ICalculator)))  
        {  
        }  
  
        // Create the custom endpoint with a fixed binding  
        public CustomEndpoint(string address, ContractDescription contract)  
            : base(contract)  
        {  
            this.Binding = new BasicHttpBinding();  
            this.IsSystemEndpoint = false;  
        }  
  
        // Definition of the additional property of this endpoint  
        public bool Property  
        {  
            get;  
            set;  
        }  
    }  
```  
  
 Para utilizar un extremo personalizado definido por el usuario en un archivo de configuración, debe derivar una clase de <xref:System.ServiceModel.Configuration.StandardEndpointElement>, derivar una clase de <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement> y registrar el nuevo extremo estándar en la sección de extensiones en app.config o en machine.config.La clase <xref:System.ServiceModel.Configuration.StandardEndpointElement> proporciona el soporte técnico de configuración para el extremo estándar, tal y como se muestra en el siguiente ejemplo.  
  
```  
public class CustomEndpointElement : StandardEndpointElement  
    {  
        // Definition of the additional property for the standard endpoint element  
        public bool Property  
        {  
            get { return (bool)base["property"]; }  
            set { base["property"] = value; }  
        }  
  
        // The additional property needs to be added to the properties of the standard endpoint element  
        protected override ConfigurationPropertyCollection Properties  
        {  
            get  
            {  
                ConfigurationPropertyCollection properties = base.Properties;  
                properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));  
                return properties;  
            }  
        }  
  
        // Return the type of this standard endpoint  
        protected override Type EndpointType  
        {  
            get { return typeof(CustomEndpoint); }  
        }  
  
        // Create the custom service endpoint  
        protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)  
        {  
            return new CustomEndpoint();  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)  
        {  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)  
        {  
        }  
    }  
  
```  
  
 La clase <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement> proporciona el tipo de apoyo para la recopilación que aparece en la sección \<`standardEndpoints`\> de la configuración correspondiente al extremo estándar.En el siguiente ejemplo, se muestra cómo implementar esta clase.  
  
```  
public class CustomEndpointCollectionElement : StandardEndpointCollectionElement<CustomEndpoint, CustomEndpointElement>  
    {  
         // ...  
  
    }  
```  
  
 En el siguiente ejemplo, se muestra cómo registrar un extremo estándar en la sección de extensiones.  
  
```  
<extensions>  
      <standardEndpointExtensions>  
        <add  
          name="customStandardEndpoint"  
          type="CustomEndpointCollectionElement, Example.dll,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>  
  
```  
  
## Configurar un extremo estándar  
 Los extremos estándar se pueden agregar en código o en configuración.Para agregar un extremo estándar en código, basta con crear instancias del tipo de extremo estándar adecuado y agregarlo al host del servicio, tal y como se muestra en el siguiente ejemplo:  
  
```csharp  
serviceHost.AddServiceEndpoint(new CustomEndpoint());  
```  
  
 Para agregar un extremo estándar en configuración, agregue un elemento \<`endpoint`\> al elemento \<`service`\> y cualquier configuración necesitada en el elemento \<`standardEndpoints`\>.En el siguiente ejemplo, se muestra cómo agregar <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, uno de los extremos estándar que se distribuye con [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
```xml  
<services>  
  <service>  
    <endpoint isSystemEndpoint=”true” kind=”udpDiscoveryEndpoint” />  
  </service>  
</services>  
<standardEndpoints>    
  <udpDiscoveryEndpoint>  
     <standardEndpoint multicastAddress="soap.udp://239.255.255.250:3702" />   
  </udpDiscoveryEndpoint>  
</ standardEndpoints >  
```  
  
 El tipo de extremo estándar se especifica mediante el atributo de clase en el elemento \<`endpoint`\>.El extremo se configura dentro del elemento \<`standardEndpoints`\>.En el ejemplo anterior, se agrega y se configura un extremo de <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.El elemento \<`udpDiscoveryEndpoint`\> contiene un \<`standardEndpoint`\> que establece la propiedad <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint.MulticastAddress%2A> de <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.  
  
## Extremos estándar distribuidos con .NET Framework  
 En la siguiente tabla, se muestra una lista de los extremos estándar distribuidos con [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
 `Mex Endpoint`  
 Un extremo estándar que se usa para exponer metadatos del servicio.  
  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
 Un extremo estándar que usan los servicios para enviar mensajes del anuncio.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
 Un extremo estándar que usan los servicios para enviar mensajes de la detección.  
  
 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
 Un extremo estándar que se pre\-configura para las operaciones de detección en un enlace de multidifusión de UDP.  
  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
 Un extremo estándar que usan los servicios para enviar mensajes de anuncio en un enlace de UDP.  
  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
 Un extremo estándar que utiliza detección del WS\-Discovery para encontrar la dirección del extremo en el tiempo de ejecución de forma dinámica.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataEndpoint>  
 Un extremo estándar para el intercambio de metadatos.  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>  
 Un extremo estándar con un enlace <xref:System.ServiceModel.WebHttpBinding> que agrega automáticamente el comportamiento <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
 <xref:System.ServiceModel.Description.WebScriptEndpoint>  
 Un extremo estándar con un enlace <xref:System.ServiceModel.WebHttpBinding> que agrega automáticamente el comportamiento <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.  
  
 <xref:System.ServiceModel.Description.WebServiceEndpoint>  
 Un extremo estándar con un enlace <xref:System.ServiceModel.WebHttpBinding>.  
  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>  
 Un extremo estándar que le permite llamar a las operaciones de control en instancias de flujo de trabajo.  
  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>  
 Un extremo estándar que admite la creación de flujo de trabajo y la reanudación del marcador.