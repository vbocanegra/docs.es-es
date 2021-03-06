---
title: "Redirigir versiones de ensamblado | Microsoft Docs"
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
  - "configuración de la aplicación[.NET Framework]"
  - "ensamblados [.NET Framework], redirección de enlaces"
  - "enlace de ensamblado, redirección"
  - "configuración [.NET Framework], aplicaciones"
  - "redirigir el enlace de ensamblados a una versión anterior"
ms.assetid: 88fb1a17-6ac9-4b57-8028-193aec1f727c
caps.latest.revision: 26
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 26
---
# Redirigir versiones de ensamblado
Puede redirigir referencias de enlace en tiempo de compilación a los ensamblados de .NET Framework, ensamblados de terceros o ensamblados de su propia aplicación. Puede redirigir la aplicación para que use una versión diferente de un ensamblado de varias maneras: mediante la directiva de edición, a través de un archivo de configuración de la aplicación o mediante el archivo de configuración de la máquina. En este artículo se describe cómo funciona el enlace de ensamblado en .NET Framework y cómo se puede configurar.  
  
<a name="BKMK_Assemblyunificationanddefaultbinding"></a>   
## Unificación de ensamblados y enlace predeterminado  
 Los enlaces de ensamblados de .NET Framework a veces se redirigen a través de un proceso denominado *unificación de ensamblados*. .NET Framework consta de una versión de Common Language Runtime y casi dos docenas de ensamblados de .NET Framework que componen la biblioteca de tipos. El runtime trata estos ensamblados de .NET Framework como una sola unidad. De manera predeterminada, cuando se inicia una aplicación, todas las referencias a tipos en código ejecutado por el runtime se dirigen a ensamblados de .NET Framework que tienen el mismo número de versión que el runtime que se carga en un proceso. Las redirecciones que se producen con este modelo son el comportamiento predeterminado para el motor en tiempo de ejecución.  
  
 Por ejemplo, si la aplicación hace referencia a tipos en el espacio de nombres System.XML y se creó con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], contiene referencias estáticas al ensamblado de System.XML que se suministra con la versión 4.5 del runtime. Si quiere redirigir la referencia de enlace para que señale al ensamblado de System.XML que se suministra con .NET Framework 4, puede colocar la información de redirección en el archivo de configuración de la aplicación. Una redirección de enlace en un archivo de configuración para un ensamblado de .NET Framework unificado cancela la unificación para ese ensamblado.  
  
 Además, puede que quiera redirigir manualmente el enlace de ensamblados para ensamblados de terceros si hay varias versiones disponibles.  
  
