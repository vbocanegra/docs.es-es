---
title: Implementar .NET Framework y aplicaciones | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- deploying applications [.NET Framework], packaging
- deploying applications [.NET Framework]
- deploying applications [.NET Framework], features
- deploying applications [.NET Framework], distribution
- .NET Framework, deploying
- .NET Framework application deployment
ms.assetid: 238d8284-6042-4a38-a7f6-1ee8efd719da
caps.latest.revision: 56
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: fe9ab371ab8d3eee3778412e446b7aa30b42476b
ms.openlocfilehash: 46f524a8c2ee2d65d5c756a101a5c26c5919e165
ms.contentlocale: es-es
ms.lasthandoff: 06/12/2017

---
# Implementar .NET Framework y aplicaciones
<a id="deploying-the-net-framework-and-applications" class="xliff"></a>
Este artículo le ayuda a empezar a implementar .NET Framework con la aplicación. La mayoría de la información está destinada a desarrolladores, OEM y administradores de empresa. Los usuarios que deseen instalar .NET Framework en sus equipos deben leer [Instalar .NET Framework](~/docs/framework/install/index.md).  
  
## Recursos de implementación clave
<a id="key-deployment-resources" class="xliff"></a>  
 Use los siguientes vínculos a otros temas de MSDN para obtener información específica sobre la implementación y mantenimiento de .NET Framework.  
  
 **Instalación e implementación**  
  
-   Información general para el instalador y la implementación:  
  
    -   Opciones del instalador:  
  
        -   [Instalador web](~/docs/framework/install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)  
  
        -   [Instalador sin conexión](~/docs/framework/install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)  
  
    -   Modos de instalación:  
  
        -   [Instalación silenciosa](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining_custom)  
  
        -   [Mostrar una interfaz de usuario](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining_default)  
  
    -   [Reducir los reinicios del sistema durante las instalaciones de .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md)  
  
    -   [Solución de problemas en instalaciones y desinstalaciones bloqueadas de .NET Framework](~/docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)  
  
