---
title: "Interop Marshaling | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "marshaling, COM interop"
  - "interop marshaling"
  - "interop marshaling, about interop marshaling"
ms.assetid: 115f7a2f-d422-4605-ab36-13a8dd28142a
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Interop Marshaling
La serialización de interoperabilidad rige cómo se pasan los datos en argumentos de método y valores devueltos entre la memoria administrada y la no administrada durante las llamadas.  La serialización de interoperabilidad es una actividad en tiempo de ejecución realizada por el servicio de serialización de Common Language Runtime.  
  
 La mayoría de los tipos de datos tienen representaciones comunes tanto en la memoria administrada como en la no administrada.  El administrador de serialización de interoperabilidad controla esos tipos automáticamente.  El resto de tipos pueden ser ambiguos o no estar representados en la memoria administrada.  
  
 Un tipo ambiguo puede tener varias representaciones no administradas que se asignan a un solo tipo administrado, o bien no tener información de tipos, como el tamaño de una matriz.  Para los tipos ambiguos, el administrador de serialización proporciona una representación predeterminada y varias representaciones alternativas si existen.  Se pueden proporcionar instrucciones explícitas al administrador de serialización sobre cómo serializar un tipo ambiguo.  
  
 Esta información general contiene las siguientes secciones:  
  
