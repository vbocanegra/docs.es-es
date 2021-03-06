---
title: "Implementar un administrador de recursos  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5c153f6-4419-49e3-a5f1-a50ae4c81bf3
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Implementar un administrador de recursos 
Un administrador de recursos administra cada recurso utilizado, cuyas acciones coordina un administrador de transacciones.Los administradores de recursos trabajan en cooperación con el administrador de transacciones para proporcionar una garantía de atomicidad y aislamiento a la aplicación.Microsoft SQL Server, colas de mensajes durables, las tablas hash en memoria, son ejemplos de administradores de recursos.  
  
 Un administrador de recursos administra los datos duraderos o volátiles.La duración \(o a la inversa la volatilidad\) de un administrador de recursos hace referencia a si el administrador de recursos admite la recuperación del error.Si un administrador de recursos admite la recuperación del error, conserva los datos del almacenamiento duradero durante la fase1 \(preparación\) de tal manera que si el administrador de recursos baja, puede reenganchar la transacción en la recuperación y realizar las acciones apropiadas basadas en las notificaciones recibidas del administrador de recursos.En general, los administradores de recursos volátiles administran recursos volátiles como una estructura de datos en memoria \(por ejemplo, una tabla hash llevada a cabo en memoria\) y los administradores de recursos duraderos administran recursos que tienen una memoria auxiliar más persistente \(por ejemplo, una base de datos cuyo dispositivo de copia de seguridad es el disco\).  
  
 Para que un administrador de recursos participe en una transacción, debe inscribirse en la transacción.La clase <xref:System.Transactions.Transaction> define un conjunto de métodos cuyos nombres comienzan con **Enlist** que proporcionan esta funcionalidad.Los distintos métodos **Enlist** corresponden a los distintos tipos de inscripción que un administrador de recursos puede tener.Específicamente, utiliza los métodos <xref:System.Transactions.Transaction.EnlistVolatile%2A> para los recursos volátiles y el método <xref:System.Transactions.Transaction.EnlistDurable%2A> para los recursos duraderos.Para simplificar, después de decidir si utilizar el método<xref:System.Transactions.Transaction.EnlistDurable%2A> o <xref:System.Transactions.Transaction.EnlistVolatile%2A> basado en la compatibilidad de la duración de su recurso, debería dar de alta su recurso para participar en la confirmación en dos fases \(2PC\) implementando la interfaz <xref:System.Transactions.IEnlistmentNotification> para su administrador de recursos.\(Para obtener más información sobre 2PC, vea [Confirmar una transacción en fase única y fase múltiple ](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)\).  
  
 Dando de alta, el administrador de recursos se asegura de que recibe las devoluciones de llamada del administrador de transacciones cuando la transacción se confirma o interrumpe.Hay una instancia de <xref:System.Transactions.IEnlistmentNotification> por la inscripción.Hay normalmente, una inscripción por la transacción, pero un administrador de recursos puede decidir darse de alta varias veces en la misma transacción.  
  
 Después de la inscripción, el administrador de recursos responde a las solicitudes de la transacción.Un administrador de recursos duradero almacena bastante información para permitir que deshaga o rehaga el trabajo de la transacción de los recursos que él administra.Hay muchas maneras para ello; manteniendo versiones de datos o manteniendo un registro de los cambios son dos técnicas comunes.  
  
 Cuando la aplicación confirma la transacción, el administrador de transacciones inicia el protocolo de confirmación en dos fases.El administrador de transacciones pregunta primero a cada administrador de recursos inscrito si está preparado para confirmar la transacción.El administrador de recursos debe prepararse para confirmar o anular la transacción.  
  
 Durante la fase de preparación, el administrador de recursos duraderos graba los datos anteriores y nuevos en almacenamiento estable para que el administrador de recursos pueda recuperarlos incluso cuando se produzca un error en el sistema.Si el administrador de recursos puede prepararse, informa sobre su voto al administrador de transacciones si va a confirmar o anular la transacción.Si cualquier administrador de recursos informa de un error para preparar, el administrador de transacciones envía un comando de recuperación a cada administrador de recursos e indica el error de la confirmación a la aplicación.  
  
 Una vez preparado, un administrador de recursos debe esperar hasta que reciba una devolución de llamada de confirmación o de interrupción del administrador de transacciones en la fase 2.Normalmente, todo el protocolo de confirmación y preparación se completa en una fracción de un segundo.Si hay sistema o errores de comunicación, la confirmación o anulación de la notificación no puede llegar durante minutos u horas.Durante este período, el administrador de recursos está en duda sobre el resultado de la transacción.No sabe si la transacción se confirmó o se anuló.Aunque el administrador de recursos está en duda sobre una transacción, mantiene los datos modificados manteniendo la transacción bloqueada, aislando por eso estos cambios de cualquier otra transacción.  
  
 Cuando se produce un error en un administrador de recursos, todas sus transacciones inscritas se anulan salvo aquellas que se preparan o se confirman antes del error.Cuando un administrador de recursos duraderos se reinicia, se reconstruye el estado confirmado de los recursos que administra recuperando la información de preparación escrita la fase de preparación y confirma o anula de acuerdo con estas transacciones.  
  
 En resumen, el protocolo de confirmación en dos fases y los administradores de recursos se combinan para hacer las transacciones atómicas y duraderas.  
  
 La clase <xref:System.Transactions.Transaction> también proporciona el método <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> para dar de alta una Inscripción de fase única promocional \(PSPE\).Esto permite a un administrador de recursos duradero \(RM\) hospedar y "poseer" una transacción que puede realizar una escalada para que sea administrada por MSDTC si es necesario.Para obtener más información sobre este tema vea [Optimización mediante el uso de la confirmación de fase única y de la confirmación de fase única promocionable ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md).  
  
## En esta sección  
 Los pasos generalmente seguidos por un administrador de recursos se describen en los temas siguientes.  
  
 [Dar de alta recursos como participantes en una transacción ](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)  
  
 Describe cómo un recurso duradero o volátil puede darse de alta en una transacción.  
  
 [Confirmar una transacción en fase única y fase múltiple ](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)  
  
 Describe cómo un administrador de recursos responde para confirmar la notificación y preparar la confirmación.  
  
 [Realizar la recuperación ](../../../../docs/framework/data/transactions/performing-recovery.md)  
  
 Describe cómo un administrador de recursos duradero se recupera del error.  
  
 [Niveles de confianza de seguridad en el acceso a recursos ](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md)  
  
 Define cómo tres niveles de confianza para System.Transactions restringen el acceso a los tipos de recursos que <xref:System.Transactions> expone.  
  
 [Optimización mediante el uso de la confirmación de fase única y de la confirmación de fase única promocionable ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md)  
  
 Describe los ejercicios de la optimización disponible sobre las implementaciones de administradores de recursos.