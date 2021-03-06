---
title: "C&#243;mo: Determinar las propiedades de p&#225;gina mediante el componente PageSetupDialog | Microsoft Docs"
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
  - "propiedades de página"
  - "configuración de página"
  - "PageSetupDialog (componente)"
ms.assetid: 6dae05bc-c0fd-4357-bb93-841a1631d98f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# C&#243;mo: Determinar las propiedades de p&#225;gina mediante el componente PageSetupDialog
El componente [PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md) presenta al usuario un diseño, un tamaño de papel y otras opciones de diseño de página para un documento.  
  
 Debe especificar una instancia de la clase <xref:System.Drawing.Printing.PrintDocument> \(el documento que se va a imprimir\). Además, los usuarios deben tener una impresora instalada en su equipo, ya sea de forma local o a través de una red, ya que en parte así es como determina el componente <xref:System.Windows.Forms.PageSetupDialog> las opciones de formato de página que se presentan al usuario.  
  
 Un aspecto importante a la hora de trabajar con el componente <xref:System.Windows.Forms.PageSetupDialog> es cómo interactúa con la clase <xref:System.Drawing.Printing.PageSettings>. La clase <xref:System.Drawing.Printing.PageSettings> se usa para especificar la configuración que modifica la manera en que se imprimirá una página, como la orientación del papel, el tamaño de la página o los márgenes. Cada una de estas opciones se representan como una propiedad de la clase <xref:System.Drawing.Printing.PageSettings>. La clase <xref:System.Windows.Forms.PageSetupDialog> modifica estos valores de propiedad para una instancia determinada de la clase <xref:System.Drawing.Printing.PageSettings>, que está asociada con el documento \(y que se representa como una propiedad <xref:System.Drawing.Printing.PrintDocument.DefaultPageSettings%2A>\).  
  
### Para establecer las propiedades de página con el componente PageSetupDialog  
  
1.  Use el método <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> para mostrar el cuadro de diálogo, especificando el <xref:System.Drawing.Printing.PrintDocument> que se va a usar.  
  
     En el siguiente ejemplo, el controlador de eventos <xref:System.Windows.Forms.Control.Click> del control <xref:System.Windows.Forms.Button> abre una instancia del componente <xref:System.Windows.Forms.PageSetupDialog>. Se especifica un documento existente en la propiedad <xref:System.Windows.Forms.PageSetupDialog.Document%2A> y su propiedad <xref:System.Drawing.Printing.PageSettings.Color%2A?displayProperty=fullName> se establece en `false`.  
  
     En el ejemplo se presupone que el formulario tiene un control <xref:System.Windows.Forms.Button>, un componente <xref:System.Drawing.Printing.PrintDocument> denominado `myDocument` y un componente <xref:System.Windows.Forms.PageSetupDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       'You will have to specify your own print document.  
       PageSetupDialog1.Document = myDocument  
       ' Sets the print document's color setting to false,  
       ' so that the page will not be printed in color.  
       PageSetupDialog1.Document.DefaultPageSettings.Color = False  
       PageSetupDialog1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       pageSetupDialog1.Document = myDocument;  
       // Sets the print document's color setting to false,  
       // so that the page will not be printed in color.  
       pageSetupDialog1.Document.DefaultPageSettings.Color = false;  
       pageSetupDialog1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void button1_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          pageSetupDialog1->Document = myDocument;  
          // Sets the print document's color setting to false,  
          // so that the page will not be printed in color.  
          pageSetupDialog1->Document->DefaultPageSettings->Color = false;  
          pageSetupDialog1->ShowDialog();  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] y [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Coloque el siguiente código en el constructor del formulario para registrar el controlador de eventos.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew   
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vea también  
 <xref:System.Windows.Forms.PageSetupDialog>   
 [How to: Create Standard Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)   
 [PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)