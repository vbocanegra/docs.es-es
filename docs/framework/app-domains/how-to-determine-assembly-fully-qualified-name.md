---
title: "C&#243;mo: Determinar el nombre completo de un ensamblado | Microsoft Docs"
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
  - "ensamblados [.NET Framework], nombres"
  - "nombres [.NET Framework], ensamblados"
  - "nombres [.NET Framework], nombres de tipo completos"
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# C&#243;mo: Determinar el nombre completo de un ensamblado
Para conocer el nombre completo de un ensamblado de la caché global de ensamblados, use la herramienta Caché global de ensamblados \([Gacutil.exe](../../../docs/framework/tools/gacutil-exe-gac-tool.md)\).  Consulte [Cómo: Consultar el contenido de la memoria caché global de ensamblados](../../../docs/framework/app-domains/how-to-view-the-contents-of-the-gac.md).  
  
 Para los ensamblados que no están en la caché global de ensamblados, puede obtener el nombre completo del ensamblado de varias formas: puede usar código para enviar la información a la consola o a una variable, o puede usar el [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) para examinar los metadatos del ensamblado, que contienen el nombre completo.  
  
-   Si el ensamblado ya está cargado por la aplicación, puede recuperar el valor de la propiedad <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName> para obtener el nombre completo.  Puede usar este enfoque tanto si el ensamblado está en la GAC como si no.  En este ejemplo se ilustra.  
  
-   Si conoce la ruta del sistema de archivos del ensamblado, puede llamar al método estático \(`Shared` en Visual Basic\) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=fullName> para obtener el nombre completo del ensamblado.  El siguiente es un ejemplo sencillo.  
  
     [!code-csharp[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/cs/getassemblyname1.cs#1)]
     [!code-vb[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/vb/getassemblyname1.vb#1)]  
  
-   Puede usar el [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) para examinar los metadatos del ensamblado, que contiene el nombre completo.  
  
 Para obtener más información acerca de cómo establecer los atributos del ensamblado, como la versión, la referencia cultural y el nombre de ensamblado, consulte [Configurar atributos de ensamblados](../../../docs/framework/app-domains/set-assembly-attributes.md).  Para obtener más información acerca de cómo dar un nombre seguro a un ensamblado, consulte [Crear y utilizar ensamblados con nombre seguro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md).  
  
## Ejemplo  
 En el siguiente ejemplo de código se indica cómo mostrar el nombre completo de un ensamblado que contiene una clase especificada en la consola.  Como recupera el nombre de un ensamblado que la aplicación ya ha cargado, no importa si el ensamblado está en la GAC.  
  
 [!code-cpp[Assembly.Fullname#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.FullName/CPP/example2.cpp#2)]
 [!code-csharp[Assembly.Fullname#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.FullName/CS/example2.cs#2)]
 [!code-vb[Assembly.Fullname#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.FullName/VB/example2.vb#2)]  
  
## Vea también  
 [Nombres de ensamblado](../../../docs/framework/app-domains/assembly-names.md)   
 [Crear ensamblados](../../../docs/framework/app-domains/create-assemblies.md)   
 [Crear y utilizar ensamblados con nombre seguro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)   
 [Caché global de ensamblados](../../../docs/framework/app-domains/gac.md)   
 [Cómo el motor en tiempo de ejecución ubica ensamblados](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Programar con ensamblados](../../../docs/framework/app-domains/programming-with-assemblies.md)