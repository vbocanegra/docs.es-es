---
title: "Funciones matem&#225;ticas | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: b040c7cb-156d-40f2-9152-61065b18148c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funciones matem&#225;ticas
El Proveedor de datos .NET Framework para SQL Server \(SqlClient\) proporciona funciones matemáticas que realizan cálculos con los valores de entrada que se proporcionan como argumentos y devuelven un resultado numérico.  Estas funciones están en el espacio de nombres SqlServer, que está disponible al utilizar SqlClient.  La propiedad del espacio de nombres de un proveedor permite a Entity Framework detectar qué prefijo usa este proveedor para estructuras concretas, como los tipos y las funciones. La tabla siguiente describe las funciones matemáticas de SqlClient.  
  
|Función|Descripción|  
|-------------|-----------------|  
|`ABS(` `expression` `)`|Lleva a cabo la función que devuelve el valor absoluto.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo`Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valor devuelto**<br /><br /> Valor absoluto de la expresión especificada.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ABS(-2)`|  
|`ACOS(` `expression` `)`|Devuelve el valor del arcocoseno de la expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ACOS(.9)`|  
|`ASIN(` `expression` `)`|Devuelve el valor del arcoseno de la expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ASIN(.9)`|  
|`ATAN(` `expression` `)`|Devuelve el valor del arcotangente de la expresión numérica especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ATAN(9)`|  
|`ATN2(` `expression`, `expression``)`|Devuelve el ángulo, en radianes, cuya tangente se encuentra entre las dos expresiones numéricas especificadas.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ATN2(9, 8)`|  
|`CEILING(` `expression` `)`|Convierte la expresión especificada al número entero más pequeño mayor o igual que él.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo`Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Ejemplo**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_ceiling)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_ceiling)]|  
|`COS(` `expression` `)`|Calcula el coseno trigonométrico del ángulo especificado, en radianes.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.COS(45)`|  
|`COT(` `expression` `)`|Calcula la cotangente trigonométrica del ángulo especificado, en radianes.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.COT(60)`|  
|`DEGREES(` `radians` `)`|Devuelve el ángulo correspondiente en grados.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo`Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.DEGREES(3.1)`|  
|`EXP(` `expression` `)`|Calcula el valor exponencial de la expresión numérica especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.EXP(1)`|  
|`FLOOR(` `expression` `)`|Convierte la expresión especificada al número entero más grande que sea menor o igual que ella.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_floor)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_floor)]|  
|`LOG(` `expression` `)`|Calcula el logaritmo natural de la expresión `float` especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.LOG(100)`|  
|`LOG10(` `expression` `)`|Devuelve el logaritmo en base 10 de la expresión `Double` especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.LOG10(100)`|  
|`PI()`|Devuelve el valor constante de Pi como un `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.PI()`|  
|`POWER(` `numeric_expression, power_expression` `)`|Calcula el valor de la expresión especificada elevada a la potencia indicada.<br /><br /> **Argumentos**<br /><br /> `numeric_expression`: valor de tipo `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> `power_expression`: valor de tipo `Double` que representa la potencia a la que se va a elevar `numeric_expression`.<br /><br /> **Valor devuelto**<br /><br /> Valor de la `numeric_expression` especificada a la `power_expression` especificada.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.POWER(2,7)`|  
|`RADIANS(` `expression` `)`|Convierte grados en radianes.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo`Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `Int32`, `Int64`<br /><br /> `Double` o<br /><br /> `Decimal`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.RADIANS(360.0)`|  
|`RAND(`\[inicialización\]`)`|Devuelve un valor aleatorio de 0 a 1.<br /><br /> **Argumentos**<br /><br /> Retruns el valor de inicialización como `Int32`.  Si la inicialización no se especifica, el motor de base de datos de SQL Server asigna uno de forma aleatoria.  Para un valor de inicialización especificado, el resultado devuelto es siempre el mismo.<br /><br /> **Valor devuelto**<br /><br /> Valor `Double` aleatorio de 0 a 1.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.RAND()`|  
|`ROUND(` `numeric_expression, length` \[ ,`function` \]`)`|Devuelve una expresión numérica, redondeada a la longitud o precisión especificadas.<br /><br /> **Argumentos**<br /><br /> `numeric_expression`: valor de tipo `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> `length`: Valor de tipo `Int32` que representa la precisión a la que se va a redondear `numeric_expression`.  Si `length` es un número positivo, `numeric_expression` se redondea al número de posiciones decimales que especifica `length`.  Si `length` es un número negativo, `numeric_expression` se redondea a la izquierda del separador decimal, según se especifica en `length`.<br /><br /> `function`: ``  \(opcional\) Valor `Int32` que representa el tipo de operación que se va a realizar.  Si la función se omite o tiene el valor 0 \(predeterminado\), `numeric_expression` se redondea.  Si se especifica un valor distinto de 0, `numeric_expression` se trunca.<br /><br /> **Valor devuelto**<br /><br /> Valor de la `numeric_expression` especificada a la `power_expression` especificada.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.ROUND(748.58, -3)`|  
|`SIGN(` `expression` `)`|Devuelve el signo positivo \(\+1\), cero \(0\) o negativo \(\-1\) de la expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Int32`, `Int64`, `Double` o `Decimal`<br /><br /> **Valor devuelto**<br /><br /> Valor de tipo `Int32`, `Int64`, `Double` o `Decimal`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.SIGN(-10)`|  
|`SIN(` `expression` `)`|Calcula el seno trigonométrico de un ángulo especificado, en radianes, y devuelve una expresión de tipo `Double`.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.SIN(20)`|  
|`SQRT(` `expression` `)`|Devuelve la raíz cuadrada de la expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.SQRT(3600)`|  
|`SQUARE(` `expression` `)`|Devuelve la raíz cuadrada de la expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: valor de tipo `Double`.<br /><br /> **Valor devuelto**<br /><br /> Un objeto `Double`.<br /><br /> **Ejemplo**<br /><br /> `SqlServer.SQUARE(25)`|  
|`TAN(` `expression` `)`|Calcula la tangente de una expresión especificada.<br /><br /> **Argumentos**<br /><br /> `expression`: `Double`<br /><br /> **Valor devuelto**<br /><br /> `Double`<br /><br /> **Ejemplo**<br /><br /> `SqlServer.TAN(45.0)`|  
  
 Para obtener más información sobre las funciones matemáticas que SqlClient admite, consulte la documentación de la versión de SQL Server que especificó en el manifiesto del proveedor SqlClient:  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[Funciones matemáticas \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115913)|[Funciones matemáticas \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115911)|[Funciones matemáticas \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115912)|  
  
## Vea también  
 [SqlClient para las funciones de Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)