<a name="BKMK_Redirectingassemblyversionsbyusingpublisherpolicy"></a>   
## Redirección de versiones de ensamblado mediante la directiva de edición  
 Los proveedores de ensamblados pueden dirigir las aplicaciones a una versión más reciente de un ensamblado incluyendo un archivo de directiva de edición con el nuevo ensamblado. El archivo de directivas de edición, que se encuentra en la caché global de ensamblados, contiene valores de redirección de ensamblados.  
  
 Cada versión *principal*.*secundaria* de un ensamblado tiene su propio archivo de directiva de edición. Por ejemplo, las redirecciones de la versión 2.0.2.222 a la 2.0.3.000 y de la versión 2.0.2.321 a la 2.0.3.000 van al mismo archivo, porque están asociadas a la versión 2.0. Sin embargo, una redirección de la versión 3.0.0.999 a la versión 4.0.0.000 va en el archivo de la versión 3.0.999. Cada versión principal de .NET Framework tiene su propio archivo de directiva de edición.  
  
 Si existe un archivo de directiva de edición para un ensamblado, el motor de tiempo de ejecución comprueba este archivo después de comprobar el manifiesto del ensamblado y el archivo de configuración de la aplicación. Los proveedores deben usar los archivos de directiva de edición cuando el nuevo ensamblado sea compatible con la versión anterior del ensamblado que se redirige.  
  
 Puede omitir la directiva de edición para la aplicación especificando los valores del archivo de configuración de la aplicación, como se describe en la [sección sobre omisión de la directiva de edición](#bypass_PP).  
  
<a name="BKMK_Redirectingassemblyversionsattheapplevel"></a>   
## Redirección de las versiones de ensamblado en el nivel de aplicación  
 Hay algunas técnicas diferentes para cambiar el comportamiento de enlace de la aplicación a través del archivo de configuración de la aplicación: puede editar manualmente el archivo, puede basarse en la redirección de enlace automática o puede especificar el comportamiento de enlace omitiendo la directiva de edición.  
  
### Edición manual del archivo de configuración de la aplicación  
 Puede editar manualmente el archivo de configuración de la aplicación para resolver problemas de ensamblado. Por ejemplo, si un proveedor puede publicar una versión más reciente de un ensamblado de la que usa su aplicación sin ofrecer una directiva de edición, porque no garantiza la compatibilidad con versiones anteriores, puede dirigir la aplicación para que use la versión más reciente del ensamblado colocando la siguiente información de enlace de ensamblado en el archivo de configuración de la aplicación de la siguiente manera.  
  
```  
<dependentAssembly> <assemblyIdentity name="someAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <bindingRedirect oldVersion="7.0.0.0" newVersion="8.0.0.0" /> </dependentAssembly>  
```  
  
### Confiar en una redirección de enlace automática  
 A partir de [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], las nuevas aplicaciones de escritorio dirigidas a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] usan la redirección de enlace automática. Esto significa que, si dos componentes hacen referencia a versiones diferentes del mismo ensamblado con nombre seguro, el motor de tiempo de ejecución agrega automáticamente una redirección de enlace a la versión más reciente del ensamblado en el archivo de configuración \(app.config\) de la aplicación de salida. Esta redirección invalida la unificación de ensamblados que, de lo contrario, puede tener lugar. El archivo app.config de origen no se modifica. Por ejemplo, supongamos que la aplicación hace referencia directamente a un componente de .NET Framework fuera de banda pero que usa una biblioteca de terceros destinada una versión anterior del mismo componente. Al compilar la aplicación, se modifica el archivo de configuración de la aplicación de salida para que incluya una redirección de enlace a la versión más reciente del componente. Si crea una aplicación web, recibirá una advertencia de compilación relacionada con el conflicto de enlace que, a su vez, le ofrece la opción de agregar la redirección de enlace necesaria para el archivo de configuración web de origen.  
  
 Si agrega redirecciones de enlace al archivo app.config de origen manualmente, en tiempo de compilación, [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] intenta unificar los ensamblados en función de las redirecciones de enlace que ha agregado. Por ejemplo, supongamos que inserta la siguiente redirección de enlace para un ensamblado:  
  
 `<bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0" />`  
  
 Si otro proyecto de la aplicación hace referencia a la versión 1.0.0.0 del mismo ensamblado, la redirección de enlace automático agrega la siguiente entrada al archivo app.config de salida para que la aplicación se unifique en la versión 2.0.0.0 de este ensamblado:  
  
 `<bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />`  
  
 Puede habilitar la redirección de enlace automático si su aplicación está dirigida a versiones anteriores de .NET Framework en [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)]. Puede invalidar este comportamiento predeterminado ofreciendo información de redirección del enlace en el archivo app.config para cualquier ensamblado o desactivar la característica de redirección de enlace. Para obtener información sobre cómo activar o desactivar esta característica, vea [Cómo: Habilitar y deshabilitar redireccionamiento de enlaces automático](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).  
  
<a name="bypass_PP"></a>   
### Omisión de la directiva de edición  
 Puede invalidar la directiva de edición del archivo de configuración de la aplicación en caso necesario. Por ejemplo, las nuevas versiones de los ensamblados que afirman ser compatibles con versiones anteriores todavía pueden interrumpir una aplicación. Si quiere omitir la directiva de edición, agregue un elemento [\<publisherPolicy\>](../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md) al elemento [\<dependentAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md) en el archivo de configuración de la aplicación y establezca el atributo **apply** en **no**, lo que invalida cualquier configuración de **yes** anterior.  
  
 `<publisherPolicy apply="no" />`  
  
 Omita la directiva de edición para mantener la aplicación en ejecución para sus usuarios, pero asegúrese de que informa del problema al proveedor del ensamblado. Si un ensamblado tiene un archivo de directiva de edición, el proveedor debe asegurarse de que el ensamblado es compatible con versiones anteriores y de que los clientes pueden usar la nueva versión tanto como sea posible.  
  
<a name="BKMK_Redirectingassemblyversionsatthemachinelevel"></a>   
## Redirección de las versiones de ensamblado en el nivel de equipo  
 En raras ocasiones es posible que un administrador del equipo quiera que todas las aplicaciones de un equipo usen una versión específica de un ensamblado. Por ejemplo, es posible que el administrador quiera que todas las aplicaciones usen una versión de ensamblado concreta, ya que la versión corrige una vulnerabilidad de seguridad. Si se redirige un ensamblado en el archivo de configuración del equipo, todas las aplicaciones de ese equipo que usen la versión anterior se dirigirán al uso de la nueva versión. El archivo de configuración del equipo reemplaza el archivo de configuración de la aplicación y el archivo de la directiva de edición. Este archivo se encuentra en el directorio %*ruta de instalación en tiempo de ejecución*%\\Config. Normalmente, .NET Framework se instala en el directorio %unidad%\\Windows\\Microsoft.NET\\Framework.  
  
