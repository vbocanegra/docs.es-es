---
title: "Encoding and Windows Forms Globalization | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ListView control [Windows Forms], lack of Unicode support"
  - "DateTimePicker control [Windows Forms], lack of Unicode support"
  - "TrackBar control [Windows Forms], lack of Unicode support"
  - "ImageList component [Windows Forms], lack of Unicode support"
  - "Unicode [Windows Forms]"
  - "ToolBar control [Windows Forms], lack of Unicode support"
  - "international applications [Windows Forms], character display"
  - "StatusBar control [Windows Forms], lack of Unicode support"
  - "MonthCalendar control [Windows Forms], lack of Unicode support"
  - "international characters"
  - "TabControl control [Windows Forms], lack of Unicode support"
  - "Windows Forms, encoding"
  - "TreeView control [Windows Forms], lack of Unicode support"
  - "ProgressBar control [Windows Forms], Unicode-enabled forms"
  - "localization [Windows Forms], character sets"
  - "globalization [Windows Forms], character sets"
ms.assetid: 22e8965d-a712-42b3-8167-3ee346bd70f9
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Encoding and Windows Forms Globalization
Las aplicaciones de Windows Forms están totalmente habilitadas para Unicode, lo que significa que cada carácter se representa mediante un número único, independientemente de la plataforma, el programa o el idioma.  Para obtener más información sobre Unicode, consulte el [sitio web del consorcio Unicode](http://www.unicode.org).  
  
## Ventajas de Unicode  
 Entre las ventajas de los formularios habilitados para Unicode se incluye la capacidad de trabajar con scripts que son solo Unicode, como el Hindi.  Además, puede usar varios idiomas en un único formulario.  En Unicode, todos los caracteres tienen una longitud de dos bytes, por lo que no es necesario realizar ningún esfuerzo especial para representar los caracteres de doble byte.  También puede escribir un único conjunto de código que funcionará en todas las plataformas.  Se trata de un cambio respecto a versiones anteriores de [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], en las que tenía que escribir código diferente para distintas plataformas, como Windows NT y [!INCLUDE[win98](../../../../includes/win98-md.md)].  
  
 Sin embargo, ciertos controles no admiten Unicode en [!INCLUDE[win98](../../../../includes/win98-md.md)] y Windows Millennium Edition.  Estos controles, que heredan todos del control común, procesarán los datos con las páginas de códigos de Windows, como [!INCLUDE[vcpransi](../../../../includes/vcpransi-md.md)].  Estos controles son: <xref:System.Windows.Forms.TabControl>, <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.DateTimePicker>, <xref:System.Windows.Forms.MonthCalendar>, <xref:System.Windows.Forms.TrackBar>, <xref:System.Windows.Forms.ProgressBar>, <xref:System.Windows.Forms.ImageList>, <xref:System.Windows.Forms.ToolBar> y <xref:System.Windows.Forms.StatusBar>.  Como resultado, no puede mostrar datos Unicode en estos controles en las plataformas indicadas.  Por ejemplo, no puede mostrar caracteres japoneses en un sistema operativo [!INCLUDE[win98](../../../../includes/win98-md.md)] en inglés.  
  
 Para obtener alternativas con reconocimiento de Unicode a los controles <xref:System.Windows.Forms.ToolBar> y <xref:System.Windows.Forms.StatusBar>, use los controles <xref:System.Windows.Forms.ToolStrip> y <xref:System.Windows.Forms.StatusStrip>, que sustituyen a los controles más antiguos.  Para mantener una apariencia similar entre los elementos visuales de la aplicación, use el control <xref:System.Windows.Forms.MenuStrip> para representar menús en lugar de <xref:System.Windows.Forms.MainMenu>.  Igual que <xref:System.Windows.Forms.ToolStrip> y <xref:System.Windows.Forms.StatusStrip>, <xref:System.Windows.Forms.MenuStrip> también puede procesar y mostrar caracteres Unicode.  
  
## Vea también  
 [Globalizing Windows Forms](../../../../docs/framework/winforms/advanced/globalizing-windows-forms.md)