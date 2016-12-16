---
title: "&#39;As Any&#39; no se admite en instrucciones &#39;Declare&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30828"
  - "vbc30828"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30828"
ms.assetid: 7e5cf519-8b64-4ac5-8116-705fe26c846d
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;As Any&#39; no se admite en instrucciones &#39;Declare&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

El tipo de datos `Any` se utilizó con instrucciones `Declare` en Visual Basic 6.0 y en versiones anteriores para permitir el uso de argumentos que podían contener cualquier tipo de datos.  Sin embargo, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] admite la sobrecarga, por lo que el tipo de datos `Any` queda obsoleto.  
  
 **Identificador de error:** BC30828  
  
### Para corregir este error  
  
1.  Declare los parámetros del tipo concreto que desea usar; por ejemplo:  
  
     [!code-vb[VbVbalrStatements#95](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_1.vb)]  
  
2.  Utilice el atributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> para especificar `As Any` cuando se espera `Void*` en el procedimiento llamado.  
  
     [!code-vb[VbVbalrStatements#96](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/as-any-is-not-supported-in-declare-statements_2.vb)]  
  
## Vea también  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Tutorial: Llamar a las API de Windows](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)   
 [Declare \(Instrucción\)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Creating Prototypes in Managed Code](../Topic/Creating%20Prototypes%20in%20Managed%20Code.md)