---
title: "Mensajes por lotes en una transacci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mensajes por lotes [WCF]"
ms.assetid: 53305392-e82e-4e89-aedc-3efb6ebcd28c
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Mensajes por lotes en una transacci&#243;n
Las aplicaciones en cola utilizan las transacciones para garantizar la exactitud y la entrega fiable de mensajes.Las transacciones, sin embargo, son operaciones caras y pueden reducir dramáticamente el rendimiento de los mensajes.Una manera de mejorar el rendimiento de los mensajes consiste en hacer que una aplicación lea y procese varios mensajes dentro de una transacción única.La balanza está entre el rendimiento y la recuperación: a medida que el número de mensajes de un lote aumenta, lo hace la cantidad de trabajo de recuperación requerida si se deshacen las transacciones.Es importante tener en cuenta la diferencia entre los mensajes por lotes en una transacción y en sesiones.Una *sesión* es una agrupación de mensajes relacionados que son procesados por una única aplicación y se confirman como una unidad única.Las sesiones se utilizan generalmente cuando se debe procesar conjuntamente un grupo de mensajes relacionados.Un ejemplo de esto es el sitio web de una tienda en línea.Los *lotes* se usan para procesar varios mensajes no relacionados de tal manera que se aumente el rendimiento de mensajes.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sesiones, vea [Agrupación de los mensajes en cola de una sesión](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md).Los mensajes de un lote también se procesan mediante una aplicación única y se confirman como una sola unidad, pero no puede haber ninguna relación entre los mensajes del lote.Los mensajes por lotes en una transacción son una optimización que no cambia cómo se ejecuta la aplicación.  
  
## Introducción al modo de procesamiento por lotes  
 El comportamiento de extremo <xref:System.ServiceModel.Description.TransactedBatchingBehavior> controla el procesamiento por lotes.Al agregar este comportamiento de extremo a un extremo de servicio se indica a [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] que procese los mensajes por lotes en una transacción.No todos los mensajes requieren una transacción, por lo que solo los mensajes que requieren una transacción se colocan en un lote y solo los mensajes enviados desde las operaciones marcados con `TransactionScopeRequired` \= `true` y `TransactionAutoComplete` \= `true` se consideran para un lote.Si todas las operaciones en el contrato de servicios se marcan con `TransactionScopeRequired` \= `false` y `TransactionAutoComplete` \= `false`, nunca se entra en el modo por lotes.  
  
## Confirmación de una transacción.  
 Una transacción por lotes se confirma en función de lo siguiente:  
  
-   `MaxBatchSize`.Una propiedad del comportamiento <xref:System.ServiceModel.Description.TransactedBatchingBehavior>.Esta propiedad determina el número máximo de mensajes que se colocan en un lote.Cuando se alcanza este número, se confirma el lote.Esto valor no es un límite estricto, es posible confirmar un lote antes de recibir este número de mensajes.  
  
-   `Transaction Timeout`.Después de que el 80 por ciento del tiempo de espera de la transacción haya transcurrido, se confirma el lote y se crea uno nuevo.Esto significa que si queda el 20 por ciento o menos del tiempo proporcionado para que una transacción se complete, se confirma el lote.  
  
-   `TransactionScopeRequired`.Al procesar un lote de mensajes, si [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] encuentra uno que tenga `TransactionScopeRequired` \= `false`, confirma el lote y vuelve a abrir un nuevo lote al recibir el primer mensaje con `TransactionScopeRequired` \= `true` y `TransactionAutoComplete` \= `true`.  
  
-   Si no existe ningún mensaje más en la cola, se confirma el lote actual, aunque no se haya alcanzado el `MaxBatchSize` o no haya transcurrido el 80 por ciento del tiempo de espera de la transacción.  
  
## Salir del modo de procesamiento por lotes  
 Si un mensaje en un lote hace que la transacción se anule, se producen los pasos siguientes:  
  
1.  Se deshace el lote completo de mensajes.  
  
2.  Los mensajes se leen de uno en uno hasta que el número de mensajes leídos supera el doble del tamaño del lote máximo.  
  
3.  Se vuelve a entrar en el modo de procesamiento por lotes.  
  
