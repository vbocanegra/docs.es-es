---
title: "Cómo determinar qué actualizaciones de .NET Framework están instaladas | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updates, determining for .NET Framework
- .NET Framework, determining updates
ms.assetid: 53c7b5f7-d47a-402a-b194-7244a696a88b
caps.latest.revision: 6
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 14abadaf548e228244a1ff7ca72fa3896ef4eb5d
ms.openlocfilehash: 6a6e4c9c2bdacc01f82d3a53aec706809bcfaa5a
ms.contentlocale: es-es
ms.lasthandoff: 06/12/2017

---
<a id="how-to-determine-which-net-framework-updates-are-installed" class="xliff"></a>

# Cómo: Determinar qué actualizaciones de .NET Framework están instaladas
Las actualizaciones instaladas para cada versión de .NET Framework instalada en un equipo se enumeran en el Registro de Windows. Puede utilizar el Editor del Registro (regedit.exe) para ver esta información.  
  
 En el Editor del Registro, las versiones de .NET Framework y las actualizaciones instaladas para cada versión se almacenan en diferentes subclaves. Para obtener información sobre cómo detectar los números de la versión instalada, consulte [Cómo: Determinar qué versiones de .NET Framework están instaladas](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md). Para obtener información sobre cómo instalar .NET Framework, consulte [Install the .NET Framework for developers](../../../docs/framework/install/guide-for-developers.md) (Instalar .NET Framework para desarrolladores).  
  
<a id="to-find-installed-updates" class="xliff"></a>

### Para buscar las actualizaciones instaladas  
  
1.  Abra el programa **regedit.exe**. En Windows 8 y versiones posteriores, abra la pantalla Inicio y escriba el nombre. En versiones anteriores de Windows, en el menú **Iniciar**, elija **Ejecutar** y, después, en el cuadro **Abrir**, escriba **regedit.exe**.  
  
     Debe tener credenciales de administrador para ejecutar regedit.exe.  
  
2.  En el Editor del Registro, abra la subclave siguiente:  
  
     HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Updates  
  
     Las actualizaciones instaladas se muestran bajo subclaves que identifican la versión de .NET Framework a la que se aplican. Cada actualización se identifica mediante un número de la Knowledge Base (KB).  
  
<a id="example" class="xliff"></a>

## Ejemplo  
 El código siguiente determina mediante programación las actualizaciones de .NET Framework instaladas en un equipo. Debe tener credenciales administrativas para ejecutar este ejemplo.  
  
 [!code-csharp[ListUpdates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/listupdates/cs/program.cs#1)] [!code-vb[ListUpdates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/listupdates/vb/program.vb#1)]  
  
 El ejemplo genera un resultado similar al siguiente:  
  
```  
Microsoft .NET Framework 3.5 SP1  
  KB953595  Hotfix for Microsoft .NET Framework 3.5 SP1 (KB953595)  
  SP1  
    KB2657424  Security Update for Microsoft .NET Framework 3.5 SP1 (KB2657424)  
    KB958484  Hotfix for Microsoft .NET Framework 3.5 SP1 (KB958484)  
    KB963707  Update for Microsoft .NET Framework 3.5 SP1 (KB963707)  
Microsoft .NET Framework 4 Client Profile  
  KB2160841  Security Update for Microsoft .NET Framework 4 Client Profile (KB2160841)  
  KB2446708  Security Update for Microsoft .NET Framework 4 Client Profile (KB2446708)  
  KB2468871  Update for Microsoft .NET Framework 4 Client Profile (KB2468871)  
  KB2478663  Security Update for Microsoft .NET Framework 4 Client Profile (KB2478663)  
  KB2518870  Security Update for Microsoft .NET Framework 4 Client Profile (KB2518870)  
  KB2533523  Update for Microsoft .NET Framework 4 Client Profile (KB2533523)  
  KB2539636  Security Update for Microsoft .NET Framework 4 Client Profile (KB2539636)  
  KB2572078  Security Update for Microsoft .NET Framework 4 Client Profile (KB2572078)  
  KB2633870  Security Update for Microsoft .NET Framework 4 Client Profile (KB2633870)  
  KB2656351  Security Update for Microsoft .NET Framework 4 Client Profile (KB2656351)  
Microsoft .NET Framework 4 Extended  
  KB2416472  Security Update for Microsoft .NET Framework 4 Extended (KB2416472)  
  KB2468871  Update for Microsoft .NET Framework 4 Extended (KB2468871)  
  KB2487367  Security Update for Microsoft .NET Framework 4 Extended (KB2487367)  
  KB2533523  Update for Microsoft .NET Framework 4 Extended (KB2533523)  
  KB2656351  Security Update for Microsoft .NET Framework 4 Extended (KB2656351)  
```  
  
<a id="see-also" class="xliff"></a>

## Vea también

[Cómo: Determinar qué versiones de .NET Framework están instaladas](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)   
[Instalar .NET Framework](../../../docs/framework/install/guide-for-developers.md)   
[Versiones y dependencias](../../../docs/framework/migration-guide/versions-and-dependencies.md)

