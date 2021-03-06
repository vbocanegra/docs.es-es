---
title: "Realizar la recuperaci&#243;n  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6dd17bf6-ba42-460a-a44b-8046f52b10d0
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Realizar la recuperaci&#243;n 
El administrador de recursos facilita la resolución de inscripciones duraderas en una transacción volviendo a inscribir al participante de la transacción después de un error de recurso.  
  
## El Proceso de la recuperación  
 Para dar de alta de forma duradera a un recurso \(se describe por una implementación de la interfaz <xref:System.Transactions.IEnlistmentNotification>\) que puede ser después elegible para la recuperación, debería llamar al método <xref:System.Transactions.Transaction.EnlistDurable%2A>.Además, debe proporcionar un identificador del administrador de recursos \(un <xref:System.Guid>\) que se utiliza para etiquetar de forma consistente al participante de la transacción en caso de un error de recurso al método <xref:System.Transactions.Transaction.EnlistDurable%2A>.Por esta razón, el <xref:System.Guid> que se proporcionan a la llamada de inscripción inicial debería ser idéntica al parámetro *resourceManagerIdentifier* en la llamada <xref:System.Transactions.TransactionManager.Reenlist%2A> durante la recuperación.De lo contrario, se produce <xref:System.Transactions.TransactionException>.Para obtener más información sobre las inscripciones duraderas vea [Dar de alta recursos como participantes en una transacción ](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md).  
  
 En la fase de preparación \(fase 1\) del  protocolo 2PC, cuando su implementación de un administrador de recursos duradero recibe la notificación <xref:System.Transactions.IEnlistmentNotification.Prepare%2A>, debería registrar su registro de preparación durante esta fase.El registro debería contener toda la información que es necesaria para completar la transacción en confirmación.Se puede tener acceso al registro de preparación después, durante la recuperación, recuperando la propiedad <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> de la devolución de llamada *preparingEnlistment*.El registro del registro no necesita ser realizado dentro del método <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> cuando RM puede hacer esto en un subproceso de trabajo.  
  
 El proceso de recuperación consiste de los dos siguientes pasos:  
  
### El paso 1 \- ReEnlist  
 El administrador de recursos examina el registro de preparación de la información para cada inscripción que está dudosa.Esto se hace examinando la propiedad <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> de la devolución de llamada <xref:System.Transactions.PreparingEnlistment>, que se pasa al administrador de recursos en la notificación <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> durante fase 1.  
  
 Para cada inscripción que examina, invoca <xref:System.Transactions.TransactionManager.Reenlist%2A> en el administrador de transacciones.Este método pasa en un <xref:System.Guid> único que identifica el administrador de recursos, así como la información de la inscripción en una matriz de bytes.Se devuelve un objeto nuevo <xref:System.Transactions.Enlistment> .En caso de error en el reenganche con una excepción, el administrador de recursos necesitará reintentar en un momento posterior.  
  
 Solo debería llamar al <xref:System.Transactions.TransactionManager.Reenlist%2A> método si un administrador de recursos se reinicia a partir de un error.Además, solo debería volver a inscribir las transacciones sin resolver registradas por un administrador de recursos durante fase de preparación inicial de una confirmación en dos fases.Cualquier intento de llamar a este método en momentos que no corresponda puede generar resultados erróneos.  
  
 Cuando se vuelve a inscribir un participante con este método, se llama a los métodos de la fase 2 de <xref:System.Transactions.IEnlistmentNotification> que corresponden al resultado de la transacción \(es decir, <xref:System.Transactions.IEnlistmentNotification.Commit%2A>, <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> o <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A>\) según sea adecuado.  
  
### El paso 2 \- Completando la recuperación  
 Cuando todas las inscripciones hayan finalizado el administrador de recursos llamará al método <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>.Este método completa la recuperación e informa el administrador de transacciones de que el administrador de recursos no tiene ninguna transacción dudosa más.Haciendo esto, el administrador de recursos garantiza que no invocará de nuevo el método <xref:System.Transactions.TransactionManager.Reenlist%2A>.  
  
 No se exige a un administrador de recursos que resuelva todas las transacciones dudosas antes de dar de alta nuevas transacciones.Se puede realizar el primer paso en cualquier momento después de que el administrador de recursos establezca una relación con el administrador de transacciones, pero una vez invocado \(el paso 2\) <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>; no se puede realizar el paso 1 de nuevo.El paso 2 se puede repetir varias veces sin afectar al resultado de transacciones.