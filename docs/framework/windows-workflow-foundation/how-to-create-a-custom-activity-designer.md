---
title: "C&#243;mo: Crear un dise&#241;ador de actividad personalizado | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2f3aade6-facc-44ef-9657-a407ef8b9b31
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# C&#243;mo: Crear un dise&#241;ador de actividad personalizado
Normalmente los diseñadores de actividad personalizados se implementan de forma que sus actividades asociadas admitan composición con otras actividades cuyos diseñadores se pueden colocar en la superficie de diseño con ellas.Esta funcionalidad requiere que un diseñador de actividad personalizado proporcione un "área de colocación" donde se pueda colocar una actividad arbitraria y también los medios para administrar la colección resultante de elementos en la superficie de diseño.En este tema se describe cómo crear un diseñador de actividad personalizado que contenga esta área de colocación y cómo crear un diseñador de actividad personalizado que proporcione la funcionalidad de edición necesaria para administrar la colección de elementos del diseñador.  
  
 Por lo general, los diseñadores de actividad personalizados heredan de <xref:System.Activities.Presentation.ActivityDesigner>, el tipo de diseñador de actividades base predeterminado para cualquier actividad sin un diseñador específico.Este tipo proporciona la experiencia de interactuar en tiempo de diseño con la cuadrícula de propiedades y de configurar los aspectos básicos como la administración de colores e iconos.  
  
 <xref:System.Activities.Presentation.ActivityDesigner> usa dos controles de aplicación auxiliar, <xref:System.Activities.Presentation.WorkflowItemPresenter> y <xref:System.Activities.Presentation.WorkflowItemsPresenter>, para facilitar el desarrollo de diseñadores de actividad personalizados.Administran funciones comunes como arrastrar y colocar elementos secundarios, además de la eliminación, selección y adición de esos elementos secundarios.<xref:System.Activities.Presentation.WorkflowItemPresenter> permite un único elemento de la interfaz de usuario secundario dentro del "área de colocación", mientras que <xref:System.Activities.Presentation.WorkflowItemsPresenter> puede admitir varios elementos de la interfaz de usuario, incluida funcionalidad adicional como la clasificación, el desplazamiento, la eliminación y la adición de elementos secundarios.  
  
 El otro elemento importante que se debe destacar en la implementación de un diseñador de actividad personalizado está relacionado con la forma en que las ediciones visuales se enlazan mediante el enlace de datos de [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] a la instancia almacenada en memoria de lo que se está editando en el diseñador.Esto se lleva a cabo mediante el árbol de elementos de modelo, que también es responsable de la habilitación de la notificación de cambios y del seguimiento de eventos como los cambios en los estados.  
  
 En este tema se describen dos procedimientos.  
  
1.  El primer procedimiento describe cómo crear un diseñador de actividad personalizado con una clase <xref:System.Activities.Presentation.WorkflowItemPresenter> que proporciona el área de colocación que recibe a otras actividades.Este procedimiento se basa en el ejemplo [Diseñadores compuestos personalizados \- Moderador de elementos de flujo de trabajo](../../../docs/framework/windows-workflow-foundation/samples/custom-composite-designers-workflow-item-presenter.md).  
  
2.  El segundo procedimiento describe cómo crear un diseñador de actividad personalizado con una clase <xref:System.Activities.Presentation.WorkflowItemsPresenter> que proporciona la funcionalidad necesaria para editar una colección de elementos contenidos.Este procedimiento se basa en el ejemplo [Diseñadores compuestos personalizados \- Moderador de elementos de flujo de trabajo](../../../docs/framework/windows-workflow-foundation/samples/custom-composite-designers-workflow-items-presenter.md).  
  
### Para crear un diseñador de actividad personalizado con un área de colocación mediante WorkflowItemPresenter  
  