-   [Modelos de invocación de plataforma e interoperabilidad COM](#platform_invoke_and_com_interop_models)  
  
-   [Serialización y apartamentos COM](#marshaling_and_com_apartments)  
  
-   [Serialización de llamadas remotas](#marshaling_remote_calls)  
  
-   [Temas relacionados](#related_topics)  
  
-   [Referencia](#reference)  
  
<a name="platform_invoke_and_com_interop_models"></a>   
## Modelos de invocación de plataforma e interoperabilidad COM  
 Common Language Runtime proporciona dos mecanismos para interoperar con código no administrado:  
  
-   Invocación de plataforma, que permite al código administrado llamar a funciones exportadas desde una biblioteca no administrada.  
  
-   Interoperabilidad COM, que permite al código administrado interactuar con modelos de objetos componentes \(COM\) a través de interfaces.  
  
 Tanto la invocación de plataforma como la interoperabilidad COM usan serialización de interoperabilidad para mover con precisión los argumentos de método desde el llamador al destinatario y viceversa, si es necesario.  Como se muestra en la siguiente ilustración, una llamada al método de invocación de plataforma fluye desde el código administrado al no administrado y nunca en sentido contrario, excepto cuando hay implicadas [funciones de devolución de llamada](../../../docs/framework/interop/callback-functions.md).  Aunque las llamadas de invocación de plataforma solo pueden realizarse desde código administrado a código no administrado, los datos pueden fluir en ambas direcciones como parámetros de entrada o salida.  Las llamadas a métodos de interoperabilidad COM pueden fluir en ambas direcciones.  
  
 ![Invocación de plataforma](../../../docs/framework/interop/media/interopmarshaling.png "interopmarshaling")  
Flujo de llamadas de invocación de plataforma e interoperabilidad COM  
  
 En el nivel más bajo, ambos mecanismos usan el mismo servicio de serialización de interoperabilidad; sin embargo, hay determinados tipos de datos que solo se admiten en la interoperabilidad COM o en la invocación de plataforma.  Para obtener más información, consulte el artículo sobre [Default Marshaling Behavior](../../../docs/framework/interop/default-marshaling-behavior.md).  
  
 [Volver al principio](#top)  
  
<a name="marshaling_and_com_apartments"></a>   
## Serialización y apartamentos COM  
 El administrador de serialización de interoperabilidad serializa datos entre el montón de Common Language Runtime y el montón no administrado.  La serialización se produce siempre que el llamador y el destinatario no pueden operar en la misma instancia de datos.  El administrador de serialización de interoperabilidad permite al llamador y al destinatario operar en los mismos datos, incluso aunque tengan su propia copia de los datos.  
  
 COM también dispone de un administrador de serialización que serializa datos entre apartamentos COM o diferentes procesos COM.  Al realizar llamadas entre código administrado y no administrado en el mismo apartamento COM, el administrador de serialización de interoperabilidad es el único administrador de serialización implicado.  Al realizar llamadas entre código administrado y código no administrado en un apartamento COM diferente o en un proceso diferente, están implicados tanto el administrador de serialización de interoperabilidad como el administrador de serialización de COM.  
  
### Clientes COM y servidores administrados  
 Un servidor administrado exportado con una biblioteca de tipos registrada por la [Regasm.exe \(Assembly Registration Tool\)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) tiene una entrada del Registro `ThreadingModel` establecida en `Both`.  Este valor indica que el servidor puede activarse en un contenedor uniproceso \(STA\) o en un contenedor multiproceso \(MTA\).  El objeto de servidor se crea en el mismo apartamento que su llamador, como se muestra en la tabla siguiente.  
  
|Cliente COM|Servidor .NET|Requisitos de serialización|  
|-----------------|-------------------|---------------------------------|  
|STA|`Both` se convierte en STA.|Serialización en mismo apartamento.|  
|MTA|`Both` se convierte en MTA.|Serialización en mismo apartamento.|  
  
 Dado que el cliente y el servidor están en el mismo apartamento, el servicio de serialización de interoperabilidad controla automáticamente toda la serialización de datos.  La ilustración siguiente muestra cómo opera el servicio de serialización de interoperabilidad entre montones administrados y no administrados dentro del mismo apartamento de estilo COM.  
  
 ![Cálculo de referencias interoperativo](../../../docs/framework/interop/media/interopheap.gif "interopheap")  
Proceso de serialización en el mismo apartamento  
  
 Si planea exportar un servidor administrado, tenga en cuenta que el cliente COM determina el apartamento del servidor.  Un servidor administrado llamado por un cliente COM inicializado en un MTA debe garantizar la seguridad de subprocesos.  
  
### Clientes administrados y servidores COM  
 La configuración predeterminada para apartamentos de cliente administrado es MTA; sin embargo, el tipo de aplicación del cliente .NET puede cambiar la configuración predeterminada.  Por ejemplo, una configuración de apartamento de cliente [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] es STA.  Puede usar <xref:System.STAThreadAttribute?displayProperty=fullName>, <xref:System.MTAThreadAttribute?displayProperty=fullName>, la propiedad <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=fullName> o la propiedad <xref:System.Web.UI.Page.AspCompatMode%2A?displayProperty=fullName> para examinar y cambiar la configuración de apartamento de un cliente administrado.  
  
 El autor del componente establece la afinidad del subproceso de un servidor COM.  En la tabla siguiente se muestran las combinaciones de configuraciones de apartamentos para clientes .NET y servidores COM.  También se muestran los requisitos de serialización resultantes para las combinaciones.  
  
|Cliente .NET|Servidor COM|Requisitos de serialización|  
|------------------|------------------|---------------------------------|  
|MTA \(valor predeterminado\)|MTA<br /><br /> STA|Serialización de interoperabilidad.<br /><br /> Serialización de interoperabilidad y COM.|  
|STA|MTA<br /><br /> STA|Serialización de interoperabilidad y COM.<br /><br /> Serialización de interoperabilidad.|  
  
 Cuando un cliente administrado y un servidor no administrado están en el mismo apartamento, el servicio de serialización de interoperabilidad controla toda la serialización de datos.  Sin embargo, cuando el cliente y el servidor se inicializan en apartamentos diferentes, también es necesaria la serialización de COM.  La ilustración siguiente muestra los elementos de una llamada entre apartamentos.  
  
 ![Cálculo de referencias COM](../../../docs/framework/interop/media/singleprocessmultapt.gif "singleprocessmultapt")  
Llamada entre apartamentos entre un cliente .NET y un objeto COM  
  
 Para una serialización entre apartamentos, puede hacer lo siguiente:  
  
-   Aceptar la sobrecarga que supone la serialización entre apartamentos, que solo es apreciable cuando hay muchas llamadas que cruzan el límite.  Debe registrar la biblioteca de tipos del componente COM para que las llamadas crucen correctamente el límite del apartamento.  
  
-   Establecer el subproceso de cliente en STA o MTA para alterar el subproceso principal.  Por ejemplo, si el cliente de C\# llama a muchos componentes COM de STA, puede evitar la serialización entre apartamentos si establece el subproceso principal en STA.  
  
    > [!NOTE]
    >  Una vez que se establece el subproceso de un cliente C\# en STA, las llamadas a componentes COM de MTA requerirán la serialización entre apartamentos.  
  
 Para obtener instrucciones sobre cómo seleccionar explícitamente un modelo de apartamento, vea el artículo sobre [Managed and Unmanaged Threading](http://msdn.microsoft.com/es-es/db425c20-4b2f-4433-bf96-76071c7881e5).  
  
 [Volver al principio](#top)  
  
<a name="marshaling_remote_calls"></a>   
## Serialización de llamadas remotas  
 Al igual que con la serialización entre apartamentos, la serialización de COM participa en todas las llamadas entre código administrado y no administrado siempre que los objetos residan en procesos independientes.  Por ejemplo:  
  
-   Un cliente COM que invoca a un servidor administrado en un host remoto usa COM distribuido \(DCOM\).  
  
-   Un cliente administrado que invoca a un servidor COM en un host remoto usa DCOM.  
  
 En la ilustración siguiente se muestra cómo la serialización de interoperabilidad y la serialización de COM proporcionan canales de comunicación a través de procesos y límites de hosts.  
  
 ![Cálculo de referencias COM](../../../docs/framework/interop/media/interophost.gif "interophost")  
Serialización entre procesos  
  
### Conservar la identidad  
 Common Language Runtime conserva la identidad de las referencias administradas y no administradas.  En la siguiente ilustración se muestra el flujo de referencias directas no administradas \(fila superior\) y de referencias directas administradas \(fila inferior\) entre procesos y límites de hosts.  
  
 ![Contenedor CCW y contenedor RCW](../../../docs/framework/interop/media/interopdirectref.gif "interopdirectref")  
Paso de referencia entre límites de hosts y procesos  
  
 En esta ilustración:  
  
-   Un cliente no administrado obtiene una referencia a un objeto COM de un objeto administrado que obtiene esta referencia de un host remoto.  El mecanismo de comunicación remota es DCOM.  
  
-   Un cliente administrado obtiene una referencia a un objeto administrado de un objeto COM que obtiene esta referencia de un host remoto.  El mecanismo de comunicación remota es DCOM.  
  
    > [!NOTE]
    >  La biblioteca de tipos exportada del servidor administrado debe estar registrada.  
  
 El número de límites de procesos entre llamador y destinatario es irrelevante; la misma referencia directa se produce para las llamadas en proceso y fuera de proceso.  
  
### Comunicación remota administrada  
 El runtime también proporciona comunicación remota administrada que puede usarse para establecer un canal de comunicaciones entre objetos administrados a través varios procesos y límites de hosts.  La comunicación remota administrada puede alojar un firewall entre los componentes de la comunicación, como se muestra en la ilustración siguiente.  
  
 ![SOAP o TcpChannel](../../../docs/framework/interop/media/interopremotesoap.gif "interopremotesoap")  
Llamadas remotas a través de firewalls que usan SOAP o la clase TcpChannel  
  
 Algunas llamadas no administradas pueden canalizarse mediante SOAP, como las llamadas entre [componentes con servicio](http://msdn.microsoft.com/es-es/f109ee24-81ad-4d99-9892-51ac6f34978c) y COM.  Para obtener información adicional sobre el uso de la comunicación remota, vea la [información general sobre comunicación remota de .NET](http://msdn.microsoft.com/es-es/eccb1d31-0a22-417a-97fd-f4f1f3aa4462).  
  
 [Volver al principio](#top)  
  
<a name="related_topics"></a>   
## Temas relacionados  
  
|Título|Descripción|  
|------------|-----------------|  
|[Default Marshaling Behavior](../../../docs/framework/interop/default-marshaling-behavior.md)|Describe las reglas que usa el servicio de serialización de interoperabilidad para serializar datos.|  
|[Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)|Describe cómo se declaran parámetros de método y se pasan argumentos a funciones exportadas por bibliotecas no administradas.|  
|[Marshaling Data with COM Interop](../../../docs/framework/interop/marshaling-data-with-com-interop.md)|Describe cómo se personalizan los contenedores COM para alterar el comportamiento de la serialización.|  
|[Cómo: Migrar código administrado DCOM a WCF](../../../docs/framework/interop/how-to-migrate-managed-code-dcom-to-wcf.md)|Describe cómo se migra de DCOM a WCF.|  
|[How to: Map HRESULTs and Exceptions](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md)|Describe cómo se asignan excepciones personalizadas a valores HRESULT y proporciona la asignación completa de cada HRESULT a su clase de excepción comparable en .NET Framework.|  
|[Interoperating Using Generic Types](http://msdn.microsoft.com/es-es/26b88e03-085b-4b53-94ba-a5a9c709ce58)|Describe qué acciones se admiten al usar tipos genéricos para la interoperabilidad COM.|  
|[Interoperating with Unmanaged Code](../../../docs/framework/interop/index.md)|Describe los servicios de interoperabilidad proporcionados por Common Language Runtime.|  
|[Advanced COM Interoperability](http://msdn.microsoft.com/es-es/3ada36e5-2390-4d70-b490-6ad8de92f2fb)|Proporciona vínculos a más información sobre la incorporación de componentes COM en una aplicación de .NET Framework.|  
|[Design Considerations for Interoperation](http://msdn.microsoft.com/es-es/b59637f6-fe35-40d6-ae72-901e7a707689)|Proporciona sugerencias para escribir componentes COM integrados.|  
|[Comunicación remota de .NET](http://msdn.microsoft.com/es-es/515686e6-0a8d-42f7-8188-73abede57c58)|Describe los diversos métodos disponibles en .NET Framework para las comunicaciones remotas.|  
  
 [Volver al principio](#top)  
  
<a name="reference"></a>   
## Referencia  
 <xref:System.Runtime.InteropServices?displayProperty=fullName>  
  
 [Volver al principio](#top)