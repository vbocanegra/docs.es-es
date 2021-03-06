---
title: nameof (Referencia de C# y Visual Basic) | Microsoft Docs
ms.date: 2017-03-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- nameof_CSharpKeyword
- nameof
dev_langs:
- CSharp
ms.assetid: 33601bf3-cc2c-4496-846d-f9679bccf2a7
caps.latest.revision: 3
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
ms.sourcegitcommit: dc1c456c71efb3cc6e60a8fdc77384e65975f110
ms.openlocfilehash: da3fef282ac71de07057131069bf58d4f761ad2d
ms.contentlocale: es-es
ms.lasthandoff: 05/15/2017

---
# <a name="nameof-c-and-visual-basic-reference"></a>nameof (Refernecia de C# y Visual Basic)

Se utiliza para obtener el nombre de cadena (incompleto) simple de una variable, tipo o miembro.  

Al informar de errores en el código, enlazar vínculos de controlador de vistas de modelo (MVC), desencadenar eventos de propiedad cambiada, etc., a menudo le interesa capturar el nombre de cadena de un método.  Usar `nameof` ayuda a lograr que su código siga siendo válido al cambiar el nombre de definiciones.  Antes había que usar literales de cadena para hacer referencia a definiciones, lo que resulta precario al cambiar el nombre de elementos de código, ya que las herramientas no saben comprobar estos literales de cadena.  
  
 Una expresión `nameof` tiene este formato:  
  
```csharp  
if (x == null) throw new ArgumentNullException(nameof(x));  
WriteLine(nameof(person.Address.ZipCode)); // prints "ZipCode"  
```  
  
## <a name="key-use-cases"></a>Casos de uso clave  
 Estos ejemplos muestran los casos de uso clave para `nameof`.  
  
 Validar parámetros:  
 ```csharp  
void f(string s) {  
    if (s == null) throw new ArgumentNullException(nameof(s));  
}  
```  
  
 Vínculos de acción de MVC:  
 ```html  
<%= Html.ActionLink("Sign up",  
             @typeof(UserController),  
             @nameof(UserController.SignUp))  
%>  
```  
  
 INotifyPropertyChanged:  
 ```csharp  
int p {  
    get { return this.p; }  
    set { this.p = value; PropertyChanged(this, new PropertyChangedEventArgs(nameof(this.p)); } // nameof(p) works too  
}  
```  
  
 Propiedad de dependencia de XAML:  
 ```csharp  
public static DependencyProperty AgeProperty = DependencyProperty.Register(nameof(Age), typeof(int), typeof(C));  
```  
  
 Registro:  
 ```csharp  
void f(int i) {  
    Log(nameof(f), "method entry");  
}  
```  
  
 Atributos:  
 ```csharp  
[DebuggerDisplay("={" + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```  
  
## <a name="examples"></a>Ejemplos  
 Algunos ejemplos de C#:  
  
```csharp  
using Stuff = Some.Cool.Functionality  
class C {  
    static int Method1 (string x, int y) {}  
    static int Method1 (string x, string y) {}  
    int Method2 (int z) {}  
    string f<T>() => nameof(T);  
}  
  
var c = new C()  
  
nameof(C) -> "C"  
nameof(C.Method1) -> "Method1"   
nameof(C.Method2) -> "Method2"  
nameof(c.Method1) -> "Method1"   
nameof(c.Method2) -> "Method2"  
nameof(z) -> "z" // inside of Method2 ok, inside Method1 is a compiler error  
nameof(Stuff) = "Stuff"  
nameof(T) -> "T" // works inside of method but not in attributes on the method  
nameof(f) -> "f"  
nameof(f<T>) -> syntax error  
nameof(f<>) -> syntax error  
nameof(Method2()) -> error "This expression does not have a name"  
```  
  
 Muchos de los ejemplos anteriores se aplican a Visual Basic.  A continuación presentamos algunos ejemplos específicos de Visual Basic:  
  
```vb  
NameOf(a!Foo) -> ' error  "This expression does not have a name"  
NameOf(dict("Foo")) -> ' error  "This expression does not have a name": default property access  
NameOf(dict.Item("Foo")) -> ' error  "This expression does not have a name"  
NameOf(arr(2)) -> ' error  "This expression does not have a name": array element index  
Dim x = Nothing   
NameOf(x.ToString(2)) -> ' error  "This expression does not have a name"  
Dim o = Nothing  
NameOf(o.Equals) -> ' result "Equals".  Warning: "Access of static member of instance; instance will not be evaluated"  
```  
  
## <a name="remarks"></a>Comentarios  
 El argumento `nameof` debe ser un nombre sencillo, nombre completo, acceso a miembros, acceso base a un miembro especificado o este acceso a un miembro especificado.  La expresión de argumento identifica una definición de código, pero nunca se evalúa.  
  
 Dado que el argumento debe ser sintácticamente una expresión, hay muchas cosas no permitidas que no sería útil mostrar.  Sí vale la pena mencionar los siguientes elementos que producen errores: tipos predefinidos (por ejemplo, `int` o `void`), tipos que aceptan valores null (`Point?`), tipos de matriz (`Customer[,]`), tipos de puntero (`Buffer*`), alias completo (`A::B`), tipos genéricos sin enlazar (`Dictionary<,>`), símbolos de preprocesamiento (`DEBUG`) y etiquetas (`loop:`).  
  
 Si necesita obtener el nombre completo, puede utilizar la expresión `typeof` junto con `nameof`.  Por ejemplo:
```csharp  
class C {
    void f(int i) {  
        Log($"{typeof(C)}.{nameof(f)}", "method entry");  
    }
}
``` 

 `typeof` no es una expresión constante como `nameof`, por lo que `typeof` no puede usarse junto con `nameof` en los mismos lugares que `nameof`.  Por ejemplo, el siguiente ejemplo provocaría un error de compilación CS0182:
 ```csharp  
[DebuggerDisplay("={" + typeof(C) + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```    
 En los ejemplos verá que puede utilizar un nombre de tipo y acceder a un nombre de método de instancia.  No es necesario tener una instancia del tipo, tal como se requiere en las expresiones evaluadas.  Usar el nombre de tipo puede ser muy práctico en algunas situaciones, y puesto que solo hace referencia al nombre y no utiliza datos de instancia, no necesita idear una expresión o una variable de instancia.  
  
 Puede hacer referencia a los miembros de una clase en expresiones de atributos en la clase.  
  
 No hay ninguna manera de obtener información de firma, como "`Method1 (str, str)`".  Una manera de hacerlo es usar una expresión, `Expression e = () => A.B.Method1("s1", "s2")`, y extraer el MemberInfo del árbol de expresión resultante.  
  
## <a name="language-specifications"></a>Especificaciones del lenguaje  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
 Para obtener más información, vea [Referencia del lenguaje Visual Basic](../../../visual-basic/language-reference/index.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de C#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [Referencia del lenguaje Visual Basic](../../../visual-basic/language-reference/index.md)   
 [Guía de programación en Visual Basic](../../../visual-basic/programming-guide/index.md)

