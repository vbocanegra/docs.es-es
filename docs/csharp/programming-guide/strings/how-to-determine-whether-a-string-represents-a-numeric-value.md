---
title: "Cómo: Determinar si una cadena representa un valor numérico (Guía de programación de C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- numeric strings [C#]
- validating numeric input [C#]
- strings [C#], numeric
ms.assetid: a4e84e10-ea0a-489f-a868-503dded9d85f
caps.latest.revision: 9
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 343e7304a83f396b8bdcc9c92e9123eed206be56
ms.contentlocale: es-es
ms.lasthandoff: 05/10/2017

---
# <a name="how-to-determine-whether-a-string-represents-a-numeric-value-c-programming-guide"></a>Cómo: Determinar si una cadena representa un valor numérico (Guía de programación de C#)
Para determinar si una cadena es una representación válida de un tipo numérico especificado, use el método estático `TryParse` implementado por todos los tipos numéricos primitivos y también por tipos como <xref:System.DateTime> y <xref:System.Net.IPAddress>. En el ejemplo siguiente se muestra cómo determinar si "108" es un valor [int](../../../csharp/language-reference/keywords/int.md) válido.  
  
```  
int i = 0;   
string s = "108";  
bool result = int.TryParse(s, out i); //i now = 108  
```  
  
 Si la cadena contiene caracteres no numéricos o el valor numérico es demasiado grande o demasiado pequeño para el tipo determinado que ha especificado, `TryParse` devuelve el valor false y establece el parámetro out en cero. De lo contrario, devuelve el valor true y establece el parámetro out en el valor numérico de la cadena.  
  
> [!NOTE]
>  Una cadena puede contener solamente caracteres numéricos pero no ser válida para el tipo cuyo método `TryParse` se está usando. Por ejemplo, "256" no es un valor válido para `byte` pero sí para `int`. "98,6" no es un valor válido para `int` pero sí para `decimal`.  
  
## <a name="example"></a>Ejemplo  
 En los ejemplos siguientes se muestra cómo usar `TryParse` con representaciones de cadena de los valores `long`, `byte` y `decimal`.  
  
 [!code-cs[csProgGuideStrings#14](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-determine-whether-a-string-represents-a-numeric-value_1.cs)]  
  
## <a name="robust-programming"></a>Programación sólida  
 Los tipos numéricos primitivos también implementan el método estático `Parse`, que produce una excepción si la cadena no es un número válido. `TryParse` es, en general, más eficaz porque simplemente devuelve false si el número no es válido.  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 Use siempre los métodos `TryParse` o `Parse` para validar los datos proporcionados por el usuario en controles como cuadros de texto y cuadros combinados.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: Convertir una matriz de bytes en un valor int](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md)   
 [Cómo: Convertir una cadena en un número](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)   
 [Cómo: Convertir cadenas hexadecimales en tipos numéricos](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)   
 [Análisis de cadenas numéricas](../../../standard/base-types/parsing-numeric.md)   
 [Aplicación de formato a tipos](../../../standard/base-types/formatting-types.md)
