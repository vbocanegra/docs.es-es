---
title: "Emular la ruptura en una actividad While | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ddff715d-d623-4b54-b841-60bacbc3ca21
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Emular la ruptura en una actividad While
En este ejemplo se muestra cómo interrumpir el mecanismo de bucle de las siguientes actividades: <xref:System.Activities.Statements.DoWhile>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.While>y <xref:System.Activities.Statements.ParallelForEach%601>.  
  
 Esto resulta útil porque [!INCLUDE[wf](../../../../includes/wf-md.md)] no incluye ninguna actividad para interrumpir la ejecución de estos bucles.  
  
## Situación  
 En el ejemplo se encuentra el primer proveedor de confianza en una lista de proveedores \(instancias de la clase `Vendor`\).Cada proveedor tiene un `ID`, un `Name` y un valor de confiabilidad numérico que determina la fiabilidad del proveedor.En el ejemplo se crea una actividad personalizada llamada `FindReliableVendor` que recibe dos parámetros de entrada \(una lista de proveedores y un valor de confiabilidad mínimo\) y devuelve el primer proveedor de la lista que coincide con los criterios proporcionados.  
  
## Interrumpir un bucle  
 [!INCLUDE[wf](../../../../includes/wf-md.md)] no incluye ninguna actividad para interrumpir un bucle.El ejemplo de código logra interrumpir un bucle utilizando una actividad <xref:System.Activities.Statements.If> y diferentes variables.En el ejemplo, la actividad <xref:System.Activities.Statements.While> se interrumpe cuando se asigna a la variable `reliableVendor` un valor distinto de `null`.  
  
 El siguiente ejemplo de código muestra cómo el ejemplo interrumpe un bucle while.  
  
```csharp  
// Iterates while the “i” variable is lower than the size of the list   
// and any reliable Vendor is found.        
new While(env => i.Get(env) < this.Vendors.Get(env).Count && reliableVendor.Get(env) == null)  
{  
    DisplayName = "Main loop. Breaks when a reliable vendor is found",  
    Body = new Sequence  
    {                              
        Activities =  
        {  
            // This is the if used for setting the value of the break value…  
            new If  
            {  
                DisplayName = "Check for a reliable vendor",  
  
                //  If a vendor satisfies the reliability level…  
                Condition = new InArgument<bool>(env =>   
                           this.Vendors.Get(env)[i.Get(env)].Reliability >   
                           this.MinimumReliability.Get(env)),  
  
                // then assign that vendor to the reliable vendor variable and   
                // the while condition becomes false (exit the loop).  
                Then = new Assign<Vendor>  
                {  
                    To = reliableVendor,  
                    Value = new InArgument<Vendor>(env =>   
                                  this.Vendors.Get(env)[i.Get(env)])  
                }  
            },  
  
            // Increment the iteration variable.   
            new Assign<int>  
            {  
                DisplayName = "Increment iteration variable",  
                To = i,  
                Value = new InArgument<int>(env => i.Get(env) + 1)  
            }   
        }  
    }  
}  
  
```  
  
#### Para utilizar este ejemplo  
  
1.  Abra el archivo de solución EmulatingBreakInWhile.sln con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Para compilar la solución, presione Ctrl\+MAYÚS\+B.  
  
3.  Para ejecutar la solución, presione CTRL\+F5.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Basic\Built-InActivities\EmulatingBreakInWhile`  
  
## Vea también