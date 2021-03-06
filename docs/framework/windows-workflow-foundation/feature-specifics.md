---
title: "Detalles de las caracter&#237;sticas de Windows Workflow Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Detalles de las caracter&#237;sticas de Windows Workflow Foundation
[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] agrega una serie de características a Windows Workflow Foundation.Este documento describe algunas de las nuevas características y proporciona detalles sobre los escenarios en que pueden ser útiles.  
  
## Actividades de mensajería  
 Las actividades de mensajería \(<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, <xref:System.ServiceModel.Activities.Send> y  <xref:System.ServiceModel.Activities.ReceiveReply>\) se utilizan para enviar y recibir mensajes de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] desde el flujo de trabajo. Las actividades <xref:System.ServiceModel.Activities.SendReply> y <xref:System.ServiceModel.Activities.Receive> se utilizan para formar una operación de servicio de [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] que se expone a través de WSDL como servicios Web de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] estándar. <xref:System.ServiceModel.Activities.Send> y <xref:System.ServiceModel.Activities.ReceiveReply> sirven para utilizar un servicio Web similar a un elemento <xref:System.ServiceModel.ChannelFactory> de WCF; también existe una experiencia de **Agregar referencia de servicio** para Workflow Foundation que genera actividades preconfiguradas.  
  
### Introducción a las actividades de mensajería  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree un proyecto de aplicación de servicio de flujo de trabajo WCF.Se colocará un par <xref:System.ServiceModel.Activities.Receive> y <xref:System.ServiceModel.Activities.SendReply> en el lienzo.  
  
-   Haga clic con el botón secundario en el proyecto y seleccione **Agregar referencia de servicio**. Señale un WSDL de servicio Web existente y haga clic en **Aceptar**. Compile el proyecto para que se muestren las actividades generadas \(se implementan utilizando <xref:System.ServiceModel.Activities.Send> y <xref:System.ServiceModel.Activities.ReceiveReply>\) en el cuadro de herramientas.  
  
-   Los ejemplos para estas actividades se pueden encontrar en las siguientes secciones:  
  
    -   Básico: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Escenarios: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
-   [Documentación conceptual](http://go.microsoft.com/fwlink/?LinkId=204801)  
  
-   [Documentación del diseñador de actividades de mensajería](http://go.microsoft.com/fwlink/?LinkId=204802)  
  
### Escenario de ejemplo de actividades de mensajería  
 Un servicio `BestPriceFinder` llama a varios servicios de líneas aéreas para encontrar el mejor precio de billete para una ruta determinada. La implementación de este escenario requeriría utilizar las actividades de mensaje para recibir la solicitud de precios, recuperar los precios de los servicios back\-end y responder a la solicitud de precios con el mejor precio. También requeriría utilizar otras actividades para uso inmediato con el fin de crear la lógica de negocios para calcular el mejor precio.  
  
## WorkflowServiceHost  
 <xref:System.ServiceModel.WorkflowServiceHost> es el host de flujo de trabajo para uso inmediato que admite varias instancias, configuración y mensajería de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(aunque no se requiere que los flujos de trabajo utilicen mensajería para ser hospedados\). También se integra con persistencia, seguimiento y control de instancias a través de un conjunto de comportamientos de servicio. Al igual que <xref:System.ServiceModel.ServiceHost> de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], <xref:System.ServiceModel.WorkflowServiceHost> se puede autohospedar en una aplicación de consola\/WinForms\/WPF o un servicio de Windows, u hospedarse en web \(como un archivo .xamlx\) en IIS o WAS.  
  
### Introducción a host de servicio de flujo de trabajo  
  
-   En Visual Studio 2010, cree un proyecto de aplicación de servicio de flujo de trabajo de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]: este proyecto se configurará para utilizar <xref:System.ServiceModel.WorkflowServiceHost> en un entorno de host de web.  
  
-   Para hospedar un flujo de trabajo que no sea de mensajería, agregue un elemento <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> personalizado que creará la instancia basándose en un mensaje.  
  
