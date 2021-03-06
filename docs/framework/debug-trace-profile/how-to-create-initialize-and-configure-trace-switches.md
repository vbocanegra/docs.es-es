---
title: "How to: Create, Initialize and Configure Trace Switches | Microsoft Docs"
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
  - "trace switches, configuring"
  - "tracing [.NET Framework], trace switches"
  - "switches, trace"
  - "tracing [.NET Framework], enabling or disabling"
  - "Web.config configuration file, trace switches"
ms.assetid: 5a0e41bf-f99c-4692-8799-f89617f5bcf9
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Create, Initialize and Configure Trace Switches
Los modificadores de seguimiento permiten habilitar, deshabilitar y filtrar la salida del seguimiento.  
  
<a name="create"></a>   
## Para crear e inicializar modificadores de seguimiento  
 Para poder usar los modificadores de seguimiento, primero debe crearlos y colocarlos en el código. Existen dos clases predefinidas desde las que puede crear objetos modificadores: la clase <xref:System.Diagnostics.BooleanSwitch?displayProperty=fullName> y la clase <xref:System.Diagnostics.TraceSwitch?displayProperty=fullName>. Debe usar <xref:System.Diagnostics.BooleanSwitch> si solo le preocupa si aparece o no un mensaje de seguimiento, y <xref:System.Diagnostics.TraceSwitch> para distinguir entre los niveles de seguimiento. Si utiliza <xref:System.Diagnostics.TraceSwitch>, puede definir sus propios mensajes de depuración y asociarlos a diferentes niveles de seguimiento. Puede utilizar ambos tipos de modificadores con el seguimiento o la depuración. De forma predeterminada, <xref:System.Diagnostics.BooleanSwitch> está deshabilitado y <xref:System.Diagnostics.TraceSwitch> está establecido en el nivel <xref:System.Diagnostics.TraceLevel?displayProperty=fullName>. Los modificadores de seguimiento pueden crearse y colocarse en cualquier parte del código que pueda utilizarlos.  
  
 Aunque puede establecer niveles de seguimiento y otras opciones de configuración en el código, le recomendamos que utilice el archivo de configuración para administrar el estado de los modificadores. El motivo es que administrar la configuración de los modificadores en el sistema de configuración le proporciona mayor flexibilidad: puede activar y desactivar los diversos modificadores y cambiar los niveles sin volver a compilar la aplicación.  
  
#### Para crear e inicializar modificadores de seguimiento  
  
1.  Defina un modificador de tipo <xref:System.Diagnostics.BooleanSwitch?displayProperty=fullName> o tipo <xref:System.Diagnostics.TraceSwitch?displayProperty=fullName> y establezca el nombre y la descripción del modificador.  
  
