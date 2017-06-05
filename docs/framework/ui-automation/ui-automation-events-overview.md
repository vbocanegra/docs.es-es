---
title: "UI Automation Events Overview | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, providers"
  - "UI Automation, events"
  - "clients, UI Automation"
  - "events, UI Automation"
  - "providers, UI Automation"
  - "UI Automation, clients"
ms.assetid: 69eebd8b-39ed-40e7-93cc-4457c4caf746
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Events Overview
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para ver la información más reciente acerca de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: automatización de la interfaz de usuario](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 La notificación de eventos de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] es una característica clave para las tecnologías de asistencia, entre las que se incluyen lectores de pantalla y lupas. Estos clientes de automatización de la interfaz de usuario, realizan un seguimiento de los eventos que los proveedores de automatización de la interfaz de usuario generan cuando sucede algo en la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], y usan esa información para notificar a los usuarios finales.  
  
 La eficacias se mejora gracias a que las aplicaciones proveedoras son capaces de generar los eventos de manera selectiva \(en función de si hay clientes suscritos a esos eventos\) o de no generarlos en absoluto \(si no hay clientes a la escucha de eventos\).  
  
<a name="Types_of_Events"></a>   
## Tipos de eventos  
 Existen varias categorías de eventos [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]:  
  
|Evento|Descripción|  
|------------|-----------------|  
|Cambio de propiedad|Se genera cuando se produce un cambio en un patrón de control o elemento de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Por ejemplo, si un cliente necesita supervisar un control de casilla de una aplicación, se puede registrar para escuchar si se produce un evento de cambio de propiedad en la propiedad <xref:System.Windows.Automation.TogglePattern.TogglePatternInformation.ToggleState%2A>. Cuando el control de casilla se activa o desactiva, el proveedor genera el evento y el cliente puede actuar según sea necesario.|  
|Acción de elemento|Se genera cuando se produce un cambio en la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] como resultado de la actividad del usuario final o de programación, por ejemplo, cuando se hace clic en un botón o se invoca mediante <xref:System.Windows.Automation.InvokePattern>.|  
|Cambio de estructura|Se genera cuando se produce un cambio en la estructura del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. La estructura cambia cuando se muestran, se ocultan o se quitan del escritorio elementos de la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|Cambio de escritorio global|Se genera cuando se producen acciones de interés global para el cliente, por ejemplo, cuando el foco cambia de un elemento a otro o cuando se cierra una ventana.|  
  
 Algunos eventos no implican necesariamente un cambio en el estado de la UI. Por ejemplo, si el usuario se desplaza presionando la tecla TAB hasta un campo de entrada de texto y después hace clic en un botón para actualizar el campo, se genera un evento `TextChangedEvent` aunque, en realidad, el usuario no modifique el texto. Al procesar un evento, puede ser necesario que la aplicación cliente compruebe si realmente se ha producido un cambio antes de realizar cualquier acción.  
  
 Los siguientes eventos se pueden generar incluso si no cambia el estado de la UI.  
  
-   `AutomationPropertyChangedEvent` \(en función de la propiedad que cambie\)  
  
-   `ElementSelectedEvent`  
  
-   `InvalidatedEvent`  
  
-   `TextChangedEvent`  
  
<a name="UI_Automation_Event_Identifiers"></a>   
## Identificadores de eventos de automatización de la interfaz de usuario  
 Los eventos de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] se identifican mediante objetos <xref:System.Windows.Automation.AutomationEvent>. La propiedad <xref:System.Windows.Automation.AutomationIdentifier.Id%2A> contiene un valor que identifica de forma única el tipo de evento.  
  
 En la tabla siguiente se indican los valores posibles de <xref:System.Windows.Automation.AutomationIdentifier.Id%2A>, junto con el tipo que se usa para los argumentos del evento. Observe que los identificadores usados por clientes y proveedores son campos de idéntico nombre y clases diferentes.  
  
|Identificador de cliente|Identificador de proveedor|Tipo de argumentos de evento|  
|------------------------------|--------------------------------|----------------------------------|  
|<xref:System.Windows.Automation.AutomationElement.AsyncContentLoadedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|  
|<xref:System.Windows.Automation.SelectionItemPattern.ElementAddedToSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementRemovedFromSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPattern.ElementSelectedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionPattern.InvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.InvokePattern.InvokedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.LayoutInvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.MenuOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPattern.TextChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElement.ToolTipOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent?displayProperty=fullName><br /><br /> <xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.AutomationPropertyChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationPropertyChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.StructureChangedEventArgs>|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent?displayProperty=fullName>|<xref:System.Windows.Automation.WindowClosedEventArgs>|  
  
<a name="UI_Automation_Event_Arguments"></a>   
## Argumentos de eventos de automatización de la interfaz de usuario  
 Las clases siguientes encapsulan los argumentos de eventos.  
  
|Clase|Descripción|  
|-----------|-----------------|  
|<xref:System.Windows.Automation.AsyncContentLoadedEventArgs>|Contiene información sobre la carga asincrónica de contenido, como el porcentaje de carga completada.|  
|<xref:System.Windows.Automation.AutomationEventArgs>|Contiene información sobre un evento simple que no requiere datos adicionales.|  
|<xref:System.Windows.Automation.AutomationFocusChangedEventArgs>|Contiene información sobre el foco de entrada, que pasa de un elemento a otro. Los eventos de este tipo los genera el sistema de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], no los proveedores.|  
|<xref:System.Windows.Automation.AutomationPropertyChangedEventArgs>|Contiene información sobre un cambio en un valor de propiedad de un elemento o patrón de control.|  
|<xref:System.Windows.Automation.StructureChangedEventArgs>|Contiene información sobre un cambio en el árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.WindowClosedEventArgs>|Contiene información sobre el cierre de una ventana.|  
  
 Todas las clases de los argumentos de evento contienen un miembro <xref:System.Windows.Automation.AutomationEventArgs.EventId%2A>. Este identificador se encapsula en un <xref:System.Windows.Automation.AutomationEvent>.  
  
 Los proveedores obtienen los objetos <xref:System.Windows.Automation.AutomationEvent>, usados para identificar los eventos, a partir de los campos de <xref:System.Windows.Automation.AutomationElementIdentifiers> y de las clases de identificadores de patrones de control como <xref:System.Windows.Automation.DockPatternIdentifiers>. Las aplicaciones cliente obtienen los campos equivalentes a partir de campos de <xref:System.Windows.Automation.AutomationElement> y de clases de patrones de control como <xref:System.Windows.Automation.DockPattern>.  
  
 Para obtener una lista de identificadores de eventos, consulte [UI Automation Events for Clients](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md).  
  
## Vea también  
 [UI Automation Events for Clients](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md)   
 [Server\-Side UI Automation Provider Implementation](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)   
 [Subscribe to UI Automation Events](../../../docs/framework/ui-automation/subscribe-to-ui-automation-events.md)