## Elección del tamaño del lote  
 El tamaño de un lote depende de la aplicación.El método empírico es la mejor manera de llegar a un tamaño de lote óptimo para la aplicación.Es importante recordar al elegir un tamaño de lote para elegir el tamaño según el modelo de implementación real de su aplicación.Por ejemplo, al implementar la aplicación, si necesita un servidor SQL en un equipo remoto y una transacción que abarque la cola y el servidor SQL, el tamaño del lote se determina mejor ejecutando esta configuración exacta.  
  
## Simultaneidad y procesamiento por lotes  
 Para aumentar el rendimiento, puede hacer que se ejecuten muchos lotes de manera simultánea.Estableciendo `ConcurrencyMode.Multiple` en `ServiceBehaviorAttribute`, se habilita el procesamiento por lotes simultáneo.  
  
 La *limitación de peticiones de servicio* es un comportamiento del servicio que se utiliza para indicar el número máximo de llamadas concurrentes que se pueden realizar en el servicio.Cuando se utiliza con procesamiento por lotes, esto se interpreta como cuántos lotes simultáneos se pueden ejecutar.Si no se establece la limitación de peticiones del servicio, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] establece el número máximo de llamadas simultáneas en 16.De este modo, si se agregara el comportamiento de procesamiento por lotes de forma predeterminada, podrían estar activos un máximo de 16 lotes al mismo tiempo.Es mejor ajustar la limitación de peticiones del servicio y el procesamiento por lotes en función de su capacidad.Por ejemplo, si la cola tiene 100 mensajes y se desea un lote de 20, tener el número máximo de llamadas simultáneas establecido en 16 no sería útil porque, dependiendo del rendimiento, 16 transacciones podrían estar activas, parecido a no tener el procesamiento por lotes activado.Por consiguiente, al afinar para mejorar el rendimiento, no tenga el procesamiento por lotes simultáneo o tenga el procesamiento por lotes simultáneo con el tamaño correcto de limitación de peticiones del servicio.  
  
## Procesamiento por lotes y varios extremos  
 Un extremo está compuesto por una dirección y un contrato.Puede haber varios extremos que comparten el mismo enlace.Es posible que dos extremos compartan el mismo enlace y escuchen al Identificador uniforme de recursos \(URI\) o dirección de la cola.Si dos extremos están leyendo desde la misma cola, y se agrega el comportamiento del procesamiento por lotes con transacciones a ambos extremos, podría surgir un conflicto en los tamaños de lotes especificados.Esto se resuelve implementando el procesamiento por lotes utilizando el tamaño de lote mínimo especificado entre los dos comportamientos de procesamiento por lotes con transacciones.En este escenario, si uno de los extremos no especifica el procesamiento por lotes con transacciones, ambos extremos no usarán el procesamiento por lotes.  
  
## Ejemplo  
 El siguiente ejemplo muestra cómo especificar el `TransactedBatchingBehavior` en un archivo de configuración.  
  
```  
<behaviors>  
      <endpointBehaviors>  
        <behavior name="TransactedBatchingBehavior"  
                  maxBatchSize="100"/>  
      </endpointBehaviors>  
    </behaviors>  
```  
  
 En el siguiente ejemplo se muestra cómo especificar mediante código <xref:System.ServiceModel.Description.TransactedBatchingBehavior>.  
  
```  
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
{  
     ServiceEndpoint sep = ServiceHost.AddServiceEndpoint(typeof(IOrderProcessor), new NetMsmqBinding(), "net.msmq://localhost/private/ServiceModelSamplesTransacted");  
                sep.Behaviors.Add(new TransactedBatchingBehavior(100));  
  
     // Open the ServiceHost to create listeners and start listening for messages.  
    serviceHost.Open();  
  
    // The service can now be accessed.  
    Console.WriteLine("The service is ready.");  
    Console.WriteLine("Press <ENTER> to terminate service.");  
    Console.WriteLine();  
    Console.ReadLine();  
  
   // Close the ServiceHostB to shut down the service.  
    serviceHost.Close();  
}  
```  
  
## Vea también  
 [Información general de colas](../../../../docs/framework/wcf/feature-details/queues-overview.md)   
 [Las colas en WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)