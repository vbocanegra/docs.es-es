---
title: Matrices en Visual Basic | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Array
dev_langs:
- VB
helpviewer_keywords:
- arrays [Visual Basic]
- Visual Basic, arrays
ms.assetid: dbf29737-b589-4443-bee6-a27588d9c67e
caps.latest.revision: 47
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: e0a5ab6a7b3ee752af6b58a35a11e4fc0fb2b08a
ms.openlocfilehash: cc7f5e28831cfe6ec12526d7dac5b12c208fb05a
ms.contentlocale: es-es
ms.lasthandoff: 07/03/2017

---
# <a name="arrays-in-visual-basic"></a>Matrices en Visual Basic
Una matriz es un conjunto de valores que están relacionados de forma lógica entre sí, como, por ejemplo, el número de alumnos de cada curso en una escuela primaria.  Si necesita ayuda sobre las matrices en Visual Basic para Aplicaciones (VBA), vea la [referencia del lenguaje](https://msdn.microsoft.com/library/office/gg264383\(v=office.14\).aspx).  
  
 Con las matrices, puede hacer referencia a estos valores relacionados con el mismo nombre y usar un número denominado índice o subíndice para distinguirlos. Los valores individuales se denominan elementos de la matriz. Son contiguos desde el índice 0 hasta el valor de índice más alto.  
  
 A diferencia de una matriz, una variable que contiene un solo valor se denomina variable *escalar* .  
  
 Veamos algunos ejemplos rápidos antes de la explicación:  
  
```vb  
'Declare a single-dimension array of 5 values  
Dim numbers(4) As Integer   
  
'Declare a single-dimension array and set array element values  
Dim numbers = New Integer() {1, 2, 4, 8}  
  
'Redefine the size of an existing array retaining the current values  
ReDim Preserve numbers(15)  
  
'Redefine the size of an existing array, resetting the values  
ReDim numbers(15)  
  
'Declare a multi-dimensional array  
Dim matrix(5, 5) As Double  
  
'Declare a multi-dimensional array and set array element values  
Dim matrix = New Integer(4, 4) {{1, 2}, {3, 4}, {5, 6}, {7, 8}}  
  
'Declare a jagged array  
Dim sales()() As Double = New Double(11)() {}  
```  
  
 **En este tema**  
  
-   [Elementos de una matriz en una matriz sencilla](#BKMK_ArrayElements)  
  
-   [Creación de una matriz](#BKMK_CreatingAnArray)  
  
-   [Almacenamiento de valores en una matriz](#BKMK_StoringValues)  
  
-   [Llenado de una matriz con valores iniciales](#BKMK_Populating)  
  
    -   [Literales de matriz anidados](#BKMK_NestedArrayLiterals)  
  
-   [Recorrer en iteración una matriz](#BKMK_Iterating)  
  
-   [Matrices como valores devueltos y parámetros](#BKMK_ReturnValues)  
  
-   [Matrices escalonadas](#BKMK_JaggedArrays)  
  
-   [Matrices de longitud cero](#BKMK_ZeroLength)  
  
-   [Tamaño de la matriz](#BKMK_ArraySize)  
  
-   [Tipos de matriz y otros tipos](#BKMK_ArrayTypes)  
  
-   [Colecciones como alternativa a las matrices](#BKMK_Collections)  
  
##  <a name="BKMK_ArrayElements"></a> Elementos de una matriz en una matriz sencilla  
 En el ejemplo siguiente se declara una variable de matriz para albergar el número de alumnos de cada curso en una escuela primaria.  
  
 [!code-vb[VbVbalrArrays#2](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#2)]  
  
 La matriz `students` del ejemplo anterior contiene siete elementos. Los índices de los elementos van del 0 al 6. Usar esta matriz es más fácil que declarar siete variables.  
  
 En la siguiente ilustración se muestra la matriz `students`. Para cada elemento de la matriz:  
  
-   El índice del elemento representa el curso (el índice 0 representa la guardería).  
  
-   El valor que se encuentra en el elemento representa el número de estudiantes en dicho curso.  
  
 ![Imagen de una matriz que muestra el número de estudiantes](../../../../visual-basic/programming-guide/language-features/arrays/media/arrayexampleschool.gif "ArrayExampleSchool")  
Elementos de la matriz "students"  
  
 El ejemplo siguiente muestra cómo hacer referencia al primero, segundo y último elemento de la matriz `students`.  
  
 [!code-vb[VbVbalrArrays#3](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#3)]  
  
 Puede hacer referencia a la matriz como un conjunto usando simplemente el nombre variable de la matriz sin índices.  
  
 La matriz `students` del ejemplo anterior usa un índice y es unidimensional. Una matriz que usa más de un índice o subíndice se denomina multidimensional. Para más información, vea el resto de este tema y [Array Dimensions in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md).  
  
##  <a name="BKMK_CreatingAnArray"></a> Creación de una matriz  
 El tamaño de una matriz se puede definir de varias maneras. Puede proporcionar el tamaño cuando se declara la matriz, como se muestra en el ejemplo siguiente.  
  
 [!code-vb[VbVbalrArrays#12](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#12)]  
  
 También puede usar una cláusula `New` para proporcionar el tamaño de la matriz cuando se crea, como se muestra en el ejemplo siguiente.  
  
 [!code-vb[VbVbalrArrays#11](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#11)]  
  
 Si tiene una matriz existente, puede volver a definir su tamaño mediante la instrucción `Redim` . Puede especificar que la instrucción `Redim` debe mantener los valores de la matriz o puede especificar que cree una matriz vacía. El ejemplo siguiente muestra los diferentes usos de la instrucción `Redim` para modificar el tamaño de una matriz existente.  
  
 [!code-vb[VbVbalrArrays#13](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#13)]  
  
 Para más información, vea [Instrucción ReDim](../../../../visual-basic/language-reference/statements/redim-statement.md).  
  
##  <a name="BKMK_StoringValues"></a> Almacenamiento de valores en una matriz  
 Puede tener acceso a cada ubicación en una matriz mediante un índice del tipo `Integer`. Puede almacenar y recuperar los valores en una matriz haciendo referencia a cada ubicación de la matriz usando su índice entre paréntesis. Los índices de matrices multidimensionales se separan mediante comas (,). Necesita un índice para cada dimensión de la matriz. El ejemplo siguiente muestra algunas instrucciones que almacenan valores en las matrices.  
  
 [!code-vb[VbVbalrArrays#5](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#5)]  
  
 El ejemplo siguiente muestra algunas instrucciones que obtienen valores de las matrices.  
  
 [!code-vb[VbVbalrArrays#6](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#6)]  
  
##  <a name="BKMK_Populating"></a> Llenado de una matriz con valores iniciales  
 Mediante el uso de un literal de matriz, puede crear una matriz que contiene un conjunto inicial de valores. Un literal de matriz consta de una lista de valores separados por comas entre llaves (`{}`).  
  
 Cuando se crea una matriz mediante un literal de matriz, puede proporcionar el tipo de matriz o usar la inferencia de tipo para determinar el tipo de matriz. El código siguiente muestra ambas opciones.  
  
 [!code-vb[VbVbalrCollectionInitializers#3](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#3)]  
  
 Cuando se usa la inferencia de tipos, el tipo de la matriz se determina por el tipo dominante en la lista de valores que se proporciona para el literal de matriz. El tipo dominante es un tipo único al que todos los demás tipos del literal de la matriz se pueden ampliar. Si no se puede determinar este tipo único, el tipo dominante es el tipo único al que todos los demás tipos de la matriz se pueden restringir. Si no se puede determinar ninguno de estos tipos únicos, el tipo dominante es `Object`. Por ejemplo, si la lista de valores que se proporciona al literal de matriz contiene valores de tipo `Integer`, `Long`y `Double`, la matriz resultante es de tipo `Double`. Tanto `Integer` como `Long` se amplían solo a `Double`. Por lo tanto, `Double` es el tipo dominante. Para obtener más información, consulta [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md). Estas reglas de inferencia se aplican a tipos que se deducen para matrices que son variables locales definidas en un miembro de clase. Aunque puede usar literales de matriz al crear variables de nivel de clase, no se puede usar la inferencia de tipos en el nivel de clase. Como resultado, los literales de matriz que se especifican en el nivel de clase deducen los valores proporcionados para el literal de matriz como tipo `Object`.  
  
 Puede especificar de manera explícita el tipo de los elementos de una matriz que se crea usando un literal de matriz. En este caso, los valores del literal de matriz se deben ampliar al tipo de los elementos de la matriz. En el ejemplo de código siguiente se crea una matriz de tipo `Double` desde una lista de enteros.  
  
 [!code-vb[VbVbalrCollectionInitializers#4](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#4)]  
  
###  <a name="BKMK_NestedArrayLiterals"></a> Literales de matriz anidados  
 Es posible crear una matriz multidimensional usando literales de matriz anidados. Los literales de matriz anidados deben tener una dimensión y un número de dimensiones o rango que sea coherente con la matriz resultante. En el ejemplo de código siguiente se crea una matriz bidimensional de enteros usando un literal de matriz.  
  
 [!code-vb[VbVbalrCollectionInitializers#7](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#7)]  
  
 En el ejemplo anterior, se produciría un error si el número de elementos en los literales de matriz anidados no coincidiese. También se producirá un error si se declarara de manera explícita que la variable de matriz no es bidimensional.  
  
> [!NOTE]
>  Para evitar que se produzca un error al proporcionar literales de matriz anidados de distintas dimensiones, incluya los literales de matriz internos entre paréntesis. Los paréntesis fuerzan la evaluación de la expresión de literal de matriz y los valores resultantes se usan con el literal de matriz exterior, tal como muestra el código siguiente.  
  
 [!code-vb[VbVbalrCollectionInitializers#11](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#11)]  
  
 Es posible usar la inferencia de tipos al crear una matriz multidimensional usando literales de matriz anidados. Cuando se usa la inferencia de tipos, el tipo inferido es el tipo dominante para todos los valores de todos los literales de matriz de un nivel de anidamiento. En el ejemplo de código siguiente se crea una matriz bidimensional del tipo `Double` a partir de valores del tipo `Integer` y `Double`.  
  
 [!code-vb[VbVbalrCollectionInitializers#8](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#8)]  
  
 Para consultar ejemplos adicionales, vea [Cómo: Inicializar una variable de matriz en Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md).  
  
##  <a name="BKMK_Iterating"></a> Recorrer en iteración una matriz  
 Cuando recorre en iteración una matriz, tiene acceso a todos los elementos de la matriz desde el índice más bajo hasta el más alto.  
  
 El ejemplo siguiente recorre en iteración una matriz unidimensional mediante el uso de la [Instrucción For...Next](../../../../visual-basic/language-reference/statements/for-next-statement.md). El método <xref:System.Array.GetUpperBound%2A> devuelve el valor más alto que puede tener el índice. El valor de índice mínimo es siempre 0.  
  
 [!code-vb[VbVbalrArrays#41](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#41)]  
  
 El ejemplo siguiente recorre en iteración una matriz multidimensional mediante el uso de una instrucción `For...Next` . El método <xref:System.Array.GetUpperBound%2A> tiene un parámetro que especifica la dimensión. `GetUpperBound(0)` devuelve el valor de índice más alto de la primera dimensión y `GetUpperBound(1)` devuelve el valor de índice más alto de la segunda dimensión.  
  
 [!code-vb[VbVbalrArrays#42](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#42)]  
  
 El ejemplo siguiente recorre en iteración una matriz unidimensional mediante el uso de la [Instrucción For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
 [!code-vb[VbVbalrArrays#43](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#43)]  
  
 El ejemplo siguiente recorre en iteración una matriz multidimensional mediante el uso de una instrucción `For Each...Next` . Sin embargo, tiene más control sobre los elementos de una matriz multidimensional si usa una instrucción `For…Next` anidada, como en un ejemplo anterior, en lugar de una instrucción `For Each…Next` .  
  
 [!code-vb[VbVbalrArrays#44](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#44)]  
  
##  <a name="BKMK_ReturnValues"></a> Matrices como valores devueltos y parámetros  
 Para devolver una matriz desde un procedimiento `Function`, especifique el tipo de datos de matriz y el número de dimensiones como tipo de valor devuelto de la [Instrucción Function](../../../../visual-basic/language-reference/statements/function-statement.md). Dentro de la función, declare una variable de matriz local con el mismo tipo de datos y número de dimensiones. En la [Instrucción Return](../../../../visual-basic/language-reference/statements/return-statement.md), incluya la variable de matriz local sin paréntesis.  
  
 Para especificar una matriz como parámetro para un procedimiento `Sub` o `Function` , defina el parámetro como una matriz con un tipo de datos especificado y el número de dimensiones. En la llamada al procedimiento, envíe una variable de matriz con el mismo tipo de datos y número de dimensiones.  
  
 En el ejemplo siguiente, la función `GetNumbers` devuelve `Integer()`. Este tipo de matriz es una matriz unidimensional de tipo `Integer`. El procedimiento `ShowNumbers` acepta un argumento `Integer()` .  
  
 [!code-vb[VbVbalrArrays#51](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#51)]  
  
 En el ejemplo siguiente, la función `GetNumbersMultiDim` devuelve un `Integer(,)`. Este tipo de matriz es una matriz bidimensional de tipo `Integer`.  El procedimiento `ShowNumbersMultiDim` acepta un argumento `Integer(,)` .  
  
 [!code-vb[VbVbalrArrays#52](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#52)]  
  
##  <a name="BKMK_JaggedArrays"></a> Matrices escalonadas  
 Una matriz que contiene otras matrices como elementos se conoce como matriz de matrices o matriz escalonada. Una matriz escalonada y cada elemento de una matriz escalonada pueden tener una o más dimensiones. A veces la estructura de datos de la aplicación es bidimensional pero no rectangular.  
  
 El ejemplo siguiente tiene una matriz de meses, siendo cada elemento una matriz de días. Puesto que los distintos meses tienen un número diferente de días, los elementos no forman una matriz bidimensional rectangular. Por lo tanto, se usa una matriz escalonada en lugar de una matriz multidimensional.  
  
 [!code-vb[VbVbalrArrays#21](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#21)]  
  
##  <a name="BKMK_ZeroLength"></a> Matrices de longitud cero  
 Una matriz que no contiene ningún elemento también se denomina matriz de longitud cero. Una variable que contiene una matriz de longitud cero no tiene el valor `Nothing`. Para crear una matriz que no tenga elementos, declare una de las dimensiones de la matriz para que sea -1, tal como se muestra en el ejemplo siguiente.  
  
 [!code-vb[VbVbalrArrays#14](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#14)]  
  
 Puede que tenga que crear una matriz de longitud cero en las circunstancias siguientes:  
  
-   Sin arriesgarse a una excepción <xref:System.NullReferenceException>, el código debe tener acceso a los miembros de la clase <xref:System.Array>, por ejemplo, <xref:System.Array.Length%2A> o <xref:System.Array.Rank%2A>, o bien deben llamar a una función [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], por ejemplo, <xref:Microsoft.VisualBasic.Information.UBound%2A>.  
  
-   Desea que el código usado sea más sencillo al no tener que comprobar `Nothing` como caso especial.  
  
-   El código interactúa con una interfaz de programación de aplicaciones (API) que requiere pasar una matriz de longitud cero a uno o más procedimientos o que devuelve una matriz de longitud cero desde uno o más procedimientos.  
  
##  <a name="BKMK_ArraySize"></a> Tamaño de la matriz  
 El tamaño de una matriz es el producto de las longitudes de todas sus dimensiones. Representa el número total de elementos contenidos actualmente en la matriz.  
  
 En el ejemplo siguiente se declara una matriz tridimensional.  
  
```  
Dim prices(3, 4, 5) As Long  
```  
  
 El tamaño total de la matriz en la variable `prices` es (3 + 1) x (4 + 1) x (5 + 1) = 120.  
  
 Puede encontrar el tamaño de una matriz mediante la propiedad <xref:System.Array.Length%2A>. Puede averiguar la longitud de cada dimensión de una matriz multidimensional utilizando el método <xref:System.Array.GetLength%2A>.  
  
 Puede cambiar el tamaño de una variable de matriz asignando un nuevo objeto de matriz o usando la instrucción `ReDim` .  
  
 Hay varios aspectos que se deben tener en cuenta cuando se trabaja con el tamaño de una matriz.  
  
|||  
|---|---|  
|Longitud de la dimensión|El índice de cada dimensión es de base 0, lo que significa que va desde 0 hasta su límite máximo. Por lo tanto, la longitud de una dimensión determinada supera en 1 el límite máximo declarado para esa dimensión.|  
|Límites de longitud|La longitud de cada dimensión de una matriz se limita al valor máximo del tipo de datos `Integer`, que es (2 ^ 31) - 1. Sin embargo, el tamaño total de una matriz también está limitado por la memoria disponible en el sistema. Si se intenta inicializar una matriz que supera la cantidad de memoria RAM disponible, Common Language Runtime produce una excepción <xref:System.OutOfMemoryException>.|  
|Tamaño y tamaño de elemento|El tamaño de la matriz es independiente del tipo de datos de sus elementos. El tamaño siempre representa el número total de elementos, no el número de bytes que se usan en el almacenamiento.|  
|Consumo de memoria|No es seguro dar nada por supuesto en lo que respecta al modo de almacenar una matriz en la memoria. El almacenamiento varía en función de las plataformas de diferentes anchos de datos, por lo que la misma matriz puede utilizar más memoria en un sistema de 64 bits que en un sistema de 32 bits. Según la configuración del sistema cuando inicializa una matriz, Common Language Runtime (CLR) puede asignar el almacenamiento para empaquetar los elementos tan juntos como sea posible o para alinearlos todos en los límites naturales del hardware. Asimismo, una matriz requiere una sobrecarga de almacenamiento para obtener su información de control y esta sobrecarga aumenta con cada dimensión agregada.|  
  
##  <a name="BKMK_ArrayTypes"></a> Tipos de matriz y otros tipos  
 Cada matriz tiene un tipo de datos, pero difiere del tipo de datos de sus elementos. No existe ningún tipo de datos para todas las matrices. En su lugar, el tipo de datos de una matriz lo determina el número de dimensiones, o *rango*, de la matriz y el tipo de datos de los elementos de la matriz. Se considera que dos variables de matriz son del mismo tipo de datos solo cuando tienen el mismo rango y sus elementos tienen el mismo tipo de datos. Las longitudes de las dimensiones de una matriz no influyen en el tipo de datos de la matriz.  
  
 Cada matriz hereda la clase <xref:System.Array?displayProperty=fullName> y puede declarar una variable del tipo `Array`, pero no puede crear una matriz del tipo `Array`. Además, la [Instrucción ReDim](../../../../visual-basic/language-reference/statements/redim-statement.md) no puede funcionar en una variable declarada de tipo `Array`. Por estas razones y para mayor seguridad del tipo, es aconsejable declarar cada matriz como un tipo específico, como `Integer` en el ejemplo anterior.  
  
 Puede averiguar el tipo de datos de una matriz o de sus elementos de varias maneras.  
  
-   Puede llamar al método <xref:System.Object.GetType%2A?displayProperty=fullName> en la variable para recibir un objeto <xref:System.Type> para el tipo en tiempo de ejecución de la variable. El objeto <xref:System.Type> contiene amplia información en sus propiedades y métodos.  
  
-   Puede pasar la variable a la función <xref:Microsoft.VisualBasic.Information.TypeName%2A> para recibir un `String` que contiene el nombre de tipo en tiempo de ejecución.  
  
-   Puede pasar la variable a la función <xref:Microsoft.VisualBasic.Information.VarType%2A> para recibir un valor `VariantType` que representa la clasificación del tipo de la variable.  
  
 En el ejemplo siguiente se llama a la función `TypeName` para determinar el tipo de la matriz y el tipo de elementos de la matriz. El tipo de matriz es `Integer(,)` y los elementos de la matriz son del tipo `Integer`.  
  
 [!code-vb[VbVbalrArrays#15](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#15)]  
  
##  <a name="BKMK_Collections"></a> Colecciones como alternativa a las matrices  
 Las matrices son muy útiles para crear y trabajar con un número fijo de objetos fuertemente tipados. Las colecciones proporcionan una manera más flexible de trabajar con grupos de objetos. A diferencia de las matrices, el grupo de objetos con el que trabaja puede aumentar y reducirse de manera dinámica a medida que cambian las necesidades de la aplicación.  
  
 Si necesita cambiar el tamaño de una matriz, debe usar la [Instrucción ReDim](../../../../visual-basic/language-reference/statements/redim-statement.md). Al hacerlo, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] crea una nueva matriz y libera la matriz anterior para su eliminación. Esto requiere tiempo de ejecución. Por lo tanto, si el número de elementos con los que trabaja cambia con frecuencia o si no puede predecir el número máximo de elementos que necesita, puede obtener un mejor rendimiento si usa una colección.  
  
 Para algunas colecciones, puede asignar una clave a cualquier objeto que incluya en la colección para, de este modo, recuperar rápidamente el objeto con la clave.  
  
 Si la colección contiene elementos de un solo tipo de datos, puede usar una de las clases del espacio de nombres <xref:System.Collections.Generic?displayProperty=fullName>. Una colección genérica cumple la seguridad de tipos para que ningún otro tipo de datos se pueda agregar a ella. Cuando recupera un elemento de una colección genérica, no tiene que determinar su tipo de datos ni convertirlo.  
  
 Para más información sobre las colecciones, vea [Colecciones](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b).  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la clase genérica [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]<xref:System.Collections.Generic.List%601?displayProperty=fullName> para crear una colección de listas de objetos `Customer`.  
  
 [!code-vb[VbVbalrArrays#1](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrArrays/VB/Class1.vb#1)]  
  
 La declaración de la colección `CustomerFile` especifica que solo puede contener elementos del tipo `Customer`. También proporciona una capacidad inicial de 200 elementos. El procedimiento `AddNewCustomer` comprueba la validez del nuevo elemento y, a continuación, lo agrega a la colección. El procedimiento `PrintCustomers` usa un bucle `For Each` para recorrer la colección y mostrar sus elementos.  
  
## <a name="related-topics"></a>Temas relacionados  
  
|Término|Definición|  
|----------|----------------|  
|[Array Dimensions in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md)|Explica el rango y las dimensiones de las matrices.|  
|[Cómo: Inicializar una variable de matriz en Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)|Describe cómo se llenan las matrices con valores iniciales.|  
|[Cómo: Ordenar una matriz en Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-sort-an-array.md)|Muestra cómo ordenar alfabéticamente los elementos de una matriz.|  
|[Asignar una matriz a otra](../../../../visual-basic/programming-guide/language-features/arrays/how-to-assign-one-array-to-another-array.md)|Describe las reglas y los pasos para asignar una matriz a otra variable de matriz.|  
|[Solución de problemas de matrices](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)|Describe algunos problemas comunes que surgen al trabajar con matrices.|  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Array>   
 [Instrucción Dim](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim (instrucción)](../../../../visual-basic/language-reference/statements/redim-statement.md)

