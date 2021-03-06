---
title: "C&#243;mo: Eliminar filas de la base de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2144c99b-8055-4080-a5c6-1ea14335e2a3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# C&#243;mo: Eliminar filas de la base de datos
Puede eliminar filas de una base de datos quitando los objetos de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] correspondientes de la colección relacionada con la tabla. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] convierte los cambios en los comandos SQL `DELETE` correspondientes.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] no admite ni reconoce las operaciones de eliminación en cascada.  Si desea eliminar una fila de una tabla que tiene restricciones, deberá realizar una de las siguientes tareas:  
  
-   Establezca la regla `ON DELETE CASCADE` en la restricción de clave externa de la base de datos.  
  
-   Utilice su propio código para eliminar primero los objetos secundarios que impiden que se elimine el objeto primario.  
  
 De lo contrario, se inicia una excepción.  Vea el segundo ejemplo de código que se muestra más adelante en este tema.  
  
> [!NOTE]
>  Puede invalidar los métodos predeterminados de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para las operaciones de base de datos `Insert`, `Update` y `Delete`.  Para obtener más información, consulte [Personalizar operaciones de actualización, inserción y eliminación](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
>   
>  Los desarrolladores de [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] pueden usar el [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] para desarrollar procedimientos almacenados con el mismo propósito.  
  
 En los pasos siguientes se asume que un objeto <xref:System.Data.Linq.DataContext> válido le conecta a la base de datos Northwind.  Para obtener más información, consulte [Cómo: Conectarse a una base de datos](../../../../../../docs/framework/data/adonet/sql/linq/how-to-connect-to-a-database.md).  
  
### Para eliminar una fila en la base de datos  
  
1.  Consulte en la base de datos la fila que se va a eliminar.  
  
2.  Llame al método <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>.  
  
3.  Envíe el cambio a la base de datos.  
  
## Ejemplo  
 En este primer ejemplo de código se consultan en la base de datos los detalles del pedido \#11000, se marcan dichos detalles para eliminarlos y se envían estos cambios a la base de datos.  
  
 [!code-csharp[System.Data.Linq.Table#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#3)]
 [!code-vb[System.Data.Linq.Table#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#3)]  
  
## Ejemplo  
 En este segundo ejemplo, el objetivo es quitar un pedido \(\#10250\).  En primer lugar, el código examina la tabla `OrderDetails` para comprobar si el pedido que se va a quitar tiene elementos secundarios en ésta.  Si el pedido tiene elementos secundarios, se marcan primero los elementos secundarios y después el pedido para eliminarlos.  El objeto <xref:System.Data.Linq.DataContext> coloca las eliminaciones en el orden correcto para que los comandos de eliminación enviados a la base de datos cumplan las restricciones de la misma.  
  
 [!code-csharp[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCascadeWorkaround/cs/Program.cs#1)]
 [!code-vb[DLinqCascadeWorkaround#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCascadeWorkaround/vb/Module1.vb#1)]  
  
## Vea también  
 [Cómo: Administrar los conflictos de cambios](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)   
 [Cómo: Asignar procedimientos almacenados para realizar actualizaciones, inserciones y eliminaciones \(Object Relational Designer\)](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [Crear y enviar cambios en los datos](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)