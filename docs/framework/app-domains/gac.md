---
title: "Cach&#233; global de ensamblados | Microsoft Docs"
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
  - "listas de control de acceso [.NET Framework]"
  - "ACL [.NET Framework]"
  - "ensamblados [.NET Framework], caché global de ensamblados"
  - "caché [.NET Framework], caché global de ensamblados"
  - "GAC (caché global de ensamblados)"
  - "caché global de ensamblados"
  - "caché global de ensamblados, acerca de"
ms.assetid: cf5eacd0-d3ec-4879-b6da-5fd5e4372202
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Cach&#233; global de ensamblados
Cada equipo donde se instala Common Language Runtime tiene una memoria caché de código denominada caché global de ensamblados.  La caché global de ensamblados almacena los ensamblados designados específicamente para ser compartidos por varias aplicaciones del equipo.  
  
 Se recomienda compartir los ensamblados mediante su instalación en la caché global de ensamblados sólo cuando sea necesario.  Como norma general, mantenga las dependencias de los ensamblados privadas y coloque los ensamblados en el directorio de la aplicación, a menos que sea explícitamente necesario compartir un ensamblado en concreto.  Además, no es necesario instalar los ensamblados en la caché global de ensamblados para que obtenga acceso a ellos el código de interoperabilidad COM o el código no administrado.  
  
> [!NOTE]
>  Habrá algunos escenarios en los que no desee instalar un ensamblado en la caché global de ensamblados.  Si coloca uno de los ensamblados que componen una aplicación en la memoria caché global de ensamblados, no podrá replicar ni instalar la aplicación utilizando el comando **xcopy** para copiar el directorio de la aplicación.  También debe mover el ensamblado en la caché global de ensamblados.  
  
 Existen dos formas de implementar un ensamblado en la memoria caché global de ensamblados:  
  
-   Usar un instalador diseñado para funcionar con la caché global de ensamblados.  Es la opción preferida para instalar ensamblados en la caché global de ensamblados.  
  
-   Utilice la herramienta de desarrollador [Caché global de ensamblados \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md), que se suministra con [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
    > [!NOTE]
    >  En escenarios de implementación, se recomienda utilizar Windows Installer para instalar los ensamblados en la caché global de ensamblados.  Utilice la herramienta Caché global de ensamblados solo en escenarios de desarrollo, porque no proporciona funciones de recuento de referencias de ensamblados y otras características que se incluyen con Windows Installer.  
  
 A partir de .NET Framework 4, la ubicación predeterminada de la caché global de ensamblados es **%windir%\\Microsoft.NET\\assembly**.  En versiones anteriores de .NET Framework, la ubicación predeterminada es **%windir%\\assembly**.  
  
 Con frecuencia, los administradores protegen el directorio systemroot con una lista de control de acceso \(ACL\) para controlar el acceso de escritura y ejecución.  Puesto que la caché global de ensamblados está instalada en un subdirectorio del directorio systemroot, hereda la lista \(ACL\) de dicho directorio.  Es recomendable que sólo puedan eliminar archivos de la caché global de ensamblados los usuarios que tengan privilegios de administrador.  
  
 Los ensamblados implementados en la caché global de ensamblados deben tener nombres seguros.  Cuando se agrega un ensamblado a la caché global de ensamblados, se realizan comprobaciones de integridad de todos los archivos que componen el ensamblado.  La caché realiza estas comprobaciones de integridad para garantizar que no se ha manipulado ningún ensamblado, por ejemplo, cuando se ha modificado un archivo pero el manifiesto no refleja el cambio.  
  
## Vea también  
 [Ensamblados en Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Trabajar con ensamblados y la memoria caché global de ensamblados](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Ensamblados con nombre seguro](../../../docs/framework/app-domains/strong-named-assemblies.md)