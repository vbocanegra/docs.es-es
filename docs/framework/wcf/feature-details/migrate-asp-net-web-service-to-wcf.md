---
title: "C&#243;mo migrar el c&#243;digo del servicio web ASP.NET a Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e528c64f-c027-4f2e-ada6-d8f3994cf8d6
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# C&#243;mo migrar el c&#243;digo del servicio web ASP.NET a Windows Communication Foundation
El procedimiento siguiente describe cómo migrar un servicio web ASP.NET a [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## Procedimiento  
  
#### Para migrar un servicio web ASP.NET a WCF  
  
1.  Asegúrese de que existe un conjunto completo de pruebas para el servicio.  
  
2.  Genere el WSDL del servicio y guarde una copia en la misma carpeta que el archivo .asmx del servicio.  
  
3.  Actualice el servicio Web ASP.NET para que pueda usar .NET 2.0.  Primero implemente .NET Framework 2.0 para la aplicación en IIS y, a continuación, use Visual Studio 2005 para automatizar el proceso de conversión de código, tal como se explica en [Guía detallada para convertir proyectos web de Visual Studio .NET 2002\/2003 a Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=96492).  Ejecute el conjunto de pruebas.  
  
4.  Proporcione los valores explícitos para `Namespace` y los parámetros `Name` de los atributos <xref:System.Web.Services.WebService>, si aún no se han proporcionado.  Repita la acción para el parámetro `MessageName` de <xref:System.Web.Services.WebMethodAttribute>.  Si aún no se han proporcionado los valores explícitos de los encabezados HTTP de SOAPAction mediante los cuales se enrutan las solicitudes a los métodos, especifique explícitamente el valor predeterminado del parámetro `Action` con <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute>.  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              double sum = 0.00;  
              foreach (double inputValue in input.Input)  
              {  
                  sum += inputValue;  
              }  
          return sum;  
         }  
    }  
    ```  
  
5.  Pruebe el cambio.  
  
6.  Mueva cualquier código sustantivo de los cuerpos de los métodos de la clase, a una clase distinta a la que utiliza la clase original.  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
    }  
  
    internal class ActualAdder  
    {  
         internal double Add(SumInput input)  
         {  
              double sum = 0.00;  
              foreach (double inputValue in input.Input)  
              {  
                  sum += inputValue;  
              }  
          return sum;  
         }  
    }  
    ```  
  
7.  Pruebe el cambio.  
  
8.  Agregue las referencias de los ensamblados System.ServiceModel y System.Runtime.Serialization [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] al proyecto de servicio web ASP.NET.  
  
9. Ejecute [Herramienta de utilidad de metadatos de ServiceModel \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) para generar una clase de cliente [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] del WSDL.  Agregue el módulo de clase generado a la solución.  
  
10. El módulo de clase generado en el paso anterior contiene la definición de una interfaz.  
  
    ```  
    [System.ServiceModel.ServiceContractAttribute()]  
    public interface AdderSoap  
    {  
         [System.ServiceModel.OperationContractAttribute(  
          Action="http://tempuri.org/Add",   
          ReplyAction="http://tempuri.org/Add")]  
         AddResponse Add(AddRequest request);  
    }  
    ```  
  
     Modifique la definición de la clase de servicio web ASP.NET para definir la clase como implementación de esa interfaz, como muestra el código siguiente.  
  
    ```  
    [WebService(Namespace = "http://tempuri.org/", Name = "Adder")]  
    public class Adder: AdderSoap  
    {  
         [WebMethod(MessageName = "Add")]  
         [SoapDocumentMethod(Action = "http://tempuri.org/Add")]  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
  
         public AddResponse Add(AddRequest request)  
         {  
            return new AddResponse(  
            new AddResponseBody(  
            this.Add(request.Body.input)));  
         }  
    }  
    ```  
  
11. Compile el proyecto.  Pueden producirse errores debido a que el código generado en el paso nueve duplicó algunas definiciones de tipo.  Repare esos errores, normalmente eliminando las definiciones de los tipos existentes anteriormente.  Pruebe el cambio.  
  
12. Quite los atributos específicos de ASP.NET, como <xref:System.Web.Services.WebService>, <xref:System.Web.Services.WebMethodAttribute> y <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute>.  
  
    ```  
    public class Adder: AdderSoap  
    {  
         public double Add(SumInput input)  
         {  
              return new ActualAdder().Add(input);  
         }  
  
         public AddResponse Add(AddRequest request)  
         {  
              return new AddResponse(  
             new AddResponseBody(  
            this.Add(request.Body.input)));  
         }  
    }  
    ```  
  
13. Configure la clase, que ahora es un tipo de servicio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], para exigir el modo de compatibilidad de ASP.NET [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si el servicio web ASP.NET se basa en alguno de los siguientes:  
  
    -   La clase <xref:System.Web.HttpContext>.  
  
    -   Los perfiles ASP.NET  
  
    -   Las listas ACL en archivos .asmx.  
  
    -   Las opciones de autenticación de IIS.  
  
    -   Las opciones de suplantación de ASP.NET  
  
    -   La globalización de ASP.NET  
  
    ```  
    [System.ServiceModel.AspNetCompatibilityRequirements(  
      RequirementsMode=AspNetCompatbilityRequirementsMode.Required)]  
    public class Adder: AdderSoap  
    ```  
  
14. Cambie el nombre del archivo .asmx original a .asmx .old.  
  
15. Cree un archivo de servicio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con la extensión .asmx y guárdelo en la raíz de la aplicación en IIS.  
  
    ```  
    <%@Service Class="MyOrganization.Adder" %>  
    <%@Assembly Name="MyServiceAssembly" %>   
    ```  
  
16. Agregue una configuración [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] para el servicio a su archivo Web.config.  Configure el servicio para utilizar [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), para utilizar el archivo de servicio con la extensión .asmx, creado en los pasos anteriores, y para no generar WSDL para sí mismo sino utilizar el WSDL del paso dos.  Configúrelo también para utilizar el modo de compatibilidad de ASP.NET, si fuese necesario.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
     <system.web>  
      <compilation>  
      <buildProviders>  
       <remove extension=".asmx" />  
       <add extension=".asmx"   
        type=  
        "System.ServiceModel.Activation.ServiceBuildProvider,  
        T:System.ServiceModel, Version=2.0.0.0,   
       Culture=neutral,   
       PublicKeyToken=b77a5c561934e089" />  
      </buildProviders>  
      </compilation>  
     </system.web>  
     <system.serviceModel>  
      <services>  
      <service name="MyOrganization.Adder "  
        behaviorConfiguration="AdderBehavior">  
       <endpoint   
        address="”  
        binding="basicHttpBinding"  
        contract="AdderSoap "/>  
       </service>  
      </services>  
      <behaviors>  
      <behavior name="AdderBehavior">  
       <metadataPublishing   
        enableMetadataExchange="true"   
        enableGetWsdl="true"   
        enableHelpPage="true"   
        metadataLocation=  
        "http://MyHost.com/AdderService/Service.WSDL"/>  
      </behavior>  
      </behaviors>  
      <serviceHostingEnvironment   
       aspNetCompatibilityEnabled ="true"/>  
     </system.serviceModel>  
    </configuration>  
  
    ```  
  
17. Guarde la configuración.  
  
18. Compile el proyecto.  
  
19. Ejecute el conjunto de pruebas para asegurarse de que todos los cambios funcionan.  
  
## Vea también  
 [Cómo: Migrar el código de cliente de servicio web ASP.NET a Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/migrate-asp-net-web-service-client-to-wcf.md)