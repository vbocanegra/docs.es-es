---
title: "Operaciones de servicio (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "HTML"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "operaciones de servicio [WCF Data Services]"
  - "Servicios de datos de Microsoft WCF, operaciones de servicio"
ms.assetid: 583a690a-e60f-4990-8991-d6efce069d76
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Operaciones de servicio (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] le permite definir operaciones de servicio en un servicio de datos para exponer métodos del servidor.  Las operaciones de servicio se direccionan como los demás recursos del servicio de datos, mediante los URI.  Las operaciones de servicio le permiten exponer la lógica de negocios de un servicio de datos; por ejemplo, implementar la lógica de validación, aplicar la seguridad basada en roles o exponer capacidades de consulta especializadas.  Las operaciones de servicio son métodos agregados a la clase de servicio de datos que deriva de <xref:System.Data.Services.DataService%601>. Al igual que otros recursos de servicio de datos, puede proporcionar los parámetros al método de la operación de servicio. Por ejemplo, el siguiente URI de operación de servicio \(basado en el servicio de datos [quickstart](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)\) pasa el valor `London` al parámetro `city`:  
  
```  
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'  
```  
  
 La definición de esta operación de servicio es la siguiente:  
  
 [!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationdef)]
 [!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationdef)]  
  
 Puede usar la propiedad <xref:System.Data.Services.DataService%601.CurrentDataSource%2A> de la clase <xref:System.Data.Services.DataService%601> para tener acceso directo al origen de datos que está usando el servicio de datos.  Para obtener más información, consulta [Cómo: Definir una operación de servicio](../../../../docs/framework/data/wcf/how-to-define-a-service-operation-wcf-data-services.md).  
  
 Para obtener información sobre cómo llamar a una operación de servicio desde una aplicación cliente de .NET Framework, vea [Operaciones de servicio de llamada](../../../../docs/framework/data/wcf/calling-service-operations-wcf-data-services.md).  
  
## Requisitos que deben cumplir las operaciones de servicio  
 Al definir operaciones de servicio en el servicio de datos deben tenerse en cuenta los requisitos siguientes.  Si un método no los cumple, no se expondrá como operación de servicio para el servicio de datos.  
  
-   La operación debe ser un método de instancia pública que sea miembro de la clase del servicio de datos.  
  
-   El método de la operación solo puede aceptar parámetros de entrada.  El servicio de datos no puede tener acceso a los datos enviados en el cuerpo del mensaje.  
  
-   Si se definen parámetros, el tipo de cada parámetro debe ser un tipo primitivo.  Cualquier dato de un tipo no primitivo se debe serializar y pasar a un parámetro de cadena.  
  
-   El método debe devolver uno de los elementos siguientes:  
  
    -   `void` \(`Nothing` en Visual Basic\)  
  
    -   <xref:System.Collections.Generic.IEnumerable%601>  
  
    -   <xref:System.Linq.IQueryable%601>  
  
    -   Un tipo de entidad en el modelo de datos expuesto por el servicio de datos.                  ``  
  
    -   Una clase primitiva como entero o cadena.  
  
-   Para admitir opciones de consulta como ordenaciones, paginaciones y filtrados, los métodos de las operaciones de servicio deben devolver <xref:System.Linq.IQueryable%601>.  Las solicitudes a operaciones de servicio que incluyen opciones de consulta se rechazan para las operaciones que solo devuelven <xref:System.Collections.Generic.IEnumerable%601>.  
  
-   Para que se pueda tener acceso a las entidades relacionadas usando las propiedades de navegación, la operación de servicio debe devolver <xref:System.Linq.IQueryable%601>.  
  
-   El método se debe anotar con el atributo `[WebGet]` o `[WebInvoke]`.  
  
    -   `[WebGet]` permite invocar el método usando una solicitud GET.  
  
    -   `[WebInvoke(Method = "POST")]` permite invocar el método usando una solicitud POST.  No se admiten otros métodos <xref:System.ServiceModel.Web.WebInvokeAttribute>.  
  
-   Una operación de servicio se puede anotar con el elemento <xref:System.Data.Services.SingleResultAttribute> que especifica que el valor devuelto desde el método es una sola entidad en vez de una colección de entidades.  Esta distinción dicta la serialización resultante de la respuesta y la manera en que se representan en el URI los recorridos de las propiedades de navegación adicionales.  Por ejemplo, cuando use la serialización AtomPub, una sola instancia de tipo de recurso se representa como elemento de entrada y un conjunto de instancias como elemento feed.  
  
