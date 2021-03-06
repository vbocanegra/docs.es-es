---
title: "How to: Create a Windows Forms Application from the Command Line | Microsoft Docs"
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
  - "Windows Forms, application development from command line"
  - "Windows Forms, getting started"
  - "Windows Forms, creating basic form"
ms.assetid: 45ad3f8b-1c26-4c9f-91a9-3bb0759a47a4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Create a Windows Forms Application from the Command Line
Los procedimientos siguientes describen los pasos básicos que debe seguir para crear y ejecutar una aplicación de Windows Forms desde la línea de comandos.  Visual Studio es altamente compatible con estos procedimientos.  Consulte también [Tutorial: Crear Windows Forms sencillos](http://msdn.microsoft.com/library/z9w2f38k%20\(v=vs.110\)).  
  
## Procedimiento  
  
#### Para crear el formulario  
  
1.  En un archivo de código vacío, escriba las siguientes instrucciones import o using:  
  
     [!code-csharp[System.Windows.Forms.BasicForm#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BasicForm#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#2)]  
  
2.  Declare una clase llamada `Form1` que hereda de la clase Form.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BasicForm#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#3)]  
  
3.  Cree un constructor predeterminado para `Form1`.  
  
     Agregará más código al constructor en un procedimiento posterior.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.BasicForm#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#4)]  
  
4.  Agregue un método `Main` a la clase.  
  
    1.  Aplique el <xref:System.STAThreadAttribute> al método `Main` para especificar que la aplicación de Windows Forms es un contenedor uniproceso.  
  
    2.  Llame a <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> para dar el aspecto de Windows XP a su aplicación.  
  
    3.  Cree una instancia del formulario y ejecútela.  
  
     [!code-csharp[System.Windows.Forms.BasicForm#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.BasicForm#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#5)]  
  
#### Para compilar y ejecutar la aplicación  
  
1.  En el símbolo del sistema de .NET Framework, vaya al directorio donde creó la clase `Form1`.  
  
2.  Compile el formulario.  
  
    -   Si está usando C\#, escriba: `csc form1.cs`  
  
         `O bien`  
  
    -   Si está usando Visual Basic, escriba: `vbc form1.vb /r:system.dll,system.drawing.dll,system.windows.forms.dll`  
  
3.  En el símbolo del sistema, escriba: `Form1.exe`  
  
## Agregar un control y controlar un evento  
 Los pasos del procedimiento anterior muestran cómo crear un Windows Form básico que se compila y se ejecuta.  El procedimiento siguiente mostrará cómo crear y agregar un control al formulario y cómo controlar un evento del control.  Para obtener más información acerca de los controles que puede agregar a Windows Forms, consulte [Controles de Windows Forms](../../../docs/framework/winforms/controls/index.md).  
  
 Además de comprender cómo se crean las aplicaciones de Windows Forms, debe conocer la programación basada en eventos y cómo controlar la entrada de datos del usuario.  Para obtener más información, consulte [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md) y [Controlar la introducción de datos por el usuario](../../../docs/framework/winforms/controls/handling-user-input.md)  
  
#### Para declarar un control de botón y controlar su evento de clic  
  
1.  Declare un control de botón llamado `button1`.  
  
2.  En el constructor, cree el botón y establezca sus propiedades <xref:System.Windows.Forms.Control.Size%2A>, <xref:System.Windows.Forms.Control.Location%2A> y <xref:System.Windows.Forms.Control.Text%2A>.  
  
3.  Agregue el botón al formulario.  
  
     En el ejemplo de código siguiente se muestra cómo declarar el control de botón.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.FormWithButton#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#2)]  
  
4.  Cree un método para controlar los eventos <xref:System.Windows.Forms.Control.Click> del botón.  
  
5.  En el controlador de eventos de clic, muestre un <xref:System.Windows.Forms.MessageBox> con el mensaje "Hello World".  
  
     En el ejemplo de código siguiente se muestra cómo controlar el evento de clic del control de botón.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.FormWithButton#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#3)]  
  
6.  Asocie el evento <xref:System.Windows.Forms.Control.Click> con el método que se ha creado.  
  
     En el ejemplo de código siguiente se muestra cómo asociar el evento con el método.  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.FormWithButton#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#4)]  
  
7.  Compile y ejecute la aplicación tal y como se describe en el procedimiento anterior.  
  
## Ejemplo  
 El ejemplo de código siguiente es el ejemplo completo de los procedimientos anteriores.  
  
 [!code-csharp[System.Windows.Forms.FormWithButton#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.FormWithButton#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#1)]  
  
## Compilar el código  
  
-   Para compilar el código, siga las instrucciones del procedimiento siguiente que describen cómo compilar y ejecutar la aplicación.  
  
## Vea también  
 <xref:System.Windows.Forms.Form>   
 <xref:System.Windows.Forms.Control>   
 [Changing the Appearance of Windows Forms](../../../docs/framework/winforms/changing-the-appearance-of-windows-forms.md)   
 [Enhancing Windows Forms Applications](../../../docs/framework/winforms/advanced/index.md)   
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)