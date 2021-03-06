---
title: Comparaciones y ordenaciones en colecciones | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sorting data, collections
- IComparable.CompareTo method
- Collections classes
- Equals method
- collections [.NET Framework], comparisons
ms.assetid: 5e4d3b45-97f0-423c-a65f-c492ed40e73b
caps.latest.revision: 11
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0da0bed43cb7871f522b94b134afb164d8ee3ab5
ms.lasthandoff: 04/18/2017

---
# <a name="comparisons-and-sorts-within-collections"></a>Comparaciones y ordenaciones en colecciones
Las clases <xref:System.Collections> realizan comparaciones en casi todos los procesos implicados en la administración de colecciones, ya sea al buscar el elemento que se va a quitar o al devolver el valor de un par clave-valor.  
  
 Normalmente, las colecciones usan un comparador de igualdad o un comparador de orden. En las comparaciones se usan dos constructores.  
  
<a name="BKMK_Checkingforequality"></a>   
## <a name="checking-for-equality"></a>Comprobar la igualdad  
 Los métodos como `Contains`, <xref:System.Collections.IList.IndexOf%2A>, <xref:System.Collections.Generic.List%601.LastIndexOf%2A> y `Remove` usan un comparador de igualdad para los elementos de la colección. Si la colección es genérica, se compara la igualdad de los elementos según las siguientes directrices:  
  
-   Si el tipo T implementa la interfaz genérica <xref:System.IEquatable%601>, el comparador de igualdad es el método <xref:System.IEquatable%601.Equals%2A> de dicha interfaz.  
  
-   Si el tipo T no implementa <xref:System.IEquatable%601>, se usa <xref:System.Object.Equals%2A?displayProperty=fullName>.  
  
 Además, algunas sobrecargas de constructores para colecciones de diccionario aceptan una implementación de <xref:System.Collections.Generic.IEqualityComparer%601>, que se usa para comparar la igualdad de claves. Para obtener un ejemplo, vea el constructor de <xref:System.Collections.Generic.Dictionary%602.%23ctor%2A?displayProperty=fullName>.  
  
<a name="BKMK_Determiningsortorder"></a>   
## <a name="determining-sort-order"></a>Determinar el criterio de ordenación  
 Los métodos como `BinarySearch` y `Sort` utilizan un comparador de orden para los elementos de la colección. Las comparaciones pueden ser entre elementos de la colección o entre un elemento y un valor especificado. Para comparar objetos, existe el concepto de un `default comparer` y un `explicit comparer`.  
  
 El comparador predeterminado se basa en al menos uno de los objetos que se comparan para implementar la interfaz **IComparable** . Una práctica recomendada es implementar **IComparable** en todas las clases que se utilizan como valores en una colección de lista o como claves en una colección de diccionarios. Para una colección genérica, la comparación de igualdad se determina según lo siguiente:  
  
-   Si el tipo T implementa la interfaz genérica de <xref:System.IComparable%601?displayProperty=fullName>, el comparador predeterminado es el método <xref:System.IComparable%601.CompareTo%28%600%29?displayProperty=fullName> de dicha interfaz.  
  
-   Si el tipo T implementa la interfaz no genérica de <xref:System.IComparable?displayProperty=fullName>, el comparador predeterminado es el método <xref:System.IComparable.CompareTo%28System.Object%29?displayProperty=fullName> de dicha interfaz.  
  
-   Si el tipo T no implementa ninguna de estas interfaces, no hay ningún comparador predeterminado y debe proporcionarse explícitamente un delegado de comparación o comparador.  
  
 Para proporcionar comparaciones explícitas, algunos métodos aceptan una implementación de **IComparer** como parámetro. Por ejemplo, el método <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName> acepta una implementación de <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName>.  
  
 La configuración de la referencia cultural actual del sistema puede afectar a las comparaciones y ordenaciones de una colección. De forma predeterminada, las comparaciones y ordenaciones de las clases **colecciones** tienen en cuenta la referencia cultural. Para ignorar la configuración de la referencia cultural y así obtener comparaciones y ordenaciones coherentes de los resultados, use el elemento <xref:System.Globalization.CultureInfo.InvariantCulture%2A> con sobrecargas de miembros que acepten una clase <xref:System.Globalization.CultureInfo>. Para obtener más información, vea [Realizar operaciones de cadenas que no tienen en cuenta las referencias culturales en colecciones](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-collections.md) y [Realizar operaciones de cadenas que no tienen en cuenta las referencias culturales en matrices](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations-in-arrays.md).  
  
<a name="BKMK_Equalityandsortexample"></a>   
## <a name="equality-and-sort-example"></a>Ejemplo de igualdad y ordenación  
 El código siguiente muestra una implementación de <xref:System.IEquatable%601> y <xref:System.IComparable%601> en un objeto comercial simple. Además, cuando el objeto se almacena en una lista y se ordena, la llamada al método <xref:System.Collections.Generic.List%601.Sort> implica el uso del comparador predeterminado para el tipo `Part` y el método <xref:System.Collections.Generic.List%601.Sort%28System.Comparison%7B%600%7D%29> implementado mediante el uso de un método anónimo.  
  
 [!code-csharp[System.Collections.Generic.List.Sort#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.collections.generic.list.sort/cs/program.cs#1)]
 [!code-vb[System.Collections.Generic.List.Sort#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.collections.generic.list.sort/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Collections.IComparer>   
 <xref:System.IEquatable%601>   
 <xref:System.Collections.Generic.IComparer%601>   
 <xref:System.IComparable>   
 <xref:System.IComparable%601>