## Direccionamiento de las operaciones de servicio  
 Puede direccionar las operaciones de servicio colocando el nombre del método en el primer segmento de la ruta de acceso de un URI.  Como ejemplo, el siguiente URI tiene acceso a una operación `GetOrdersByState` que devuelve una colección <xref:System.Linq.IQueryable%601> de objetos `Orders`.  
  
```  
http://localhost:12345/Northwind.svc/GetOrdersByState?state='CA'&includeItems=true  
```  
  
 Al llamar a una operación de servicio, los parámetros se proporcionan como opciones de consulta.  La operación de servicio anterior acepta tanto un parámetro de cadena `state` como un parámetro booleano `includeItems` que indica si se van a incluir objetos `Order_Detail` relacionados en la respuesta.  
  
 A continuación se enumeran los tipos de valor devueltos válidos para una operación de servicio:  
  
|Tipos de valor devueltos válidos|Reglas que deben cumplir los URI|  
|--------------------------------------|--------------------------------------|  
|`void` \(`Nothing` en Visual Basic\)<br /><br /> o bien<br /><br /> Tipos de entidad<br /><br /> o bien<br /><br /> Tipos primitivos|El URI debe ser un solo segmento de ruta de acceso que sea el nombre de la operación de servicio.  No se permiten las opciones de consulta.|  
|<xref:System.Collections.Generic.IEnumerable%601>|El URI debe ser un solo segmento de ruta de acceso que sea el nombre de la operación de servicio.  Puesto que el tipo de resultado no es un tipo <xref:System.Linq.IQueryable%601>, no se permiten las opciones de consulta.|  
|<xref:System.Linq.IQueryable%601>|Se permiten segmentos de ruta de acceso de la consulta además de la ruta de acceso que es el nombre de la operación de servicio.  También se permiten las opciones de consulta.|  
  
 Se pueden agregar segmentos de ruta de acceso u opciones de consulta adicionales al URI en función del tipo de valor devuelto de la operación de servicio.  Por ejemplo, el URI siguiente tiene acceso a una operación `GetOrdersByCity` que devuelve una colección <xref:System.Linq.IQueryable%601> de objetos `Orders`, ordenada en orden descendente por `RequiredDate`, junto con los objetos `Order_Details` relacionados:  
  
```  
http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc  
  
```  
  
## Control de acceso a las operaciones de servicio  
 El método <xref:System.Data.Services.IDataServiceConfiguration.SetServiceOperationAccessRule%2A> de la clase <xref:System.Data.Services.IDataServiceConfiguration> controla la visibilidad en el ámbito de todos los servicios de las operaciones de servicio, de la misma forma que el método <xref:System.Data.Services.IDataServiceConfiguration.SetEntitySetAccessRule%2A> controla la visibilidad del conjunto de entidades.  Por ejemplo, la línea de código siguiente de la definición del servicio de datos permite el acceso a la operación de servicio `CustomersByCity`.  
  
 [!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationconfig)]
 [!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationconfig)]  
  
> [!NOTE]
>  Si una operación de servicio tiene un tipo de valor devuelto que se oculta restringiendo el acceso en los conjuntos de entidades subyacentes, la operación de servicio no estará disponible para las aplicaciones cliente.  
  
 Para obtener más información, consulta [Cómo: Definir una operación de servicio](../../../../docs/framework/data/wcf/how-to-define-a-service-operation-wcf-data-services.md).  
  
## Producir excepciones  
 Recomendamos usar la clase <xref:System.Data.Services.DataServiceException> cada vez que produzca una excepción en la ejecución del servicio de datos.  Esto es porque el tiempo de ejecución del servicio de datos sabe cómo asignar correctamente propiedades de este objeto de excepción al mensaje de respuesta HTTP.  Al generar una <xref:System.Data.Services.DataServiceException> en una operación de servicio, la excepción devuelta está contenida en <xref:System.Reflection.TargetInvocationException>.  Para devolver la <xref:System.Data.Services.DataServiceException> base sin la <xref:System.Reflection.TargetInvocationException> envolvente, debe invalidar el método <xref:System.Data.Services.DataService%601.HandleException%2A> en <xref:System.Data.Services.DataService%601>, extraer <xref:System.Data.Services.DataServiceException> de <xref:System.Reflection.TargetInvocationException> y devolverlo como el error de nivel superior, como en el siguiente ejemplo:  
  
 [!code-csharp[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#handleexceptions)]
 [!code-vb[Astoria Northwind Service#HandleExceptions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#handleexceptions)]  
  
## Vea también  
 [Interceptores](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md)