-   Las instancias de flujo de trabajo se pueden controlar \(por ejemplo,suspendido o terminado\) agregando <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> a <xref:System.ServiceModel.WorkflowServiceHost> y usando después <xref:System.ServiceModel.Activities.WorkflowControlClient>.  
  
-   Los ejemplos para <xref:System.ServiceModel.WorkflowServiceHost> se pueden encontrar en las siguientes secciones:  
  
    -   [Ejecución](../../../docs/framework/windows-workflow-foundation/samples/execution.md)  
  
    -   Básico: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Escenarios: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Aplicación: [Administración de instancias suspendidas](../../../docs/framework/windows-workflow-foundation/samples/suspended-instance-management.md)  
  
-   [Documentación conceptual de WorkflowServiceHost](http://go.microsoft.com/fwlink/?LinkId=204807)  
  
### Escenario de WorkflowServiceHost  
 Un servicio BestPriceFinder llama a varios servicios de líneas aéreas para encontrar el mejor precio de billete para una ruta determinada. La implementación de este escenario requeriría hospedar el flujo de trabajo en <xref:System.ServiceModel.WorkflowServiceHost>. También se utilizarían las actividades de mensaje para recibir la solicitud de precios, recuperar los precios de los servicios back\-end y responder a la solicitud de precios con el mejor precio.  
  
## Correlación  
 Una correlación es una de estas dos cosas:  
  
-   Una forma de agrupar mensajes; es decir, la relación entre un mensaje de solicitud y su respuesta.  
  
-   Una forma de asignar un fragmento de datos a una instancia de servicio.  
  
### Introducción  
  
-   Para iniciarse en la correlación, cree un nuevo proyecto en Visual Studio.Cree una variable de tipo <xref:System.ServiceModel.Activities.CorrelationHandle>.  
  
-   Un ejemplo de correlación utilizado para agrupar mensajes es una correlación solicitud\-respuesta que agrupa los mensajes.  
  
    -   En una actividad <xref:System.ServiceModel.Activities.Receive>, haga clic en la propiedad <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> y agregue un elemento <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> utilizando la variable de tipo CorrelationHandle creada anteriormente en el primer paso.  
  
    -   Cree una actividad <xref:System.ServiceModel.Activities.SendReply> haciendo clic con el botón secundario en <xref:System.ServiceModel.Activities.Receive> y haciendo clic en "Crear SendReply".Péguela en su flujo de trabajo después de la actividad <xref:System.ServiceModel.Activities.Receive>.  
  
-   Un ejemplo de asignación de un fragmento de datos a una instancia de servicio es la correlación basada en contenido que asigna un fragmento de datos \(por ejemplo, un identificador de pedido\) a una instancia de flujo de trabajo en particular.  
  
    -   En cualquier actividad de mensajería, haga clic en la propiedad `CorrelationInitializers` y agregue un elemento <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> utilizando la variable <xref:System.ServiceModel.Activities.CorrelationHandle> creada anteriormente.Haga doble clic en la propiedad deseada en el mensaje \(por ejemplo,OrderID\) en el menú desplegable.Establezca la propiedad `CorrelatesWith` en la variable <xref:System.ServiceModel.Activities.CorrelationHandle> utilizada anteriormente.  
  
-   Ejemplos:  
  
    -   Básico: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Escenarios: [Servicios](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   [Documentación conceptual de correlación](http://go.microsoft.com/fwlink/?LinkId=204939)  
  
### Escenario de correlación  
 Se utiliza un flujo de trabajo del procesamiento de pedidos para administrar la creación de nuevos pedidos y la actualización de pedidos existentes. La implementación de este escenario requeriría hospedar el flujo de trabajo en <xref:System.ServiceModel.WorkflowServiceHost> y utilizar las actividades de mensajería. También requeriría correlación basada en `orderId` para asegurarse de que las actualizaciones se realizan en el flujo de trabajo correcto.  
  
## Configuración simplificada  
 El esquema de configuración de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] es complejo y proporciona a los usuarios muchas dificultades para encontrar características.En [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], nos hemos centrado en ayudar a los usuarios de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] a configurar sus servicios con las siguientes características:  
  
-   Eliminar la necesidad de configuración por servicio explícita.Si no configura elementos \<service\> para su servicio y este no define extremos mediante programación, se agregará automáticamente al servicio un conjunto de extremos, uno por cada dirección base del servicio y por cada contrato implementado por el servicio.  
  
-   Permite al usuario definir valores predeterminados para los comportamientos y enlaces de WCF, que se aplicarán a los servicios sin ninguna configuración explícita.  
  
-   Los extremos estándar definen extremos preconfigurados reutilizables, que tienen valores fijos para una o varias propiedades de extremo \(dirección, enlace y contrato\), y permiten la definición de propiedades personalizadas.  
  
-   Finalmente, <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> permite realizar la administración central de la configuración del cliente de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], que es útil en escenarios en que la configuración se selecciona o se cambia después del tiempo de carga del dominio de aplicación.  
  
