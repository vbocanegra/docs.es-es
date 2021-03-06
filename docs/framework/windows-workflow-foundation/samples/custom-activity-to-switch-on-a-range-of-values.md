---
title: "Actividad personalizada para cambiar en un intervalo de valores | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 441e0a17-421f-430c-ba97-59e4cc6c88e3
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Actividad personalizada para cambiar en un intervalo de valores
En este ejemplo se muestra cómo crear una actividad personalizada que amplía el uso de una instrucción <xref:System.Activities.Statements.Switch%601>.Una instrucción <xref:System.Activities.Statements.Switch%601> convencional permite el cambio en función de un único valor.Sin embargo, existen escenarios empresariales donde una actividad debe cambiar en función de un intervalo de valores.Por ejemplo, una actividad podría ejecutar una acción cuando el valor de cambio se sitúa entre 1 y 5, otra acción cuando el valor se sitúa entre 6 y 10 y una acción predeterminada para los demás valores.Esta actividad personalizada permite exactamente ese escenario.  
  
## Actividad SwitchRange  
 La actividad `SwitchRange` programa una actividad secundaria cuando el valor de resultado de su expresión está incluido dentro del intervalo de uno de `Cases`.  
  
 El siguiente ejemplo de código es una actividad personalizada que cambia en función de un intervalo de valores.  
  
```csharp  
  
public sealed class SwitchRange<T> : NativeActivity where T : IComparable  
{  
   [RequiredArgument]  
   [DefaultValue(null)]  
   public InArgument<T> Expression { get; set; }  
  
   public IList<CaseRange<T>> Cases  
  
   [DefaultValue(null)]  
   public Activity Default { get; set; }}  
}  
```  
  
|||  
|-|-|  
|Propiedad|Descripción|  
|Expresión|Es la expresión que se va a evaluar y comparar con los intervalos de la lista Cases.El resultado de la expresión es de tipo T.|  
|Cases|Cada caso consta de un intervalo \(From y To\) y una actividad \(Body\).La expresión se evalúa y se compara con los intervalos.Si el resultado de la expresión se sitúa dentro del intervalo de uno de los casos, se ejecuta la actividad correspondiente.|  
|Default|La actividad que se ejecuta cuando no coincide ningún caso.Cuando se establece en `null`, no se realiza ninguna acción.|  
  
## Clase CaseRange  
 La clase `CaseRange` representa un intervalo dentro de una actividad `SwitchRange`.Cada instancia de `CaseRange` contiene un intervalo \(compuesto de `From` y `To`\) y una actividad `Body` que se programan si la expresión de `SwitchRange` se evalúa dentro del intervalo.  
  
 El ejemplo de código siguiente es la definición de la clase `CaseRange`.  
  
```  
  
public class CaseRange<T> where T : IComparable  
{  
    public T From { get; set; }  
  
    public T To { get; set; }  
  
    public Activity Action { get; set; }  
}  
```  
  
> [!NOTE]
>  Las clases `CaseRange` y `SwitchRange` que se definen en el ejemplo son clases genéricas que pueden funcionar con cualquier tipo que implemente `IComparable`, como la clase <xref:System.Activities.Statements.Switch%601>.  
  
## Uso del ejemplo  
 En el ejemplo de código siguiente se muestra cómo utilizar la actividad `SwitchRange`.  
  
```csharp  
  
Activity SwitchRange = new SwitchRange<int>  
{  
    Expression = new InArgument<int>(value),  
    Cases =   
    {  
        new CaseRange<int>                      
        {  
            From = 1,  
            To = 5,  
            Action = new WriteLine  
            {  
                Text = "Case 1-5 selected",  
            }  
        },  
        new CaseRange<int>  
        {  
            From = 6,  
            To = 10,  
            Action = new WriteLine  
            {  
                Text = "Case 6-10 selected",  
            }  
        }  
    },  
    Default = new WriteLine { Text = "Default Case selected" }  
};  
```  
  
#### Para utilizar este ejemplo  
  
1.  Con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], abra el archivo de solución SwitchRange.sln.  
  
2.  Para compilar la solución, presione Ctrl\+MAYÚS\+B.  
  
3.  Para ejecutar la solución, presione CTRL\+F5.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SwitchRange`  
  
## Vea también