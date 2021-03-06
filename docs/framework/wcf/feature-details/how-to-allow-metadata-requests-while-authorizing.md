---
title: "C&#243;mo: Permitir las solicitudes de metadatos durante la autorizaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "permitir solicitudes de metadatos durante la autorización [WCF]"
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# C&#243;mo: Permitir las solicitudes de metadatos durante la autorizaci&#243;n
Durante la autorización personalizada, puede ser necesario permitir una solicitud para que se procesen los metadatos.El tema siguientes describe los pasos para validar este tipo de solicitud.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] la autorización de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], vea [Autorización](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).  
  
### Para permitir las solicitudes de los metadatos durante la autorización  
  
1.  Cree una extensión de la clase <xref:System.ServiceModel.ServiceAuthorizationManager>.  
  
2.  Invalide el método <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.El método devuelve `true` o `false` dependiendo de si se permite la autorización.La información sobre el procedimiento actual se encuentra en <xref:System.ServiceModel.OperationContext> que se pasa como un parámetro al método.  
  
3.  En la invalidación, compruebe el nombre del contrato, espacio de nombres y la acción tal como se muestra en el ejemplo siguiente.Si las condiciones son válidas, devuelva `true.`  
  
4.  Utilice el punto de extensibilidad para emplear la clase.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Cómo crear un administrador de autorización personalizado para un servicio](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md).  
  
## Ejemplo  
 En el siguiente ejemplo de código se muestra una invalidación del método <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>.  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## Vea también  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [Autorización](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [Administración de notificaciones y autorización con el modelo de identidad](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)