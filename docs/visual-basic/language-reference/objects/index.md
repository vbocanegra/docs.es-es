---
title: Objetos (Visual Basic) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- objects [Visual Basic]
ms.assetid: 651c73e4-dca8-402b-9c6b-e3902b3a3f4b
caps.latest.revision: 22
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 31905a37f09db5f5192123f0118252fbe8b02eff
ms.openlocfilehash: 6d4ed7e551c9a0d039f0206a86fa3a748dd728ef
ms.contentlocale: es-es
ms.lasthandoff: 06/12/2017

---
<a id="objects-visual-basic" class="xliff"></a>

# Objetos (Visual Basic)
En este tema se proporcionan vínculos a otros temas en los que se describen los objetos en tiempo de ejecución de Visual Basic y contienen tablas con sus procedimientos de miembro, propiedades y eventos.  
  
<a id="visual-basic-run-time-objects" class="xliff"></a>

## Objetos en tiempo de ejecución de Visual Basic  
  
|||  
|---|---|  
|<xref:Microsoft.VisualBasic.Collection>|Proporciona una cómoda manera de ver un grupo de elementos relacionado como un solo objeto.|  
|<xref:Microsoft.VisualBasic.Information.Err%2A>|Contiene información sobre los errores en tiempo de ejecución.|  
|El objeto `My.Application` consta de las clases siguientes:<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> proporciona miembros que están disponibles en todos los proyectos.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> proporciona miembros disponibles en aplicaciones de Windows Forms.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> proporciona miembros disponibles en aplicaciones de consola.|Proporciona datos asociados únicamente con la aplicación actual o el archivo DLL. No se puede modificar la información de nivel de sistema mediante `My.Application`.<br /><br /> Algunos miembros solo están disponibles para aplicaciones de consola o de Windows Forms.|  
|`My.Application.Info` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Info%2A>)|Proporciona propiedades para obtener información sobre una la aplicación, como el número de versión, la descripción, los ensamblados cargados, etc.|  
|`My.Application.Log` (<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log%2A>)|Proporciona una propiedad y métodos para escribir información de eventos y excepciones en los agentes de escucha de registro de la aplicación.|  
|`My.Computer` (<xref:Microsoft.VisualBasic.Devices.Computer>)|Proporciona propiedades para manipular componentes del equipo, como el audio, el reloj, el teclado, el sistema de archivos, etc.|  
|`My.Computer.Audio` (<xref:Microsoft.VisualBasic.Devices.Audio>)|Proporciona métodos para reproducir sonidos.|  
|`My.Computer.Clipboard` (<xref:Microsoft.VisualBasic.Devices.Computer.Clipboard%2A>)|Proporciona métodos para manipular el Portapapeles.|  
|`My.Computer.Clock` (<xref:Microsoft.VisualBasic.Devices.Clock>)|Proporciona propiedades para obtener acceso a la hora local actual y al Horario universal coordinado (equivalente a la Hora del meridiano de Greenwich) desde el reloj del sistema.|  
|`My.Computer.FileSystem` (<xref:Microsoft.VisualBasic.FileIO.FileSystem>)|Proporciona propiedades y métodos para trabajar con unidades, archivos y directorios.|  
|`My.Computer.FileSystem.SpecialDirectories` (<xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>)|Proporciona propiedades para obtener acceso a directorios a los que suele hacerse referencia.|  
|`My.Computer.Info` (<xref:Microsoft.VisualBasic.Devices.ComputerInfo>)|Proporciona propiedades para obtener información sobre la memoria, los ensamblados cargados, el nombre y el sistema operativo del equipo.|  
|`My.Computer.Keyboard` (<xref:Microsoft.VisualBasic.Devices.Keyboard>)|Proporciona propiedades para obtener acceso al estado actual del teclado, como las teclas que se han presionado, y proporciona un método para enviar pulsaciones de teclas a la ventana activa.|  
|`My.Computer.Mouse` (<xref:Microsoft.VisualBasic.Devices.Mouse>)|Proporciona propiedades para obtener información sobre el formato y la configuración del mouse instalado en el equipo local.|  
|`My.Computer.Network` (<xref:Microsoft.VisualBasic.Devices.Network>)|Proporciona una propiedad, un evento y métodos para interactuar con la red a la que está conectado el equipo.|  
|`My.Computer.Ports` (<xref:Microsoft.VisualBasic.Devices.Ports>)|Proporciona una propiedad y un método para obtener acceso a los puertos serie del equipo.|  
|`My.Computer.Registry` (<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>)|Proporciona propiedades y métodos para manipular el Registro.|  
|[My.Forms (objeto)](../../../visual-basic/language-reference/objects/my-forms-object.md)|Proporciona propiedades para obtener acceso a una instancia de cada formulario Windows Forms declarado en el proyecto actual.|  
|`My.Log` (<xref:Microsoft.VisualBasic.Logging.AspLog>)|Proporciona una propiedad y métodos para escribir información de eventos y excepciones en los agentes de escucha de registro de la aplicación para aplicaciones web.|  
|[My.Request (objeto)](../../../visual-basic/language-reference/objects/my-request-object.md)|Obtiene el objeto <xref:System.Web.HttpRequest> para la página solicitada. Objeto `My.Request` que contiene información sobre la solicitud HTTP actual.<br /><br /> El objeto `My.Request` solo está disponible para las aplicaciones [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)].|  
|[My.Resources (objeto)](../../../visual-basic/language-reference/objects/my-resources-object.md)|Proporciona propiedades y clases para obtener acceso a los recursos de una aplicación.|  
|[My.Response (objeto)](../../../visual-basic/language-reference/objects/my-response-object.md)|Obtiene el objeto <xref:System.Web.HttpResponse> asociado al <xref:System.Web.UI.Page>. Este objeto permite enviar datos de respuesta HTTP a un cliente y contiene información sobre esa respuesta.<br /><br /> El objeto `My.Response` solo está disponible para las aplicaciones [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)].|  
|[My.Settings (objeto)](../../../visual-basic/language-reference/objects/my-settings-object.md)|Proporciona propiedades y métodos para obtener acceso a la configuración de una aplicación.|  
|`My.User` (<xref:Microsoft.VisualBasic.ApplicationServices.User>)|Proporciona acceso a información sobre el usuario actual.|  
|[My.WebServices (objeto)](../../../visual-basic/language-reference/objects/my-webservices-object.md)|Proporciona propiedades para crear y obtener acceso a una sola instancia de cada servicio web al que hace referencia el proyecto actual.|  
|<xref:Microsoft.VisualBasic.FileIO.TextFieldParser>|Proporciona los métodos y propiedades para analizar archivos de texto estructurados.|  
  
<a id="see-also" class="xliff"></a>

## Vea también  
 [Referencia del lenguaje Visual Basic](../../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../../visual-basic/index.md)
