---
title: "Ejemplo de Web Services Generics Serialization Technology | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cdc15ea4-f678-4729-8ebe-188ae720bef7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Ejemplo de Web Services Generics Serialization Technology
[Descargar ejemplo](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/GenericsSerialization.zip.exe)  
  
 Este ejemplo muestra cómo utilizar y controlar la serialización de genéricos en servicios Web ASP.NET.  
  
### Para generar el ejemplo mediante Visual Studio  
  
1.  Abra Visual Studio y seleccione **Nuevo sitio web** en el menú **Archivo**.  
  
2.  En el panel izquierdo del cuadro de diálogo **Nuevo sitio web**, seleccione su lenguaje de programación deseado y, a continuación, en el panel derecho, seleccione **Servicio Web ASP.NET**.  
  
3.  Haga clic en **Examinar** y desplácese hasta el subdirectorio del \\CS\\GenericsService.  
  
4.  Seleccione Service.asmx para abrir el archivo en Visual Studio.  
  
5.  En el menú **Compilar**, haga clic en **Compilar solución**.  
  
> [!NOTE]
>  Los primeros cinco pasos en esta lista son opcionales.El runtime de .NET Framework generará automáticamente el servicio Web la primera vez que se solicita el servicio.  
  
> [!NOTE]
>  Los siguientes pasos son obligatorios para generar el ejemplo.  
  
1.  Abra el [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)] y navegue hasta el subdirectorio \\CS.  
  
2.  Haga clic con el botón secundario en el icono del subdirectorio GenericsService y seleccione **Compartir y seguridad**.  
  
3.  En la pestaña **Uso compartido de web**, seleccione **Compartir esta carpeta**.  
  
> [!IMPORTANT]
>  Tome nota del nombre del directorio virtual que aparece en la lista en el panel **Alias**, porque necesitará para ejecutar el ejemplo.  
  
### Para generar el ejemplo mediante Internet Information Services  
  
1.  Abra el complemento de administración de **Internet Information Services** y expanda **Sitios web**.  
  
2.  Haga clic en **Sitio web predeterminado** y seleccione **Nuevo**, **Directorio virtual** para crear el **Asistente para crear un directorio virtual**.  
  
3.  Haga clic en **Siguiente**, escriba el alias público para su directorio virtual y haga clic en **Siguiente**.  
  
4.  Escriba la ruta de acceso al directorio donde guardó el ejemplo \(normalmente el subdirectorio del \\CS\\GenericsService\) y haga clic en **Siguiente**.Haga clic en **Siguiente** para cerrar el asistente.  
  
> [!IMPORTANT]
>  Tome nota del nombre del directorio virtual que aparece en la lista en el panel **Alias**, porque necesitará para ejecutar el ejemplo.  
  
### Para ejecutar el ejemplo  
  
1.  Abra una ventana del explorador y seleccione su barra de direcciones.  
  
2.  Escriba  **http:\/\/localhost\/**\[directorio virtual\]**\/Service.asmx**, donde \[directorio virtual\] representa el directorio virtual que creó cuando generó el ejemplo.  
  
## Comentarios  
 En el ejemplo se muestra una página ASP.NET predeterminada que contiene los vínculos a la definición del servicio Web.Puede personalizar la presentación además de modificar el código fuente del servicio Web.Para obtener más información, vea [Building XML Web Service Clients](http://msdn.microsoft.com/es-es/c606f3cb-4111-45b4-ae42-9300420fa16c).  
  
## Vea también  
 <xref:System.Collections.Generic>   
 <xref:System.Web.Services>   
 <xref:System.Xml.Serialization>   
 [Serialización](../../../docs/framework/serialization/index.md)   
 [XML Web Services Created Using ASP.NET and XML Web Service Clients](http://msdn.microsoft.com/es-es/1e64af78-d705-4384-b08d-591a45f4379c)