2.  Configure el modificador de seguimiento. Para más información, consulte [Configuración de modificadores de seguimiento](#configure).  
  
     El siguiente código crea dos modificadores, uno de cada tipo:  
  
    ```vb  
    Dim dataSwitch As New BooleanSwitch("Data", "DataAccess module") Dim generalSwitch As New TraceSwitch("General", "Entire application")  
  
    ```  
  
    ```csharp  
    System.Diagnostics.BooleanSwitch dataSwitch = new System.Diagnostics.BooleanSwitch("Data", "DataAccess module"); System.Diagnostics.TraceSwitch generalSwitch = new System.Diagnostics.TraceSwitch("General", "Entire application");  
  
    ```  
  
<a name="configure"></a>   
## Configurar modificadores de seguimiento  
 Después de que se distribuya la aplicación, puede habilitar o deshabilitar el resultado del seguimiento configurando los modificadores de seguimiento de la aplicación. Configurar un modificador consiste en cambiar su valor desde un origen externo después de que se inicialice. Puede cambiar los valores de los objetos modificadores con el archivo de configuración. Puede configurar un modificador de seguimiento para activarlo y desactivarlo, o para establecer su nivel y determinar la cantidad y el tipo de mensajes que pasa a los agentes de escucha.  
  
 Los modificadores se configuran con el archivo .config. En una aplicación web, es el archivo Web.config asociado al proyecto. En una aplicación de Windows, este archivo se denomina \(nombre de la aplicación\).exe.config. En una aplicación implementada, este archivo debe residir en la misma carpeta que el ejecutable.  
  
 Cuando la aplicación ejecuta el código que crea una instancia de un modificador por primera vez, la aplicación comprueba el archivo de configuración para obtener información de nivel de seguimiento sobre el modificador con nombre. El sistema de seguimiento examina el archivo de configuración una sola vez con cada modificador, la primera vez que la aplicación crea el modificador.  
  
 En una aplicación implementada, el código de seguimiento se habilita volviendo a configurar los modificadores cuando la aplicación no se está ejecutando. Normalmente, esto implica activar y desactivar los modificadores cambiando los niveles de seguimiento y, luego, reiniciar la aplicación.  
  
 Cuando crea una instancia de un modificador, también la inicializa especificando dos argumentos: un argumento *displayName* y un argumento *description*. El argumento *displayName* del constructor establece la propiedad <xref:System.Diagnostics.Switch.DisplayName%2A?displayProperty=fullName> de la instancia de clase <xref:System.Diagnostics.Switch>.*displayName* es el nombre que se utiliza para configurar el modificador en el archivo .config, y el argumento *description* debería devolver una breve descripción del modificador e indicar qué mensajes controla.  
  
 Además de especificar el nombre de un modificador para configurarlo, también debe especificar un valor para el modificador. El valor es un entero. Para <xref:System.Diagnostics.BooleanSwitch>, un valor de 0 corresponde a **Desactivado**, y cualquier valor distinto de cero corresponde a **Activado**. Para <xref:System.Diagnostics.TraceSwitch>, 0, 1, 2, 3 y 4 corresponden a **Desactivar**, **Error**, **Advertencia**, **Información** y **Detallado**, respectivamente. Todos los números mayores de 4 se tratan como **Detallado**, y todos los números menores de cero se tratan como **Desactivado**.  
  
> [!NOTE]
>  En la versión 2.0 de .NET Framework, puede utilizar texto para especificar el valor de un modificador. Por ejemplo, `true` para un <xref:System.Diagnostics.BooleanSwitch> o el texto que representa un valor de enumeración como `Error` para un <xref:System.Diagnostics.TraceSwitch>. La línea `<add name="myTraceSwitch" value="Error" />` es equivalente a `<add name="myTraceSwitch" value="1" />`.  
  
 Para que los usuarios finales puedan configurar los modificadores de seguimiento de una aplicación, debe proporcionar documentación detallada sobre los modificadores de la aplicación. Debe detallar qué modificadores controlan qué y cómo activarlos y desactivarlos. También debe proporcionar al usuario final un archivo .config con una ayuda apropiada en los comentarios.  
  
#### Para configurar modificadores de seguimiento  
  
1.  Para usar modificadores de seguimiento, primero debe crearlos y colocarlos en su código según se describe en la sección [Para crear e inicializar modificadores de seguimiento](#create).  
  
2.  Si el proyecto no contiene un archivo de configuración \(app.config o Web.config\), en el menú **Proyecto**, elija **Agregar nuevo elemento**.  
  
    -   **Visual Basic:** en el cuadro de diálogo **Agregar nuevo elemento**, elija **Archivo de configuración de aplicaciones**.  
  
         El archivo de configuración de la aplicación se creará y se abrirá. Se trata de un documento XML cuyo elemento raíz es `<configuration>.`  
  
    -   **Visual C\#:** en el cuadro de diálogo **Agregar nuevo elemento**, elija **Archivo XML**. Nombre a este archivo como **app.config**. En el editor XML, después de la declaración de XML, agregue el siguiente código XML:  
  
        ```  
        <configuration> </configuration>  
        ```  
  
         Cuando se compila el proyecto, el archivo app.config se copia a la carpeta de salida del proyecto y se cambia su nombre a *nombreDeLaAplicación*.exe.config.  
  
3.  Después de la etiqueta  `<configuration>` , pero antes de la etiqueta  `</configuration>` , agregue el código XML adecuado para configurar los modificadores. Los ejemplos siguientes muestran un **BooleanSwitch** con una propiedad **DisplayName** de `DataMessageSwitch` y un **TraceSwitch** con una propiedad **DisplayName** de `TraceLevelSwitch`.  
  
    ```  
    <system.diagnostics> <switches> <add name="DataMessagesSwitch" value="0" /> <add name="TraceLevelSwitch" value="0" /> </switches> </system.diagnostics>  
    ```  
  
     En esta configuración, ambos modificadores están desactivados.  
  
4.  Si necesita activar un **BooleanSwitch**, como `DataMessagesSwitch`, que se muestra en el ejemplo anterior, cambie el **Value** por cualquier entero distinto de 0.  
  
5.  Si necesita activar un **TraceSwitch**, como `TraceLevelSwitch`, que se muestra en el ejemplo anterior, cambie el **Value** por el ajuste del nivel adecuado \(del 1 al 4\).  
  
6.  Agregue comentarios al archivo .config para que el usuario final entienda claramente qué valores debe cambiar para configurar los modificadores de la manera correcta.  
  
     En el ejemplo siguiente se muestra cómo podría quedar el código final, incluidos los comentarios:  
  
    ```  
    <system.diagnostics> <switches> <!-- This switch controls data messages. In order to receive data trace messages, change value="0" to value="1" --> <add name="DataMessagesSwitch" value="0" /> <!-- This switch controls general messages. In order to receive general trace messages change the value to the appropriate level. "1" gives error messages, "2" gives errors and warnings, "3" gives more detailed error information, and "4" gives verbose trace information --> <add name="TraceLevelSwitch" value="0" /> </switches> </system.diagnostics>  
    ```  
  
## Vea también  
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [How to: Add Trace Statements to Application Code](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [Trace Switches](../../../docs/framework/debug-trace-profile/trace-switches.md)   
 [Esquema de la configuración de seguimiento y depuración](../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)