1.  Inicie [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  
  
2.  En el menú **Archivo**, elija **Nuevo** y después seleccione **Proyecto**.  
  
     Aparece el cuadro de diálogo **Nuevo proyecto**.  
  
3.  En el panel **Plantillas instaladas**, seleccione **Windows** en la categoría de lenguaje preferido.  
  
4.  En el panel **Plantillas**, seleccione **Aplicación WPF**.  
  
5.  En el cuadro **Nombre**, escriba `UsingWorkflowItemPresenter`.  
  
6.  En el cuadro **Ubicación**, escriba el directorio en el que desea guardar el proyecto o haga clic en **Examinar** para navegar hasta él.  
  
7.  En el cuadro **Solución**, acepte el valor predeterminado.  
  
8.  Haga clic en **Aceptar**.  
  
9. Haga clic con el botón secundario en el archivo MainWindows.xaml en el **Explorador de soluciones**, seleccione **Eliminar** y confirme con **Aceptar** en el cuadro de diálogo **Microsoft Visual Studio**.  
  
10. Haga clic con el botón secundario en el proyecto UsingWorkflowItemPresenter en el **Explorador de soluciones**, seleccione **Agregar**, a continuación **Nuevo elemento…** para tener acceso al cuadro de diálogo **Agregar nuevo elemento** y seleccione la categoría **WPF** de la sección **Plantillas instaladas** de la izquierda.  
  
11. Seleccione la plantilla **Ventana \(WPF\)**, asígnele el nombre `RehostingWFDesigner` y haga clic en **Agregar**.  
  
12. Abra el archivo RehostingWFDesigner.xaml y pegue el siguiente código en él para definir la interfaz de usuario de la aplicación.  
  
    ```  
  
    <Window x:Class=" UsingWorkflowItemPresenter.RehostingWFDesigner"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
            xmlns:sys="clr-namespace:System;assembly=mscorlib"  
            Title="Window1" Height="600" Width="900">  
        <Window.Resources>  
            <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
        </Window.Resources>  
        <Grid>  
            <Grid.ColumnDefinitions>  
                <ColumnDefinition Width="2*"/>  
                <ColumnDefinition Width="7*"/>  
                <ColumnDefinition Width="3*"/>  
            </Grid.ColumnDefinitions>  
            <Border Grid.Column="0">  
                <sapt:ToolboxControl Name="Toolbox">  
                    <sapt:ToolboxCategory CategoryName="Basic">  
                        <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.Sequence  
                            </sapt:ToolboxItemWrapper.ToolName>  
                           </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.WriteLine  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.If  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.While  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                    </sapt:ToolboxCategory>  
                </sapt:ToolboxControl>  
            </Border>  
            <Border Grid.Column="1" Name="DesignerBorder"/>  
            <Border Grid.Column="2" Name="PropertyBorder"/>  
        </Grid>  
    </Window>  
  
    ```  
  
13. Para asociar un diseñador de actividad a un tipo de actividad, debe registrar ese diseñador de actividad con el almacén de metadatos.Para ello, agregue el método `RegisterMetadata` a la clase `RehostingWFDesigner`.Dentro del ámbito del método `RegisterMetadata`, cree un objeto <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder> y llame al método <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder.AddCustomAttributes%2A> para agregar los atributos a él.Llame al método <xref:System.Activities.Presentation.Metadata.MetadataStore.AddAttributeTable%2A> para agregar <xref:System.Activities.Presentation.Metadata.AttributeTable> al almacén de metadatos.El siguiente código contiene la lógica de rehospedaje para el diseñador.Registra los metadatos, coloca `SimpleNativeActivity` en el cuadro de herramientas y crea el flujo de trabajo.Coloque este código en el archivo RehostingWFDesigner.xaml.cs.  
  
    ```  
  
    using System;  
    using System.Activities.Core.Presentation;  
    using System.Activities.Presentation;  
    using System.Activities.Presentation.Metadata;  
    using System.Activities.Presentation.Toolbox;  
    using System.Activities.Statements;  
    using System.ComponentModel;  
    using System.Windows;  
  
    namespace UsingWorkflowItemPresenter  
    {  
        // Interaction logic for RehostingWFDesigner.xaml  
        public partial class RehostingWFDesigner  
        {  
            public RehostingWFDesigner()  
            {  
                InitializeComponent();  
            }  
  
            protected override void OnInitialized(EventArgs e)  
            {  
                base.OnInitialized(e);  
                // register metadata  
                (new DesignerMetadata()).Register();  
                RegisterCustomMetadata();  
                // add custom activity to toolbox  
                Toolbox.Categories.Add(new ToolboxCategory("Custom activities"));  
                Toolbox.Categories[1].Add(new ToolboxItemWrapper(typeof(SimpleNativeActivity)));  
  
                // create the workflow designer  
                WorkflowDesigner wd = new WorkflowDesigner();  
                wd.Load(new Sequence());  
                DesignerBorder.Child = wd.View;  
                PropertyBorder.Child = wd.PropertyInspectorView;  
  
            }  
  
            void RegisterCustomMetadata()  
            {  
                AttributeTableBuilder builder = new AttributeTableBuilder();  
                builder.AddCustomAttributes(typeof(SimpleNativeActivity), new DesignerAttribute(typeof(SimpleNativeDesigner)));  
                MetadataStore.AddAttributeTable(builder.CreateTable());  
            }  
        }  
    }  
  
    ```  
  
14. Haga clic con el botón secundario en el directorio Referencias en el Explorador de soluciones y seleccione **Agregar referencia…** para tener acceso al cuadro de diálogo **Agregar referencia**.  
  
15. Haga clic en la pestaña **.NET**, localice el ensamblado denominado **System.Activities.Core.Presentation**, selecciónelo y haga clic en **Aceptar**.  
  
16. Con el mismo procedimiento, agregue referencias a los siguientes ensamblados:  
  
    1.  System.Data.DataSetExtensions.dll  
  
    2.  System.Activities.Presentation.dll  
  
    3.  System.ServiceModel.Activities.dll  
  
17. Abra el archivo App.xaml y cambie el valor de StartUpUri a "RehostingWFDesigner.xaml".  
  
18. Haga clic con el botón secundario en el proyecto UsingWorkflowItemPresenter en el **Explorador de soluciones**, seleccione **Agregar**, a continuación **Nuevo elemento…** para tener acceso al cuadro de diálogo **Agregar nuevo elemento** y seleccione la categoría **Flujo de trabajo** de la sección **Plantillas instaladas** de la izquierda.  
  
19. Seleccione la plantilla **Diseñador de actividad**, asígnele el nombre `SimpleNativeDesigner` y haga clic en **Agregar**.  
  
20. Abra el archivo SimpleNativeDesigner.xaml y pegue el siguiente código en él.Observe que este código utiliza <xref:System.Activities.Presentation.ActivityDesigner> como elemento raíz y muestra cómo se usa el enlace para integrar <xref:System.Activities.Presentation.WorkflowItemPresenter> en el diseñador de forma que se pueda mostrar un tipo secundario en el diseñador de actividad compuesto.  
  
    > [!NOTE]
    >  El esquema para <xref:System.Activities.Presentation.ActivityDesigner> permite agregar únicamente un elemento secundario a la definición personalizada del diseñador de actividad; sin embargo, este elemento podría ser un `StackPanel`, `Grid` o algún otro elemento compuesto de la interfaz de usuario.  
  
    ```  
  
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemPresenter.SimpleNativeDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"  
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">  
        <sap:ActivityDesigner.Resources>  
            <DataTemplate x:Key="Collapsed">  
                <StackPanel>  
                    <TextBlock>This is the collapsed view</TextBlock>  
                </StackPanel>  
            </DataTemplate>  
            <DataTemplate x:Key="Expanded">  
                <StackPanel>  
                    <TextBlock>Custom Text</TextBlock>  
                    <sap:WorkflowItemPresenter Item="{Binding Path=ModelItem.Body, Mode=TwoWay}"  
                                            HintText="Please drop an activity here" />  
                </StackPanel>  
            </DataTemplate>  
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
                <Style.Triggers>  
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">  
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
                    </DataTrigger>  
                </Style.Triggers>  
            </Style>  
        </sap:ActivityDesigner.Resources>  
        <Grid>  
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}" />  
        </Grid>  
    </sap:ActivityDesigner>  
  
    ```  
  
21. Haga clic con el botón secundario en el proyecto UsingWorkflowItemPresenter en el **Explorador de soluciones**, seleccione **Agregar**, a continuación **Nuevo elemento…** para tener acceso al cuadro de diálogo **Agregar nuevo elemento** y seleccione la categoría **Flujo de trabajo** de la sección **Plantillas instaladas** de la izquierda.  
  
22. Seleccione la plantilla **Actividad de código**, asígnele el nombre `SimpleNativeActivity` y haga clic en **Agregar**.  
  
23. Implemente la clase `SimpleNativeActivity` registrando el siguiente código en el archivo SimpleNativeActivity.cs.  
  
    ```  
  
    using System.Activities;  
  
    namespace UsingWorkflowItemPresenter  
    {  
        public sealed class SimpleNativeActivity : NativeActivity  
        {  
            // this property contains an activity that will be scheduled in the execute method  
    // the WorkflowItemPresenter in the designer is bound to this to enable editing  
    // of the value  
            public Activity Body { get; set; }  
  
            protected override void CacheMetadata(NativeActivityMetadata metadata)  
            {  
               metadata.AddChild(Body);  
               base.CacheMetadata(metadata);  
  
            }  
  
            protected override void Execute(NativeActivityContext context)  
            {  
                context.ScheduleActivity(Body);  
            }  
        }  
    }  
  
    ```  
  
24. En el menú **Compilar**, seleccione **Compilar solución**.  
  
25. Seleccione **Iniciar sin depurar** en el menú **Depurar** para abrir la ventana del diseño personalizado rehospedado.  
  
### Para crear un diseñador de actividad personalizado mediante WorkflowItemsPresenter  
  
1.  El procedimiento para el segundo diseñador de actividad personalizado es paralelo al primero con algunas modificaciones; la primera consiste en asignar a la segunda aplicación el nombre `UsingWorkflowItemsPresenter`.Esta aplicación tampoco define una nueva actividad personalizada.  
  
2.  Las diferencias clave se encuentran en los archivos CustomParallelDesigner.xaml y RehostingWFDesigner.xaml.cs.A continuación se indica el código del archivo CustomParallelDesigner.xaml que define la interfaz de usuario.  
  
    ```  
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemsPresenter.CustomParallelDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"  
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">  
        <sap:ActivityDesigner.Resources>  
            <DataTemplate x:Key="Collapsed">  
                <TextBlock>This is the Collapsed View</TextBlock>  
            </DataTemplate>  
            <DataTemplate x:Key="Expanded">  
                <StackPanel>  
                    <TextBlock HorizontalAlignment="Center">This is the</TextBlock>  
                    <TextBlock HorizontalAlignment="Center">extended view</TextBlock>  
                    <sap:WorkflowItemsPresenter HintText="Drop Activities Here"  
                                        Items="{Binding Path=ModelItem.Branches}">  
                        <sap:WorkflowItemsPresenter.SpacerTemplate>  
                            <DataTemplate>  
                                <Ellipse Width="10" Height="10" Fill="Black"/>  
                            </DataTemplate>  
                        </sap:WorkflowItemsPresenter.SpacerTemplate>  
                        <sap:WorkflowItemsPresenter.ItemsPanel>  
                            <ItemsPanelTemplate>  
                                <StackPanel Orientation="Horizontal"/>  
                            </ItemsPanelTemplate>  
                        </sap:WorkflowItemsPresenter.ItemsPanel>  
                    </sap:WorkflowItemsPresenter>  
                </StackPanel>  
            </DataTemplate>  
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
                <Style.Triggers>  
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">  
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
                    </DataTrigger>  
                </Style.Triggers>  
            </Style>  
        </sap:ActivityDesigner.Resources>  
        <Grid>  
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}"/>  
        </Grid>  
    </sap:ActivityDesigner>  
  
    ```  
  
3.  A continuación se indica el código del archivo RehostingWFDesigner.xaml.cs que proporciona la lógica de rehospedaje.  
  
    ```  
  
    using System;  
    using System.Activities.Core.Presentation;  
    using System.Activities.Presentation;  
    using System.Activities.Presentation.Metadata;  
    using System.Activities.Statements;  
    using System.ComponentModel;  
    using System.Windows;  
  
    namespaceUsingWorkflowItemsPresenter  
    {  
        public partial class RehostingWfDesigner : Window  
        {  
            public RehostingWfDesigner()  
            {  
                InitializeComponent();  
            }  
  
            protected override void OnInitialized(EventArgs e)  
            {  
                base.OnInitialized(e);  
                // register metadata  
                (new DesignerMetadata()).Register();  
                RegisterCustomMetadata();  
  
                // create the workflow designer  
                WorkflowDesigner wd = new WorkflowDesigner();  
                wd.Load(new Sequence());  
                DesignerBorder.Child = wd.View;  
                PropertyBorder.Child = wd.PropertyInspectorView;  
  
            }  
  
            void RegisterCustomMetadata()  
            {  
                AttributeTableBuilder builder = new AttributeTableBuilder();  
                builder.AddCustomAttributes(typeof(Parallel), new DesignerAttribute(typeof(CustomParallelDesigner)));  
                MetadataStore.AddAttributeTable(builder.CreateTable());  
            }  
        }  
    }  
    ```  
  
## Vea también  
 <xref:System.Activities.Presentation.ActivityDesigner>   
 <xref:System.Activities.Presentation.WorkflowItemPresenter>   
 <xref:System.Activities.Presentation.WorkflowItemsPresenter>   
 <xref:System.Activities.Presentation.WorkflowViewElement>   
 <xref:System.Activities.Presentation.Model.ModelItem>   
 [Personalizar la experiencia de diseño del flujo de trabajo](../../../docs/framework/windows-workflow-foundation//customizing-the-workflow-design-experience.md)