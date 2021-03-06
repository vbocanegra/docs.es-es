---
title: "C&#243;mo: Crear un dise&#241;o de formularios Windows Forms que sea apropiado para la localizaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "diseño de aplicaciones, adaptación"
  - "adaptación, diseño de Windows Forms"
  - "TableLayoutPanel (control) [Windows Forms]"
  - "Windows Forms, adaptación"
ms.assetid: d13eff2d-701c-4b6e-8838-3885cbfb7223
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# C&#243;mo: Crear un dise&#241;o de formularios Windows Forms que sea apropiado para la localizaci&#243;n
La creación de formularios ya listos para ser localizados acelera en gran medida el desarrollo para los mercados internacionales.  Puede utilizar el control <xref:System.Windows.Forms.TableLayoutPanel> para implementar diseños que respondan correctamente cuando los controles cambien de tamaño debido a los cambios en los valores de la propiedad <xref:System.Windows.Forms.Control.Text%2A>.  
  
## Ejemplo  
 Este formulario muestra cómo crear un diseño que se ajusta proporcionalmente cuando traduce los valores de cadena mostrados a otros idiomas.  Este proceso de traducción se denomina *localización*.  Para obtener más información, consulte [Localización](../../../../docs/standard/globalization-localization/localization.md).  
  
 Visual Studio es altamente compatible con esta tarea.  Consulte también [Tutorial: Crear un diseño que ajuste las proporciones para la localización](http://msdn.microsoft.com/library/7k9fa71y\(v=vs.110\)).  
  
 [!code-csharp[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/CS/localizableform.cs#1)]
 [!code-vb[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/VB/localizableform.vb#1)]  
  
1.  [Cómo: Alinear y expandir un control en un control TableLayoutPanel](http://msdn.microsoft.com/library/ms171688\(v=vs.110\))  
  
2.  [Tutorial: Organizar controles en Windows Forms mediante FlowLayoutPanel](http://msdn.microsoft.com/library/z9w7ek2f\(v=vs.110\))  
  
3.  [Cómo: Abarcar filas y columnas en un control TableLayoutPanel](http://msdn.microsoft.com/library/ms171687\(v=vs.110\))  
  
4.  [Cómo: Editar columnas y filas en un control TableLayoutPanel](http://msdn.microsoft.com/library/ms171686\(v=vs.110\))  
  
5.  [Tutorial: Realizar tareas comunes utilizando etiquetas inteligentes en controles de Windows Forms](http://msdn.microsoft.com/library/xhz359sc\(v=vs.110\))  
  
6.  [Tutorial: Organizar controles en Windows Forms mediante TableLayoutPanel](http://msdn.microsoft.com/library/w4yc3e8c\(v=vs.110\))  
  
7.  [Tutorial: Diseñar controles de Windows Forms con relleno, márgenes y la propiedad AutoSize](http://msdn.microsoft.com/library/3z3f9e8b\(v=vs.110\))  
  
8.  [Cómo: Admitir la localización en Windows Forms mediante AutoSize y el control TableLayoutPanel](http://msdn.microsoft.com/library/1zkt8b33\(v=vs.110\))  
  
9. [Tutorial: Crear Windows Forms de entrada de datos de tamaño variable](http://msdn.microsoft.com/library/991eahec\(v=vs.110\))  
  
## Compilar el código  
 Para este ejemplo se necesita:  
  
-   Referencias a los ensamblados System, System.Data, System.Drawing y System.Windows.Forms.  
  
 Para obtener información acerca de cómo generar este ejemplo desde la línea de comandos para [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], consulte [Compilar desde la línea de comandos](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilar la línea de comandos con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  También puede compilar este ejemplo en [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] pegando el código en un nuevo proyecto.  Consulte también [Cómo: Compilar y ejecutar un ejemplo de código completo de Windows Forms en Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vea también  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 [Localización](../../../../docs/standard/globalization-localization/localization.md)