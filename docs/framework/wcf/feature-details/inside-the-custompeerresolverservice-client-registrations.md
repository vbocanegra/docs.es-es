---
title: "Dentro de CustomPeerResolverService: registros de cliente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40236953-a916-4236-84a6-928859e1331a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Dentro de CustomPeerResolverService: registros de cliente
Cada nodo de la malla publica su información de extremo en el servicio de resolución a través de la función `Register`.  El servicio de resolución almacena esta información como un registro.  Este registro contiene un identificador único \(RegistrationID\) e información de extremo \(PeerNodeAddress\) para el nodo.  
  
## Registros obsoletos y tiempo de expiración  
 Lo ideal es que, cuando un nodo deja la malla, llame a la función `Unregister`, que hace que el servicio de resolución quite la entrada de registro.  A veces, los nodos se cierran o dejan de estar accesibles antes de llamar a `Unregister`, dejando un registro obsoleto.  
  
 Los registros obsoletos del servicio de resolución pueden producir errores de conexión.  Si un nodo que intenta conectar con una malla recibe información de conexión obsoleta del servicio de resolución, puede tardar mucho más tiempo en unirse a la malla correctamente.  Los registros obsoletos también consumen memoria.  Si no se dispone de un proceso de limpieza eficaz, la memoria caché utilizada para almacenar los registros podría desbordarse y bloquear el servicio de resolución.  
  
 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> marca cada registro con un tiempo de expiración \(DateTime\) y almacena esa información como parte del registro.  El servicio utiliza el tiempo de expiración para identificar los registros obsoletos.  Las implementaciones personalizadas deberían hacer algo similar.  
  
## RefreshInterval y CleanupInterval  
 La propiedad `RefreshInterval` de <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> define el tiempo durante el cual los registros siguen siendo válidos en la tabla de búsqueda del registro del servicio.  Cuando ha transcurrido el tiempo indicado en esta propiedad para un registro determinado, ese registro se vuelve obsoleto y se marca para su eliminación.  
  
 La propiedad `CleanupInterval` de <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> indica al servicio con qué frecuencia debe buscar y eliminar los registros obsoletos.  `CleanupInterval` se debería establecer en un valor mayor o igual que el valor de `RefreshInterval` establecido en el servicio.  
  
 Para implementar su propio servicio de resolución, necesita escribir una función de mantenimiento para quitar los registros obsoletos.  Existen varias formas de hacerlo:  
  
-   **Mantenimiento periódico**: establezca un temporizador que se active periódicamente y examine el almacén de datos para eliminar los registros antiguos.  <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> usa este método.  
  
-   **Eliminación pasiva**: en lugar de buscar los registros obsoletos activamente a intervalos regulares, puede identificar y eliminar los registros obsoletos cuando el servicio ya esté realizando otra función.  Existe la posibilidad de que se reduzca el tiempo de respuesta para las solicitudes de los clientes de resolución, pero evita la necesidad de disponer de un temporizador y puede ser más eficaz si se espera que pocos nodos terminen sin llamar a `Unregister`.  
  
## RegistrationLifetime y Refresh  
 Cuando un nodo se registra con un servicio de resolución, recibe un objeto <xref:System.ServiceModel.PeerResolvers.RegisterResponseInfo> desde el servicio.  Este objeto tiene una propiedad `RegistrationLifetime` que indica al nodo cuánto tiempo tiene antes de que el registro expire y el servicio de resolución lo quite.  Por ejemplo, si `RegistrationLifetime` es 2 minutos, el nodo necesita llamar a `Refresh` en menos de 2 minutos para asegurarse de que el registro se mantiene actualizado y no se elimina.  Cuando el servicio de resolución recibe una solicitud `Refresh`, busca el registro y restablece el tiempo de expiración.  Refresh devuelve un objeto <xref:System.ServiceModel.PeerResolvers.RefreshResponseInfo> con una propiedad `RegistrationLifetime`.  
  
## Vea también  
 [Resoluciones del mismo nivel](../../../../docs/framework/wcf/feature-details/peer-resolvers.md)