-   Implementar .NET Framework con una aplicación cliente (para desarrolladores):  
  
    -   [Usar InstallShield](../../../docs/framework/deployment/deployment-guide-for-developers.md#installshield-deployment) en un proyecto de instalación e implementación  
  
    -   [Usar una aplicación ClickOnce de Visual Studio](../../../docs/framework/deployment/deployment-guide-for-developers.md#clickonce-deployment)  
  
    -   [Crear un paquete de instalación de WiX](../../../docs/framework/deployment/deployment-guide-for-developers.md#wix)  
  
    -   [Usar un instalador personalizado](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining)  
  
    -   [Información adicional](../../../docs/framework/deployment/deployment-guide-for-developers.md) para desarrolladores  
  
-   Implementar .NET Framework (para OEM y administradores):  
  
    -   [Windows Assessment and Deployment Kit (ADK)](http://go.microsoft.com/fwlink/p/?LinkId=254976)  
  
    -   [Guía del administrador](../../../docs/framework/deployment/guide-for-administrators.md)  
  
 **Mantenimiento**  
  
-   Para obtener información general, vea el [blog de .NET Framework](http://go.microsoft.com/fwlink/p/?LinkId=254977)  
  
-   [Detectar versiones](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)  
  
-   [Detectar Service Pack y actualizaciones](../../../docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)  
  
## Características que simplifican la implementación
<a id="features-that-simplify-deployment" class="xliff"></a>  
 .NET Framework proporciona algunas características básicas que facilitan la implementación de las aplicaciones:  
  
-   Aplicaciones carentes de impacto.  
  
     Esta característica permite aislar la aplicación y eliminar conflictos de archivos DLL. De forma predeterminada, los componentes no afectan a otras aplicaciones  
  
-   Componentes privados predeterminados.  
  
     De forma predeterminada, los componentes se implementan en el directorio de la aplicación y sólo son visibles para la aplicación en la que están incluidos.  
  
-   Uso compartido de código controlado.  
  
     El uso compartido de código no es el comportamiento predeterminado; para compartir código, es necesario que este quede explícitamente disponible para el uso compartido.  
  
-   Control de versiones en paralelo.  
  
     Es posible que coexistan varias versiones de un componente o de una aplicación; el usuario puede elegir las versiones que desea utilizar, y Common Language Runtime impone la directiva de control de versiones.  
  
-   Implementación y duplicación mediante XCOPY.  
  
     Los componentes y aplicaciones autodescriptivos e independientes pueden implementarse sin entradas del Registro o dependencias.  
  
-   Actualizaciones inmediatas.  
  
     Los administradores pueden utilizar servidores host, como ASP.NET, para actualizar programas de archivos DLL, incluso en equipos remotos.  
  
-   Integración con Windows Installer.  
  
     A la hora de implementar la aplicación, estarán disponibles las características de anuncio, edición, reparación e instalación a petición.  
  
-   Implementación de empresa.  
  
     Esta característica proporciona una distribución de software sencilla, que incluye el uso de Active Directory.  
  
-   Descarga y almacenamiento en caché.  
  
     Las descargas incrementales reducen el tamaño de las mismas, y los componentes pueden aislarse a fin de que solo los use la aplicación para una implementación de bajo impacto.  
  
-   Código que no es de plena confianza.  
  
     La identidad no se basa en el usuario sino en el código y no aparece ningún cuadro de diálogo de certificado.  
  
## Empaquetar y distribuir aplicaciones de .NET Framework
<a id="packaging-and-distributing-net-framework-applications" class="xliff"></a>  
 Parte de la información relacionada con el empaquetado y la implementación de .NET Framework se describe en otras secciones de la documentación. En esas secciones se proporciona información sobre los [ensamblados](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md), que son unidades autodescriptivas que no necesitan entradas del Registro, los [ensamblados con nombre seguro](../../../docs/framework/app-domains/strong-named-assemblies.md), que garantizan el carácter unívoco del nombre e impiden la simulación de este, y el [control de versiones de los ensamblados](../../../docs/framework/app-domains/assembly-versioning.md), que aborda muchos de los problemas asociados a conflictos de archivos DLL. En las siguientes secciones, se proporciona información sobre cómo se empaquetan y se distribuyen las aplicaciones de .NET Framework.  
  
### Empaquetado
<a id="packaging" class="xliff"></a>  
 .NET Framework proporciona las siguientes opciones para empaquetar aplicaciones:  
  
-   Como un solo ensamblado o como una colección de ensamblados.  
  
     Con esta opción, simplemente se emplean los archivos.dll o .exe tal y como se compilaron.  
  
-   Como archivos contenedores (CAB).  
  
     Con esta opción, los archivos se comprimen en archivos .cab para disminuir el tiempo de distribución y descarga.  
  
-   Como un paquete de Microsoft Windows Installer o en otros formatos de instalación.  
  
     Con esta opción, se crean archivos .msi para usarlos con Windows Installer o se empaqueta la aplicación para utilizarla con otro instalador.  
  
### Distribución
<a id="distribution" class="xliff"></a>  
 .NET Framework proporciona las siguientes opciones para distribuir aplicaciones:  
  
-   Utilizar XCOPY o FTP.  
  
     Como las aplicaciones de tipo Common Language Runtime son autodescriptivas y no precisan entradas del Registro, se puede utilizar XCOPY o FTP simplemente para copiar la aplicación en un directorio adecuado. La aplicación puede entonces ejecutarse desde ese directorio.  
  
-   Emplear descarga de código.  
  
     Si la aplicación se está distribuyendo a través de Internet o de una intranet corporativa, puede simplemente descargar el código en un equipo y ejecutar la aplicación allí mismo.  
  
-   Utilizar un programa de instalación como Windows Installer 2.0.  
  
     Windows Installer 2.0 puede instalar, reparar o quitar ensamblados de .NET Framework de la memoria caché global de ensamblados y de directorios privados.  
  
### Ubicación de instalación
<a id="installation-location" class="xliff"></a>  
 Para determinar la ubicación donde se van a implementar los ensamblados de la aplicación para que el runtime los encuentre, vea [Cómo el motor en tiempo de ejecución ubica ensamblados](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
 Las cuestiones de seguridad pueden afectar también al modo en que se implementa la aplicación. Los permisos de seguridad se conceden al código administrado según la ubicación del código. Si se implementa una aplicación o un componente en una ubicación donde reciba poca confianza, como Internet, se verán limitadas las funciones de dicha aplicación o dicho componente. Para obtener más información sobre la implementación y la seguridad, vea [Conceptos básicos sobre la seguridad de acceso del código](../../../docs/framework/misc/code-access-security-basics.md).  
  
## Temas relacionados
<a id="related-topics" class="xliff"></a>  
  
|Título|Descripción|  
|-----------|-----------------|  
|[Cómo el motor en tiempo de ejecución ubica ensamblados](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)|Describe la forma en que Common Language Runtime determina el ensamblado que se va a utilizar para llevar a cabo una solicitud de enlace.|  
|[Procedimientos recomendados para cargar ensamblados](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)|Aborda formas de evitar problemas de identidad de tipos que pueden causar errores como <xref:System.InvalidCastException> o <xref:System.MissingMethodException>, entre otros.|  
|[Reducir los reinicios del sistema durante las instalaciones de .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md)|Describe el Administrador de reinicio, que evita, en la medida de lo posible, los reinicios del equipo y explica cómo pueden aprovecharlo las aplicaciones que instalan .NET Framework.|  
|[Guía de implementación para administradores](../../../docs/framework/deployment/guide-for-administrators.md)|Explica cómo un administrador del sistema puede implementar .NET Framework y sus dependencias del sistema en una red utilizando System Center Configuration Manager (SCCM).|  
|[Guía de implementación para desarrolladores](../../../docs/framework/deployment/deployment-guide-for-developers.md)|Explica cómo los desarrolladores de software pueden instalar .NET Framework en los equipos de los usuarios con sus aplicaciones.|  
|[Implementar aplicaciones, servicios y componentes](https://docs.microsoft.com/visualstudio/deployment/deploying-applications-services-and-components)|Describe las opciones de implementación de Visual Studio e incluye instrucciones para publicar una aplicación mediante las tecnologías ClickOnce y Windows Installer.| 
|[Publicar aplicaciones ClickOnce](/visualstudio/deployment/publishing-clickonce-applications)|Describe cómo empaquetar una aplicación de Windows Forms e implementarla con ClickOnce en los equipos cliente en una red.|  
|[Empaquetar e implementar recursos](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)|Describe el modelo de concentrador y de radio que .NET Framework usa para empaquetar e implementar los recursos; aborda las convenciones de nomenclatura de los recursos, el proceso de reserva y las alternativas de empaquetado.|  
|[Implementar una aplicación interoperativa](../../../docs/framework/interop/deploying-an-interop-application.md)|Explica cómo distribuir e instalar aplicaciones de interoperabilidad, que suelen incluir un ensamblado de cliente de .NET Framework, uno o varios ensamblados de interoperabilidad que representan diferentes bibliotecas de tipos COM, y uno o varios componentes COM registrados.|  
|[Cómo: Obtener el progreso del instalador de .NET Framework 4.5](../../../docs/framework/deployment/how-to-get-progress-from-the-dotnet-installer.md)|Describe cómo iniciar y seguir en modo silencioso el proceso de instalación de .NET Framework, mientras se muestra la vista del progreso de la instalación.|  
  
## Vea también
<a id="see-also" class="xliff"></a>  
 [Guía de desarrollo](../../../docs/framework/development-guide.md)

