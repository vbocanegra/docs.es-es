---
title: "Cómo: devolver el resultado de una consulta LINQ como tipo específico (Visual Basic) | Documentos de Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], specific type returned
- projection [LINQ in Visual Basic]
- anonymous types [Visual Basic]
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 621bb10a-e5d7-44fb-a025-317964b19d92
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2031e24ca0fe5aa86ca6c0bcd0e0e4f27238c8ae
ms.contentlocale: es-es
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-a-linq-query-result-as-a-specific-type-visual-basic"></a>Cómo: Devolver el resultado de una consulta con LINQ como tipo específico (Visual Basic)
Language-Integrated Query (LINQ) facilita el acceso a la información de la base de datos y ejecutar consultas. De forma predeterminada, las consultas LINQ devuelven una lista de objetos como un tipo anónimo. También puede especificar que una consulta devuelve una lista de un tipo específico mediante el uso de la `Select` cláusula.  
  
 En el ejemplo siguiente se muestra cómo crear una nueva aplicación que realiza consultas en una base de datos de SQL Server y proyecta los resultados como un tipo con nombre específico. Para obtener más información, consulte [tipos anónimos](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) y [cláusula Select](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
 Los ejemplos de este tema utilizan la base de datos de ejemplo Northwind. Si no tiene la base de datos de ejemplo Northwind en el equipo de desarrollo, puede descargarla desde el [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) sitio Web. Para obtener instrucciones, consulte [descargar bases de datos de ejemplo](https://msdn.microsoft.com/library/bb399411).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>Para crear una conexión a una base de datos  
  
1.  En Visual Studio, abra **Explorador de servidores**/**Database Explorer** haciendo clic en **Explorador de servidores**/**Database Explorer** en el **vista** menú.  
  
2.  Haga clic en **las conexiones de datos** en **Explorador de servidores**/**Database Explorer** y, a continuación, haga clic en **Agregar conexión**.  
  
3.  Especifique una conexión válida a la base de datos de ejemplo Northwind.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>Para agregar un proyecto que contiene un archivo de LINQ to SQL  
  
1.  En Visual Studio, en el **archivo** menú, seleccione **nueva** y, a continuación, haga clic en **proyecto**. Seleccione Visual Basic **aplicación de Windows Forms** como el tipo de proyecto.  
  
2.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**. Seleccione el **clases LINQ to SQL** plantilla de elemento.  
  
3.  Nombre de archivo `northwind.dbml`. Haga clic en **Agregar**. Se abre el Object Relational Designer (Object Relational Designer) para el archivo northwind.dbml.  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>Para agregar tablas a la consulta para el Object Relational Designer  
  
1.  En **Explorador de servidores**/**Database Explorer**, expanda la conexión de la base de datos Northwind. Expanda el **tablas** carpeta.  
  
     Si ha cerrado el Object Relational Designer, puede volver a abrirlo haciendo doble clic en el archivo northwind.dbml que agregó anteriormente.  
  
2.  Haga clic en la tabla Customers y arrástrela hasta el panel izquierdo del diseñador.  
  
     El diseñador crea un nuevo `Customer` objeto para su proyecto. Se puede proyectar el resultado de una consulta como la `Customer` tipo o como un tipo que cree. En este ejemplo se crea un nuevo tipo en un procedimiento posterior y el resultado de una consulta como ese tipo de proyecto.  
  
3.  Guarde los cambios y cierre el diseñador.  
  
4.  Guarde el proyecto.  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>Para agregar código para consultar la base de datos y mostrar los resultados  
  
1.  Desde el **herramientas**, arrastre un <xref:System.Windows.Forms.DataGridView>control en el formulario Windows Forms predeterminado del proyecto, Form1.</xref:System.Windows.Forms.DataGridView>  
  
2.  Haga doble clic en Form1 para modificar la clase Form1.  
  
3.  Después de la `End Class` instrucción de la clase Form1, agregue el código siguiente para crear un `CustomerInfo` tipo para contener los resultados de la consulta de este ejemplo.  
  
     [!code-vb[VbLINQToSQLHowTos Nº&16;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_1.vb)]  
  
4.  Cuando agrega tablas a Object Relational Designer, el diseñador agrega un <xref:System.Data.Linq.DataContext>objeto a su proyecto.</xref:System.Data.Linq.DataContext> Este objeto contiene el código que debe tener acceso a esas tablas y tener acceso a objetos individuales y colecciones de cada tabla. La <xref:System.Data.Linq.DataContext>objeto para su proyecto se denomina según el nombre del archivo .dbml.</xref:System.Data.Linq.DataContext> Para este proyecto, el <xref:System.Data.Linq.DataContext>se denomina objeto `northwindDataContext`.</xref:System.Data.Linq.DataContext>  
  
     Puede crear una instancia de la <xref:System.Data.Linq.DataContext>en el código y consultar las tablas especifican por el Object Relational Designer.</xref:System.Data.Linq.DataContext>  
  
     En el `Load` eventos de la clase Form1, agregue el código siguiente para consultar las tablas que se exponen como propiedades del contexto de datos. El `Select` creará una nueva cláusula de la consulta `CustomerInfo` tipo en lugar de un tipo anónimo para cada elemento del resultado de la consulta.  
  
     [!code-vb[VbLINQToSQLHowTos&#15;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_2.vb)]  
  
5.  Presione F5 para ejecutar el proyecto y ver los resultados.  
  
## <a name="see-also"></a>Vea también  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Consultas](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [Métodos de DataContext (Object Relational Designer)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)

