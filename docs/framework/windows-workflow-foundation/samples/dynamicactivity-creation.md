---
title: "Creaci&#243;n de DynamicActivity | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d8ebe82f-98c8-4452-aed7-2c60a512b097
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Creaci&#243;n de DynamicActivity
En este ejemplo se muestran dos maneras diferentes de crear una actividad en tiempo de ejecución utilizando la actividad <xref:System.Activities.DynamicActivity>.  
  
 En este ejemplo, se crea una actividad en tiempo de ejecución con un cuerpo que contiene una actividad <xref:System.Activities.Statements.Sequence> que incluye las actividades <xref:System.Activities.Statements.Assign%601> y <xref:System.Activities.Statements.ForEach%601>.Se pasa una lista de entrada de enteros a la actividad y se establece como una propiedad.A continuación, la actividad <xref:System.Activities.Statements.ForEach%601> recorre en iteración la lista de valores y la acumula.En la actividad <xref:System.Activities.Statements.Assign%601>, el valor medio se calcula dividiendo el acumulador por el número de elementos en la lista y asignándolo a la media.  
  
 En el ejemplo se muestra el uso de una actividad <xref:System.Activities.DynamicActivity> que pasa variables como argumentos de entrada y devuelve valores como argumentos de salida.La actividad tiene un argumento de entrada denominado `Numbers` que es una lista de enteros.La actividad <xref:System.Activities.Statements.ForEach%601> recorre en iteración la lista de valores y la acumula.En la actividad <xref:System.Activities.Statements.Assign%601>, el valor medio se calcula dividiendo el acumulador por el número de elementos en la lista y asignándolo a la media.La media se devuelve como un argumento de salida denominado `Average`.  
  
 Cuando se crea la actividad dinámica mediante programación, la entrada y la salida se declaran como se muestra en el siguiente ejemplo de código.  
  
```csharp  
DynamicActivity act = new DynamicActivity()  
{  
    DisplayName = "Find average",  
    Properties =   
    {  
        // Input argument  
        new DynamicActivityProperty  
        {  
            Name = "Numbers",  
            Type = typeof(InArgument<List<int>>),  
            Value = numbers  
        },  
        // Output argument  
        new DynamicActivityProperty  
        {  
            Name = "Average",  
            Type = typeof(OutArgument<double>),  
            Value = average  
        }  
    },  
};  
  
```  
  
 El siguiente ejemplo de código muestra la definición completa de `DynamicActivity` que calcula la media de los valores de una lista.  
  
```  
DynamicActivity act = new DynamicActivity()  
{  
    DisplayName = "Find average",  
    Properties =   
    {  
        // Input argument  
        new DynamicActivityProperty  
        {  
            Name = "Numbers",  
            Type = typeof(InArgument<List<int>>),  
            Value = numbers  
        },  
        // Output argument  
        new DynamicActivityProperty  
        {  
            Name = "Average",  
            Type = typeof(OutArgument<double>),  
            Value = average  
        }  
    },  
    Implementation = () =>  
        new Sequence  
        {  
            Variables = { result, accumulator },  
            Activities =  
            {  
                new ForEach<int>  
                {  
                    Values =  new ArgumentValue<IEnumerable<int>> { ArgumentName = "Numbers" },                                  
                    Body = new ActivityAction<int>  
                    {  
                        Argument = iterationVariable,  
                        Handler = new Assign<int>  
                        {  
                            To = accumulator,  
                            Value = new InArgument<int>(env => iterationVariable.Get(env) +  accumulator.Get(env))  
                        }  
                    }  
                },  
  
                // Calculate the average and assign to the output argument.  
                new Assign<double>  
                {  
                    To = new ArgumentReference<double> { ArgumentName = "Average" },  
                    Value = new InArgument<double>(env => accumulator.Get(env) / numbers.Get(env).Count<int>())  
                },  
            }  
        }  
};  
```  
  
 Cuando se crean en XAML, la entrada y salida se declaran como se muestra en el siguiente ejemplo.  
  
```  
<Activity x:Class="Microsoft.Samples.DynamicActivityCreation.FindAverage"  
          xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
          xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <x:Members>  
    <x:Property Name="Numbers" Type="InArgument(scg:List(x:Int32))" />  
    <x:Property Name="Average" Type="OutArgument(x:Double)" />  
  </x:Members>  
    ...  
    ...  
</Activity>  
```  
  
 El XAML se puede crear visualmente utilizando [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)].Si está incluido en un proyecto de Visual Studio, asegúrese de establecer su "Acción de compilación" en "Ninguna" para evitar que se compile.El XAML se puede cargar entonces dinámicamente utilizando la siguiente llamada.  
  
```  
Activity act2 = ActivityXamlServices.Load(@"FindAverage.xaml");  
  
```  
  
 La instancia de <xref:System.Activities.DynamicActivity> creada mediante programación o a través de la carga de un flujo de trabajo de XAML se puede utilizar como se muestra en el siguiente ejemplo de código.Observe que el "acto" pasado a `WorkflowInvoker.Invoke` es el "acto" <xref:System.Activities.Activity> definido en el primer ejemplo de código.  
  
```  
IDictionary<string, object> results = WorkflowInvoker.Invoke(act, new Dictionary<string, object> { { "Numbers", numbers } });  
  
Console.WriteLine("The average calculated using the code activity is = " + results["Average"]);  
  
```  
  
#### Para utilizar este ejemplo  
  
1.  Abra el archivo de solución de DynamicActivityCreation.sln con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Para compilar la solución, presione Ctrl\+MAYÚS\+B.  
  
3.  Para ejecutar la solución, presione CTRL\+F5.  
  
## Argumentos de línea de comandos  
 En este ejemplo se aceptan los argumentos de la línea de comandos.Los usuarios pueden proporcionar una lista de números para que la actividad calcule su media.La lista de números que se va a utilizar se pasa como una lista de números separados por un espacio.Por ejemplo, para calcular la media de 5, 10 y 32, invoque el ejemplo utilizando la siguiente línea de comandos.  
  
 **DynamicActivityCreation 5 10 32**   
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(valor predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] y [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Basic\Built-InActivities\DynamicActivity\DynamicActivityCreation`  
  
## Vea también