# [Programación en paralelo](index.md)
## [Biblioteca TPL](task-parallel-library-tpl.md)
### [Data Parallelism](data-parallelism-task-parallel-library.md) (Paralelismo de datos)
#### [How to: Write a Simple Parallel.For Loop](how-to-write-a-simple-parallel-for-loop.md) (Cómo: Escribir un bucle Parallel.For simple)
#### [How to: Write a Simple Parallel.ForEach Loop](how-to-write-a-simple-parallel-foreach-loop.md) (Cómo: Escribir un bucle Parallel.ForEach simple)
#### [How to: Write a Parallel.For Loop with Thread-Local Variables](how-to-write-a-parallel-for-loop-with-thread-local-variables.md) (Cómo: Escribir un bucle Parallel.For con variables locales de subproceso)
#### [How to: Write a Parallel.ForEach Loop with Thread-Local Variables](how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md) (Cómo: Escribir un bucle Parallel.ForEach con variables locales de subproceso)
#### [How to: Cancel a Parallel.For or ForEach Loop](how-to-cancel-a-parallel-for-or-foreach-loop.md) (Cómo: Cancelar un bucle Parallel.For o ForEach)
#### [Controlar excepciones en bucles paralelos](how-to-handle-exceptions-in-parallel-loops.md)
#### [How to: Speed Up Small Loop Bodies](how-to-speed-up-small-loop-bodies.md) (Cómo: Acelerar cuerpos de bucle pequeños)
#### [Recorrer en iteración directorios con la clase paralela](how-to-iterate-file-directories-with-the-parallel-class.md)
### [Programación asincrónica basada en tareas](task-based-asynchronous-programming.md)
#### [Chaining Tasks by Using Continuation Tasks](chaining-tasks-by-using-continuation-tasks.md) (Encadenar tareas mediante tareas de continuación)
#### [Attached and Detached Child Tasks](attached-and-detached-child-tasks.md) (Tareas secundarias asociadas y desasociadas)
#### [Task Cancellation](task-cancellation.md) (Cancelación de tareas)
#### [Control de excepciones](exception-handling-task-parallel-library.md)
#### [How to: Use Parallel.Invoke to Execute Parallel Operations](how-to-use-parallel-invoke-to-execute-parallel-operations.md) (Usar Parallel.Invoke para ejecutar operaciones en paralelo)
#### [How to: Return a Value from a Task](how-to-return-a-value-from-a-task.md) (Devolver un valor a partir de una tarea)
#### [How to: Cancel a Task and Its Children](how-to-cancel-a-task-and-its-children.md) (Cancelar una tarea y los elementos secundarios)
#### [How to: Create Pre-Computed Tasks](how-to-create-pre-computed-tasks.md) (Crear tareas precalculadas)
#### [How to: Traverse a Binary Tree with Parallel Tasks](how-to-traverse-a-binary-tree-with-parallel-tasks.md) (Recorrer un árbol binario con tareas en paralelo)
#### [How to: Unwrap a Nested Task](how-to-unwrap-a-nested-task.md) (Desencapsular una tarea anidada)
#### [Impedir que una tarea secundaria se adjunte a su elemento primario](how-to-prevent-a-child-task-from-attaching-to-its-parent.md)
### [Flujo de datos](dataflow-task-parallel-library.md)
#### [How to: Write Messages to and Read Messages from a Dataflow Block](how-to-write-messages-to-and-read-messages-from-a-dataflow-block.md) (Cómo: Leer y escribir mensajes en un bloque de flujo de datos)
#### [How to: Implement a Producer-Consumer Dataflow Pattern](how-to-implement-a-producer-consumer-dataflow-pattern.md) (Cómo: Implementar un modelo de flujo de datos productor-consumidor)
#### [How to: Perform Action When a Dataflow Block Receives Data](how-to-perform-action-when-a-dataflow-block-receives-data.md) (Cómo: Realizar una acción cuando un bloque de flujo de datos recibe datos)
#### [Walkthrough: Creating a Dataflow Pipeline](walkthrough-creating-a-dataflow-pipeline.md) (Tutorial: Creación de una canalización de flujo de datos)
#### [How to: Unlink Dataflow Blocks](how-to-unlink-dataflow-blocks.md) (Cómo: Desvincular bloques de flujo de datos)
#### [Walkthrough: Using Dataflow in a Windows Forms Application](walkthrough-using-dataflow-in-a-windows-forms-application.md) (Tutorial: Uso de flujos de datos en aplicaciones de Windows Forms)
#### [How to: Cancel a Dataflow Block](how-to-cancel-a-dataflow-block.md) (Cómo: Cancelar un bloque de flujo de datos)
#### [Walkthrough: Creating a Custom Dataflow Block Type](walkthrough-creating-a-custom-dataflow-block-type.md) (Tutorial: Creación de un tipo de bloque de flujo de datos personalizado)
#### [How to: Use JoinBlock to Read Data From Multiple Sources](how-to-use-joinblock-to-read-data-from-multiple-sources.md) (Cómo: Utilizar JoinBlock para leer datos de varios orígenes)
#### [How to: Specify the Degree of Parallelism in a Dataflow Block](how-to-specify-the-degree-of-parallelism-in-a-dataflow-block.md) (Cómo: Especificar el grado de paralelismo en un bloque de flujo de datos)
#### [How to: Specify a Task Scheduler in a Dataflow Block](how-to-specify-a-task-scheduler-in-a-dataflow-block.md) (Cómo: Especificar un programador de tareas en un bloque de flujo de datos)
#### [Walkthrough: Using BatchBlock and BatchedJoinBlock to Improve Efficiency](walkthrough-using-batchblock-and-batchedjoinblock-to-improve-efficiency.md) (Tutorial: Uso de BatchBlock y BatchedJoinBlock para mejorar la eficacia)
### [Usar TPL con otros patrones asincrónicos](using-tpl-with-other-asynchronous-patterns.md)
#### [TPL y la programación asincrónica tradicional de .NET Framework](tpl-and-traditional-async-programming.md)
#### [Encapsular modelos de EAP en una tarea](how-to-wrap-eap-patterns-in-a-task.md)
### [Problemas potenciales en el paralelismo de datos y tareas](potential-pitfalls-in-data-and-task-parallelism.md)
## [Parallel LINQ (PLINQ)](parallel-linq-plinq.md)
### [Introducción a PLINQ](introduction-to-plinq.md)
### [Introducción a la velocidad en PLINQ](understanding-speedup-in-plinq.md)
### [Conversación del orden en PLINQ](order-preservation-in-plinq.md)
### [Opciones de combinación en PLINQ](merge-options-in-plinq.md)
### [Posibles problemas con PLINQ](potential-pitfalls-with-plinq.md)
### [Creación y ejecución de una consulta PLINQ simple](how-to-create-and-execute-a-simple-plinq-query.md)
### [Control de la ordenación en una consulta PLINQ](how-to-control-ordering-in-a-plinq-query.md)
### [Combinación de consultas LINQ en paralelo y secuenciales](how-to-combine-parallel-and-sequential-linq-queries.md)
### [Control de excepciones en una consulta PLINQ](how-to-handle-exceptions-in-a-plinq-query.md)
### [Cancelación de una consulta PLINQ](how-to-cancel-a-plinq-query.md)
### [Escritura de una función de agregado personalizada de PLINQ](how-to-write-a-custom-plinq-aggregate-function.md)
### [Especificación del modo de ejecución en PLINQ](how-to-specify-the-execution-mode-in-plinq.md)
### [Especificación de opciones de combinación en PLINQ](how-to-specify-merge-options-in-plinq.md)
### [Iteración de directorios de archivos con PLINQ](how-to-iterate-file-directories-with-plinq.md)
### [Medición del rendimiento de consultas PLINQ](how-to-measure-plinq-query-performance.md)
### [Ejemplo de datos de PLINQ](plinq-data-sample.md)
## [Estructuras de datos para la programación paralela](data-structures-for-parallel-programming.md)
## [Herramientas de diagnóstico paralelo](parallel-diagnostic-tools.md)
## [Particionadores personalizados para PLINQ y TPL](custom-partitioners-for-plinq-and-tpl.md)
### [Implementar las particiones dinámicas](how-to-implement-dynamic-partitions.md)
### [Implementar un particionador para particionamiento estático](how-to-implement-a-partitioner-for-static-partitioning.md)
## [Lambda Expressions in PLINQ and TPL](lambda-expressions-in-plinq-and-tpl.md) (Expresiones lambda en PLINQ y TPL)
## [Información adicional](for-further-reading-parallel-programming.md)