<a name="BKMK_Specifyingassemblybindinginconfigurationfiles"></a>   
## Especificación del enlace de ensamblados en archivos de configuración  
 Use el mismo formato XML para especificar redirecciones de enlace si se encuentra en el archivo de configuración de la aplicación, el archivo de configuración del equipo o el archivo de directiva de edición. Para redirigir una versión del ensamblado a otra, use el elemento [\<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md). El atributo **oldVersion** puede especificar una versión de ensamblado única o un intervalo de versiones. El atributo `newVersion` debe especificar una única versión.  Por ejemplo, `<bindingRedirect oldVersion="1.1.0.0-1.2.0.0" newVersion="2.0.0.0"/>` especifica que el motor de tiempo de ejecución debe usar la versión 2.0.0.0 en lugar de las versiones de ensamblado comprendidas entre la versión 1.1.0.0 y la versión 1.2.0.0.  
  
 El siguiente ejemplo de código muestra una variedad de escenarios de redirección de enlace. En el ejemplo se especifica una redirección para un intervalo de versiones para `myAssembly` y una redirección de enlace único para `mySecondAssembly`. En el ejemplo también se especifica que dicho archivo de directiva de edición no invalidará las redirecciones de enlace para `myThirdAssembly`.  
  
 Para enlazar un ensamblado, debe especificar la cadena "urn:schemas\-microsoft\-com:asm.v1" con el atributo **xmlns** en la etiqueta [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md).  
  
```  
<configuration> <runtime> <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"> <dependentAssembly> <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <!-- Assembly versions can be redirected in app, publisher policy, or machine configuration files. --> <bindingRedirect oldVersion="1.0.0.0-2.0.0.0" newVersion="3.0.0.0" /> </dependentAssembly> <dependentAssembly> <assemblyIdentity name="mySecondAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" /> </dependentAssembly> <dependentAssembly> <assemblyIdentity name="myThirdAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <!-- Publisher policy can be set only in the app configuration file. --> <publisherPolicy apply="no" /> </dependentAssembly> </assemblyBinding> </runtime> </configuration>  
```  
  
### Limitación de enlaces de ensamblados a una versión específica  
 Puede usar el atributo **appliesTo** en el elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) de un archivo de configuración de la aplicación para redirigir las referencias de enlace de ensamblados a una versión específica de .NET Framework. Este atributo opcional usa un número de versión de .NET Framework para indicar a qué versión se aplica. Si no se especifica ningún atributo **appliesTo**, el elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) se aplica a todas las versiones de .NET Framework.  
  
 Por ejemplo, para redirigir el enlace para un ensamblado de .NET Framework 3.5, incluiría el siguiente código XML en el archivo de configuración de la aplicación.  
  
```  
<runtime> <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v3.5"> <dependentAssembly> <!-- assembly information goes here --> </dependentAssembly> </assemblyBinding> </runtime>  
```  
  
 Debe especificar la información de redirección en orden de versión. Por ejemplo, escriba la información de redirección de enlace de ensamblados para los ensamblados de .NET Framework 3.5 seguidos de los ensamblados de .NET Framework 4.5. Por último, especifique la información de redirección de enlace de ensamblados para cualquier redirección de ensamblados de .NET Framework que no use el atributo **appliesTo** y, por tanto, se aplica a todas las versiones de .NET Framework. Si hay un conflicto en la redirección, se usa la primera instrucción de redirección que coincida en el archivo de configuración.  
  
 Por ejemplo, para redirigir una referencia a un ensamblado de .NET Framework 3.5 y otra referencia a un ensamblado de .NET Framework 4, usaría el patrón que se muestra en el siguiente pseudocódigo.  
  
```  
<assemblyBinding xmlns="..." appliesTo="v3.5 "> <!—.NET Framework version 3.5 redirects here --> </assemblyBinding> <assemblyBinding xmlns="..." appliesTo="v4.0.30319"> <!—.NET Framework version 4.0 redirects here --> </assemblyBinding> <assemblyBinding xmlns="..."> <!-- redirects meant for all versions of the runtime --> </assemblyBinding>  
```  
  
## Vea también  
 [Cómo: Habilitar y deshabilitar redireccionamiento de enlaces automático](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)   
 [Elemento \<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md)   
 [Permiso de seguridad para la redirección de enlaces de ensamblados](../../../docs/framework/configure-apps/assembly-binding-redirection-security-permission.md)   
 [Ensamblados en Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Programar con ensamblados](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [Cómo el motor en tiempo de ejecución ubica ensamblados](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configurar aplicaciones](../../../docs/framework/configure-apps/index.md)   
 [Configurar aplicaciones de .NET Framework](http://msdn.microsoft.com/es-es/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)   
 [Esquema de la configuración de Common Language Runtime](../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Esquema de los archivos de configuración](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Cómo: Crear una directiva de publicador](../../../docs/framework/configure-apps/how-to-create-a-publisher-policy.md)