---
title: "Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a4ead79-8550-4037-84e3-fd70ff56e001
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure
El servicio de protocolo WS\-AT no pudo registrar a un participante para un protocolo de control.  
  
## Descripción  
 Se realiza el seguimiento si MSDTC detecta una solicitud de registro no válida.Esto puede deberse a varias solicitudes de registro de realización y errores internos.  
  
## Solución de problemas  
 No intente registrarse para la realización más de una vez.Asimismo, inspeccione la cadena de estado dentro del mensaje de seguimiento para determinar si existe cualquier elemento al que se le puede realizar alguna acción.  
  
## Vea también  
 [Seguimiento](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Uso del seguimiento para solucionar problemas de su aplicación](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Administración y diagnóstico](../../../../../docs/framework/wcf/diagnostics/index.md)