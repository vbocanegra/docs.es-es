---
title: "C&#243;mo: Instalar un ensamblado en la memoria cach&#233; global de ensamblados | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ensamblados [.NET Framework], caché global de ensamblados"
  - "Gacutil.exe"
  - "Caché global de ensamblados (herramienta)"
  - "caché global de ensamblados, instalar ensamblados"
  - "ensamblados con nombre seguro, caché global de ensamblados"
ms.assetid: a7e6f091-d02c-49ba-b736-7295cb0eb743
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# C&#243;mo: Instalar un ensamblado en la memoria cach&#233; global de ensamblados
Hay dos formas de instalar un ensamblado con nombre seguro en la memoria caché global de ensamblados \(GAC\):  
  
> [!IMPORTANT]
>  En la memoria caché global de ensamblados solamente se pueden instalar ensamblados con nombre seguro.  Para obtener información sobre cómo crear un ensamblado de este tipo, vea [Cómo: Firmar un ensamblado con un nombre seguro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  
  
-   Uso de [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx).  
  
     Esto se hace en Visual Studio 2012 y Visual Studio 2013 mediante la creación de un proyecto de InstallShield Limited Edition.  
  
     Esta es la forma recomendada y más normal de agregar ensamblados a la caché global de ensamblados.  El instalador proporciona el recuento de referencias de los ensamblados de la caché global de ensamblados, además de otras ventajas.  
  
-   Utilizar la [herramienta Caché global de ensamblados \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
     Gacutil.exe se puede utilizar para agregar ensamblados con nombre seguro a la caché global de ensamblados y ver el contenido de dicha caché.  
  
    > [!NOTE]
    >  Gacutil.exe sólo debe usarse para programación y no para instalar ensamblados de producción en la caché global de ensamblados.  
  
> [!NOTE]
>  En versiones anteriores de .NET Framework, la extensión Shfusion.dll del shell de Windows le permitía instalar ensamblados arrastrándolos en el Explorador de archivos.  A partir de [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Shfusion.dll está obsoleto.  
  
### Para usar la herramienta Caché global de ensamblados \(Gacutil.exe\)  
  
1.  En el símbolo del sistema, escriba el siguiente comando:  
  
     **gacutil \-i** \<*nombre del ensamblado*\>  
  
     En este comando, *nombre del ensamblado* es el nombre del ensamblado que se va a instalar en la caché global de ensamblados.  
  
 En el ejemplo siguiente se instala un ensamblado con el nombre de archivo `hello.dll` en la caché global de ensamblados.  
  
```  
gacutil -i hello.dll  
```  
  
 Para obtener más información, vea [Herramienta Caché global de ensamblados \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
### Para usar un proyecto InstallShield Limited Edition  
  
1.  Agregue un paquete de instalación e implementación a la solución. Para ello, abra el menú contextual de la solución y, a continuación, elija **Agregar**, **Nuevo proyecto**.  
  
2.  En la carpeta **Instalado** del cuadro de diálogo **Agregar nuevo proyecto**, elija **Otros tipos de proyectos**, **Instalación e implementación** e **InstallShield Limited Edition** y asigne un nombre al proyecto.  \(En caso necesario, descargue, instale y active InstallShield\).  
  
3.  Aplique la configuración general del proyecto de instalación e implementación mediante el asistente para proyectos del **Explorador de soluciones** o los pasos secundarios de los pasos numerados en el **Explorador de soluciones**.  Configure su instalación como si no fuese a agregar ensamblados a la GAC.  
  
4.  Para iniciar el proceso de adición de un ensamblado a la memoria caché global de ensamblados, elija **Archivos**, bajo el paso **Especifique los datos de la aplicación** en el **Explorador de soluciones**.  
  
5.  En el panel **Destination computer's folders**, abra el menú contextual de **Destination Computer**y, a continuación, **Show Predefined Folder**, **\[GlobalAssemblyCache\]**.  
  
6.  Para cada proyecto de la solución que contenga un ensamblado que desee instalar en la memoria caché global de ensamblados:  
  
    1.  En el panel **Source computer's folders**, elija el proyecto.  
  
    2.  En el panel **Destination computer's folders**, elija **\[GlobalAssemblyCache\]**.  
  
    3.  En el panel **Source computer's files**, elija **Primary output from** *\<nombre\_proyecto\>*.  
  
    4.  Arrastre el archivo del paso c al panel **Destination computer's files** \(o use los comandos **Copiar** y **Pegar** del menú contextual del archivo\).  
  
## Vea también  
 [Trabajar con ensamblados y la memoria caché global de ensamblados](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Cómo: Quitar un ensamblado de la memoria caché global de ensamblados](../../../docs/framework/app-domains/how-to-remove-an-assembly-from-the-gac.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)   
 [Cómo: Firmar un ensamblado con un nombre seguro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)   
 [Windows Installer Deployment](http://msdn.microsoft.com/es-es/121be21b-b916-43e2-8f10-8b080516d2a0)