---
title: "How to: Write a Parallel.ForEach Loop with Thread-Local Variables | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parallel foreach loop, how to use local state"
ms.assetid: 24b10041-b30b-45cb-aa65-66cf568ca76d
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# How to: Write a Parallel.ForEach Loop with Thread-Local Variables
En el siguiente ejemplo se muestra cómo escribir un método <xref:System.Threading.Tasks.Parallel.ForEach%2A> que utiliza variables locales de subproceso.  Cuando un bucle <xref:System.Threading.Tasks.Parallel.ForEach%2A> se ejecuta, divide su colección de origen en varias particiones.  Cada partición obtendrá su propia copia de la variable "local de subproceso".  \(El término "local de subproceso" es ligeramente inexacto, porque en algunos casos dos particiones se pueden ejecutar en el mismo subproceso\).  
  
 El código y los parámetros de este ejemplo se parecen mucho al método <xref:System.Threading.Tasks.Parallel.For%2A> correspondiente.  Para obtener más información, vea [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md).  
  
 Para utilizar una variable local de subproceso en un bucle <xref:System.Threading.Tasks.Parallel.ForEach%2A>, realice una llamada a una de las sobrecargas del método que toma dos parámetros de tipo.  El primer parámetro de tipo, `TSource`, especifica el tipo del elemento de origen, mientras que el segundo parámetro de tipo, `TLocal`, especifica el tipo de la variable local de subproceso.  
  
## Ejemplo  
 En el ejemplo siguiente se realiza una llamada a la sobrecarga <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=fullName> para calcular la suma de una matriz de un millón de elementos.  Esta sobrecarga gráfico tiene cuatro parámetros:  
  
-   `source`, que es el origen de datos.  Debe implementar <xref:System.Collections.Generic.IEnumerable%601>.  El origen de datos de este ejemplo es un objeto `IEnumerable<Int32>` de un millón de miembros que ha sido devuelto por el método <xref:System.Linq.Enumerable.Range%2A?displayProperty=fullName>.  
  
-   `localInit`, o la función que inicializa la variable local de subproceso.  Esta función se llama una vez por cada partición en la que se ejecuta la operación <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName>.  En el ejemplo se inicializa la variable local de subproceso en cero.  
  
-   `body`, un <xref:System.Func%604> al que invoca el bucle paralelo en cada iteración del mismo bucle.  Su firma es `Func\<TSource, ParallelLoopState, TLocal, TLocal>`.  Se proporciona el código para el delegado y el bucle pasa los parámetros de entrada, que son:  
  
    -   El elemento actual de <xref:System.Collections.Generic.IEnumerable%601>.  
  
    -   Una variable <xref:System.Threading.Tasks.ParallelLoopState> que se puede usar en el código del delegado a fin de examinar el estado del bucle.  
  
    -   La variable local de subproceso.  
  
     El delegado devuelve la variable local de subproceso, y esta se pasa luego a la siguiente iteración del bucle que se ejecuta en esa partición concreta.  Cada una de las particiones del bucle mantiene una instancia independiente de esta variable.  
  
     En el ejemplo, el delegado agrega el valor de cada entero a la variable local de subproceso, que mantiene un total acumulativo de los valores de los elementos enteros de esa partición.  
  
-   `localFinally`, un delegado `Action<TLocal>` al que invoca <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> cuando se han completado las operaciones de bucle en las particiones.  El método <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> pasa al delegado `Action<TLocal>` el valor final de la variable local de subproceso correspondiente a este subproceso \(o partición del bucle\), y usted proporciona el código que realiza la acción necesaria para combinar el resultado de esta partición con los resultados de las otras particiones.  Varias tareas pueden invocar simultáneamente a este delegado.  Debido a esto, en el ejemplo se usa el método <xref:System.Threading.Interlocked.Add%28System.Int32%40%2CSystem.Int32%29?displayProperty=fullName> se utiliza para sincronizar el acceso a la variable `total`.  Como el tipo de delegado es <xref:System.Action%601>, no hay valor devuelto.  
  
 [!code-csharp[TPL_Parallel#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/foreachthreadlocal.cs#04)]
 [!code-vb[TPL_Parallel#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/foreachthreadlocal.vb#04)]  
  
## Vea también  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)