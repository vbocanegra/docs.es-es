---
title: "Interoperabilidad (Guía de programación de C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- COM interop
- interoperability
- platform invoke, accessing APIs with C#
- C# language, interoperability
ms.assetid: 238bb95a-e962-4026-bbd5-197055bdb8ee
caps.latest.revision: 31
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: be95d675d22dedcbf45c8eb1e8fd8d9f5ce0b56c
ms.contentlocale: es-es
ms.lasthandoff: 06/12/2017

---
<a id="interoperability-c-programming-guide" class="xliff"></a>

# Interoperabilidad (Guía de programación de C#)
La interoperabilidad permite conservar y aprovechar las inversiones existentes en código no administrado. El código que se ejecuta bajo el control de Common Language Runtime (CLR) se denomina *código administrado*, y el código que se ejecuta fuera de CLR se denomina *código no administrado*. COM, COM+, los componentes de C++, los componentes de ActiveX y la API Win32 de Microsoft son ejemplos de código no administrado.  
  
 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] habilita la interoperabilidad con código no administrado a través de los servicios de invocación de plataforma, el espacio de nombres <xref:System.Runtime.InteropServices>, la interoperabilidad de C++ y la interoperabilidad COM.  
  
<a id="in-this-section" class="xliff"></a>

## En esta sección  
 [Información general sobre interoperabilidad](../../../csharp/programming-guide/interop/interoperability-overview.md)  
 Se describen métodos para habilitar la interoperabilidad entre el código administrado y el código no administrado de C#.  
  
 [Cómo: Tener acceso a objetos de interoperabilidad de Office mediante las características de Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)  
 Describe las características introducidas en Visual C# para facilitar la programación de Office.  
  
 [Cómo: Utilizar propiedades indizadas en la programación de interoperabilidad COM](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)  
 Se describe cómo utilizar las propiedades indizadas para acceder a las propiedades de COM que tienen parámetros.  
  
 [Cómo: Utilizar la invocación de plataforma para reproducir un archivo de sonido](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md)  
 Se describe cómo usar los servicios de invocación de plataforma para reproducir un archivo de sonido .wav en el sistema operativo Windows.  
  
 [Tutorial: Programación de Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)  
 Muestra cómo crear un libro de Excel y un documento de Word que contiene un vínculo al libro.  
  
 [Clase COM de ejemplo](../../../csharp/programming-guide/interop/example-com-class.md)  
 Muestra cómo exponer una clase de C# como un objeto COM.  
  
<a id="c-language-specification" class="xliff"></a>

## Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
<a id="see-also" class="xliff"></a>

## Vea también  
 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=fullName>   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Interoperating with Unmanaged Code](https://msdn.microsoft.com/library/sd10k43k)  (Interoperabilidad con código no administrado)  
 [Tutorial: Programación de Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)