### Introducción  
  
-   [Guía del desarrollador para WCF 4.0](http://go.microsoft.com/fwlink/?LinkId=204940)  
  
-   [Generador de canales de configuración](http://go.microsoft.com/fwlink/?LinkId=204941)  
  
-   [Elemento de extremo estándar](http://go.microsoft.com/fwlink/?LinkId=204942)  
  
-   [Mejoras de la configuración de servicio en .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=204943)  
  
-   [Error común del usuario en .NET 4: escribir incorrectamente el nombre de configuración de servicio de WF\/WCF](http://go.microsoft.com/fwlink/?LinkId=204944)  
  
### Escenarios de configuración simplificados  
  
-   Un desarrollador de ASMX experimentado desea empezar a utilizar [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Sin embargo, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] parece también demasiado complicado.¿Qué es toda la información que necesito escribir en un archivo de configuración?En .NET 4, se puede decidir incluso no tener un archivo de configuración en absoluto.  
  
-   Un conjunto existente de servicios de WCF es muy difícil de configurar y mantener.El archivo de configuración tiene miles de líneas de código XML cuya modificación es sumamente peligrosa.Se necesita ayuda para reducir esa cantidad de código a algo más fácil de tratar.  
  
## Resolución del contrato de datos  
 En .NET 3.5, había unas cuantas limitaciones en el diseño de tipos conocidos:  
  
-   No era posible agregar tipos conocidos dinámicamente durante la serialización o la deserialización.  
  
-   Los serializadores no podían tratar información de xsi:type desconocida.  
  
-   No era posible que los usuarios especificasen qué xsi:type preferirían que apareciese en la conexión para, por ejemplo, reducir el tamaño de una instancia de serialización en la conexión.  
  
 [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md) resuelve estos problemas en .NET 4.5.  
  
### Introducción  
  
-   [Documentación de la API de resolución del contrato de datos](http://go.microsoft.com/fwlink/?LinkId=204946)  
  
-   [Introducir la resolución del contrato de datos](http://go.microsoft.com/fwlink/?LinkId=204947)  
  
-   Ejemplos:  
  
    -   [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md)  
  
    -   [KnownAssemblyAttribute](../../../docs/framework/wcf/samples/knownassemblyattribute.md)  
  
### Escenarios de resolución del contrato de datos  
  
-   Evitar tener que declarar decenas de objetos <xref:System.Runtime.Serialization.KnownTypeAttribute> en un servicio.  
  
-   Reducir el tamaño del blob XML.  
  
## Diagrama de flujo  
 El diagrama de flujo es un paradigma conocido para representar visualmente los problemas de dominio.Es un nuevo estilo de flujo de control que se está introduciendo en .NET 4.Una característica básica de diagrama de flujo es que solo se ejecuta una actividad en un momento dado.Los diagramas de flujo pueden expresar bucles y resultados alternativos, pero no pueden expresar de forma nativa la ejecución simultánea de varios nodos.  
  
### Introducción  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree una aplicación de consola de flujo de trabajo.Agregue un diagrama de flujo en el diseñador de flujo de trabajo.  
  
-   La característica de diagrama de flujo utiliza las siguientes clases:  
  
    -   <xref:System.Activities.Statements.Flowchart>  
  
    -   <xref:System.Activities.Statements.FlowNode>  
  
    -   <xref:System.Activities.Statements.FlowDecision>  
  
    -   <xref:System.Activities.Statements.FlowStep>  
  
    -   <xref:System.Activities.Statements.FlowSwitch%601>  
  
-   Ejemplos:  
  
    -   [Control de errores en una actividad de diagrama de flujo utilizando TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    -   [Escenario StateMachine utilizando una combinación de actividades FlowChart y Pick](../../../docs/framework/windows-workflow-foundation/samples/statemachine-scenario-using-a-combination-of-flowchart-and-pick.md)  
  
    -   [Proceso de contratación](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
-   Documentación del diseñador:  
  
    -   [Diseñadores de actividades Flowchart](../Topic/Flowchart%20Activity%20Designers.md)  
  
### Escenarios de diagrama de flujo  
 Una actividad de diagrama de flujo se puede utilizar para implementar un juego de adivinanzas.Este juego es muy simple: el equipo selecciona un número aleatorio y el jugador tiene que adivinar el número.Cuando el jugador envía cada respuesta, el equipo le muestra una sugerencia \(por ejemplo,"intente un número menor"\).Si el jugador encuentra el número en menos de 7 intentos, recibe una felicitación especial por parte del equipo.Este juego se puede implementar con una combinación de las siguientes actividades de procedimiento:  
  
-   <xref:System.Activities.Statements.Sequence>  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.Switch%601>  
  
-   <xref:System.Activities.Statements.TryCatch>  
  
-   <xref:System.Activities.Statements.Assign%601>  
  
-   <xref:System.Activities.Statements.If>  
  
## Actividades de procedimiento \(Sequence, If, ForEach, Switch, Assign, DoWhile, While\)  
 Las actividades de procedimiento proporcionan un mecanismo para modelar el flujo de control secuencial utilizando conceptos familiares para los programadores.Estas actividades habilitan tradicionalmente construcciones de lenguaje de programación estructurada y, cuando corresponde, proporcionan paridad de lenguaje con lenguajes comunes de procedimiento como C\# o VB.  
  
### Introducción  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree una aplicación de consola de flujo de trabajo.Agregue actividades de procedimiento en el diseñador de flujo de trabajo.  
  
-   Ejemplos:  
  
    -   [Proceso de contratación](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
    -   [Proceso de compra corporativa](../../../docs/framework/windows-workflow-foundation/samples/corporate-purchase-process.md)  
  
-   Documentación del diseñador:  
  
    -   [Diseñador de actividades Parallel](../Topic/Parallel%20Activity%20Designer.md)  
  
    -   [Diseñador de actividades ParallelForEach\<T\>](../Topic/ParallelForEach%3CT%3E%20Activity%20Designer.md)  
  
### Escenarios de actividad de procedimiento  
  
-   <xref:System.Activities.Statements.Parallel>Parallel: un sistema de administración de documentos de intranet tiene un flujo de trabajo de aprobación de documentos.Los documentos necesitan ser aprobados por personas en varios departamentos antes de poderse publicar en la intranet.No hay un orden establecido para las aprobaciones; se pueden producir en cualquier momento mientras el documento esté en la fase de "pendiente de aprobación".Cuando un usuario envía un documento para su revisión, debe ser aprobado por su superior directo, el administrador de la intranet, y el administrador de comunicaciones internas.  
  
-   <xref:System.Activities.Statements.ParallelForEach%601>: una aplicación de WF administra las compras corporativas dentro de una gran compañía.Las reglas corporativas establecen que, antes de planear cualquier operación de compra, se requieren las valoraciones de tres proveedores diferentes.Un empleado del departamento de compras selecciona tres proveedores de la lista de proveedores de la compañía.Una vez seleccionados e informados estos proveedores, la compañía esperará a que realicen sus propuestas económicas.Las propuestas pueden llegar en cualquier orden.Para implementar este escenario en WF, se utiliza un elemento <xref:System.Activities.Statements.ParallelForEach%601> que recorrerá en iteración la colección de proveedores y pedirá sus propuestas económicas.Una vez reunidas todas las ofertas, se selecciona y se muestra la mejor.  
  
## InvokeMethod  
 La actividad <xref:System.Activities.Statements.InvokeMethod> permite invocar métodos públicos en objetos o tipos dentro del ámbito.Admite la invocación de métodos estáticos y de instancia con o sin parámetros \(incluidas matrices de parámetros\) y de métodos genéricos.También permite la ejecución de métodos sincrónica y asincrónicamente.  
  
### Introducción  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree una aplicación de consola de flujo de trabajo.Agregue una actividad <xref:System.Activities.Statements.InvokeMethod> en el diseñador de flujo de trabajo y configure en él métodos estáticos y de instancia.  
  
-   Ejemplos:  
  
    -   [InvokeMethod](../../../docs/framework/windows-workflow-foundation/samples/invokemethod.md)  
  
-   Documentación del diseñador: [Diseñador de actividades InvokeMethod](../Topic/InvokeMethod%20Activity%20Designer.md)  
  
### Escenarios de InvokeMethod  
  
-   Se necesita invocar un método en un objeto dentro del ámbito.Por ejemplo, se necesita agregar un valor a un diccionario.Se invoca el método Add de la instancia del diccionario y se proporcionan la clave y el valor.  
  
-   Se necesita invocar un método en un objeto CLR heredado.En lugar de crear una actividad personalizada para encapsular la llamada a esa clase heredada, si permanece dentro del ámbito durante la ejecución del flujo de trabajo, se puede utilizar <xref:System.Activities.Statements.InvokeMethod>.  
  
## Actividades de control de errores  
 La actividad <xref:System.Activities.Statements.TryCatch> proporciona un mecanismo para detectar excepciones que se producen durante la ejecución de un conjunto de actividades contenidas \(similar a la construcción Try\/Catch en C\#\/VB\).<xref:System.Activities.Statements.TryCatch> proporciona control de excepciones en el nivel de flujo de trabajo.Cuando se produce una excepción no controlada, se anula el flujo de trabajo y no se ejecutará el bloque Finally.Este comportamiento es coherente con C\#.  
  
### Introducción  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree una aplicación de consola de flujo de trabajo.Agregue una actividad <xref:System.Activities.Statements.TryCatch> en el diseñador de flujo de trabajo.  
  
-   Ejemplos:  
  
    1.  [Control de errores en una actividad de diagrama de flujo utilizando TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    2.  [Usar actividades de procedimiento](../../../docs/framework/windows-workflow-foundation/samples/using-procedural-activities.md)  
  
-   Documentación del diseñador: [Diseñadores de actividades de control de errores](../Topic/Error%20Handling%20Activity%20Designers.md)  
  
### Escenarios de control de errores  
 Necesita ejecutarse un conjunto de actividades y es necesaria la ejecución de una lógica específica cuando se produce un error.Si durante esa lógica de control de errores se encuentra que el error no es recuperable, volverá a producirse la excepción y la actividad primaria \(o el host\) abordará el problema.  
  
## Actividad Pick  
 La actividad <xref:System.Activities.Statements.Pick> proporciona un modelado de flujo de control basado en eventos en WF.<xref:System.Activities.Statements.Pick> contiene muchas bifurcaciones donde cada bifurcación espera que se produzca un evento determinado antes de ejecutarse.En esta configuración, el comportamiento de <xref:System.Activities.Statements.Pick> es similar al de <xref:System.Activities.Statements.Switch%601>, ya que la actividad solo ejecutará un evento del conjunto de eventos de los que está realizando escuchas.Cada bifurcación está orientada a eventos y el evento que se produzca ejecutará primero la bifurcación correspondiente.El resto de bifurcaciones se cancelan y se dejan de realizar escuchas de eventos.  
  
### Introducción  
  
-   En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree una aplicación de consola de flujo de trabajo.Agregue una actividad <xref:System.Activities.Statements.Pick> en el diseñador de flujo de trabajo.  
  
-   Ejemplo: [Uso de la actividad Pick](../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)  
  
-   Documentación del diseñador: [Diseñador de actividades Pick](../Topic/Pick%20Activity%20Designer.md)  
  
### Escenario de Pick  
 Se necesita solicitar una entrada a un usuario.En circunstancias normales, el desarrollador utilizaría una llamada a un método como <xref:System.Console.ReadLine%2A> para solicitar la entrada de un usuario.El problema con esta configuración es que el programa espera hasta que el usuario especifica algo.En este escenario, se necesita un tiempo de espera para desbloquear una actividad de bloqueo.Un escenario común es el que requiere que una tarea se complete dentro de un período de tiempo determinado.El agotamiento del tiempo de espera de una actividad de bloqueo es un escenario en el que Pick agrega gran cantidad de valor.  
  
## Servicio de enrutamiento de WCF  
 El servicio de enrutamiento está diseñado para ser un enrutador por software genérico que permite controlar cómo los mensajes de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] circulan entre los clientes y los servicios. El servicio de enrutamiento permite desacoplar los clientes de los servicios, proporcionando mucha más libertad en lo respecta a las configuraciones que se pueden admitir y la flexibilidad que se tiene al considerar cómo se han de hospedar los servicios. En .NET 3.5, los clientes y los servicios se acoplaban estrechamente; un cliente tenía que estar al corriente de todos los servicios con los que necesitaba hablar y saber dónde estaban ubicados.Además, WCF en .NET Framework 3.5 tenía las siguientes limitaciones:  
  
-   El control de errores era complejo, ya que esta lógica tenía que codificarse de forma rígida en el cliente.  
  
-   Los clientes y los servicios tenían que utilizar siempre los mismos enlaces.  
  
-   Los servicios raramente se factorizaban correctamente: es más fácil que el cliente hable con un servicio que implementa todo en lugar de tener que elegir entre varios servicios.  
  
 El servicio del enrutamiento en .NET 4 está diseñado para facilitar la solución de estos problemas.El nuevo servicio de enrutamiento tiene las siguientes características:  
  
1.  Enrutamiento basado en contenido \(los objetos <xref:System.ServiceModel.Dispatcher.MessageFilter> examinan un mensaje para determinar dónde se debe enviar\).  
  
2.  Protocolo de puente \(transporte y mensaje\)  
  
3.  Control de errores \(el enrutador detecta excepciones de comunicación y no puede establecer comunicación con los extremos de reserva\)  
  
4.  Actualización dinámica \(en memoria\) de <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> y configuración de enrutamiento.  
  
### Introducción  
  
1.  Documentación: [Enrutamiento](../../../docs/framework/wcf/feature-details/routing.md)  
  
2.  Ejemplos: [Servicios de enrutamiento &#91;ejemplos de WCF&#93;](../../../docs/framework/wcf/samples/routing-services.md)  
  
3.  Blog: [Reglas de enrutamiento](http://go.microsoft.com/fwlink/?LinkId=204956)  
  
### Escenarios de enrutamiento  
 El servicio de enrutamiento es útil en los siguientes escenarios:  
  
-   Los clientes pueden hablar con varios servicios sin tener que dirigirse a todos ellos directamente.  
  
-   Los clientes pueden realizar lógica adicional en la solicitud de un cliente para determinar dónde hay que enrutarlo.  
  
-   Descomponer las operaciones que un cliente realiza en varias implementaciones de servicio sin refactorizar el cliente.  
  
-   Los clientes y los servicios pueden hablar con enlaces diferentes que tienen configuraciones de seguridad diferentes.  
  
-   Puede habilitarse a los clientes para que sean más sólidos ante errores o la no disponibilidad de servicios.  
  
## Detección de WCF  
 La detección de [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] es una tecnología de .NET Framework que permite incorporar un mecanismo de detección a la infraestructura de las aplicaciones.Puede utilizarla para hacer su servicio reconocible y configurar los clientes para buscar los servicios.Los clientes ya no necesitan estar codificados de forma rígida con el extremo, lo que hace que la aplicación sea más sólida y tolerante a los errores.La detección es la plataforma perfecta para integrar capacidades de autoconfiguración en la aplicación.  
  
 El producto se basa en la norma WS\-Discovery.Está diseñado para ser interoperable, extensible y genérico.El producto admite dos modos de operación:  
  
1.  Administrado: donde hay una entidad en la red con gran conocimiento de los servicios existentes; los clientes la consultan directamente para obtener información.Esto es análogo a Active Directory.  
  
2.  Ad hoc: donde los clientes utilizan los mensajes de multidifusión para buscar los servicios.  
  
 Además, los mensajes de detección son válidos para distintos protocolos de red; pueden utilizarse sobre cualquier protocolo que admita los requisitos de modo.Por ejemplo, los mensajes de multidifusión de detección se pueden enviar a través del canal UDP o cualquier otra red que admita la mensajería de multidifusión. Estos puntos de diseño, combinados con la flexibilidad de características, permiten adaptar la detección de forma específica a la solución.  
  
### Introducción  
  
-   Documentación: [Detección de WCF](../../../docs/framework/wcf/feature-details/wcf-discovery.md)  
  
-   Ejemplos: [Detección \(ejemplos\)](../../../docs/framework/wcf/samples/discovery-samples.md)  
  
### Escenarios de detección  
 Un desarrollador no desea codificar de forma rígida los extremos, porque no se sabe cuándo estará disponible un servicio determinado.En su lugar, desea elegir un servicio en tiempo de ejecución.Se necesita más desacoplamiento, solidez y autoconfiguración entre los componentes de la aplicación.  
  
## Seguimiento  
 El seguimiento de flujo de trabajo proporciona una visión sobre la ejecución de una instancia de flujo de trabajo. Los eventos de seguimiento se emiten desde un flujo de trabajo en el nivel de instancia de flujo de trabajo y cuando se ejecutan las actividades dentro del flujo de trabajo.Se necesita agregar un participante de seguimiento de flujo de trabajo al host de flujo de trabajo para suscribirse a los registros de seguimiento.Los registros de seguimiento se filtran utilizando un perfil de seguimiento..NET Framework proporciona un participante de seguimiento ETW \(Seguimiento de eventos para Windows\) y se instala un perfil básico en el archivo machine.config.  
  
### Introducción  
  
1.  En [!INCLUDE[vs2010](../../../includes/vs2010-md.md)], cree un proyecto de aplicación de servicio de flujo de trabajo WCF.Se colocará un par <xref:System.ServiceModel.Activities.Receive> y <xref:System.ServiceModel.Activities.SendReply> en el lienzo para empezar.  
  
2.  Abra web.config y agregue un comportamiento de seguimiento de ETW sin ningún perfil.  
  
    1.  Se utiliza el perfil predeterminado.  
  
    2.  Abra el visor de eventos y habilite el canal analítico en el nodo siguiente: **Visor de eventos**, **Registros de aplicaciones y servicios**, **Microsoft**, **Windows**, **Servidor de aplicaciones\-Aplicaciones**.Haga clic con el botón secundario en **Analítico** y seleccione **Habilitar registro**.  
  
    3.  Ejecute el servicio de flujo de trabajo.  
  
    4.  Observe los eventos de seguimiento de flujo de trabajo en el visor de eventos.  
  
3.  Ejemplos: [Seguimiento](../../../docs/framework/windows-workflow-foundation/samples/tracking.md)  
  
4.  Documentación conceptual: [Seguimiento y traza del flujo de trabajo](../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)  
  
## Almacén de instancias de flujo de trabajo de SQL  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> es una implementación basada en SQL Server de un almacén de instancias.Un almacén de instancias almacena el estado de una instancia en ejecución junto con todos los datos necesarios para cargar y reanudar esa instancia.El host de servicio indica al almacén de instancias que guarde el estado de la instancia si el flujo de trabajo persiste y le indica también que cargue el estado de la instancia cuando llegue un mensaje para esa instancia o expire una actividad Delay.  
  
### Introducción  
  
1.  En [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], cree un flujo de trabajo que contenga una actividad <xref:System.Activities.Statements.Persist> implícita o explícita.Agregue el comportamiento de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> al host de servicio de flujo de trabajo.Esto se puede realizar en el código o en el archivo de configuración de la aplicación.  
  
2.  Ejemplos: [Persistencia](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)  
  
3.  Documentación conceptual: [Almacén de instancias de flujo de trabajo de SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)