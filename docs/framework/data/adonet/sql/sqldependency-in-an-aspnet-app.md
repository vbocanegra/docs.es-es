---
title: "SqlDependency en una aplicaci&#243;n ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# SqlDependency en una aplicaci&#243;n ASP.NET
En el ejemplo de esta sección se muestra cómo utilizar <xref:System.Data.SqlClient.SqlDependency> de forma indirecta aprovechando el objeto <xref:System.Web.Caching.SqlCacheDependency> de ASP:NET.  El objeto <xref:System.Web.Caching.SqlCacheDependency> utiliza <xref:System.Data.SqlClient.SqlDependency> para escuchar notificaciones y de actualizar correctamente la caché.  
  
> [!NOTE]
>  En el ejemplo se parte de que las notificaciones de consulta están habilitadas mediante la ejecución de los scripts en [Habilitación de notificaciones de consulta](../../../../../docs/framework/data/adonet/sql/enabling-query-notifications.md).  
  
## Acerca de la aplicación de ejemplo  
 La aplicación de ejemplo utiliza una única página web de ASP.NET para mostrar información de producto de la base de datos **AdventureWorks** de SQL Server en un control <xref:System.Web.UI.WebControls.GridView>.  Cuando se carga la página, el código escribe la hora actual en un control <xref:System.Web.UI.WebControls.Label>.  A continuación, se define un objeto <xref:System.Web.Caching.SqlCacheDependency> y se establecen las propiedades del objeto <xref:System.Web.Caching.Cache> para almacenar los datos de la caché durante tres minutos como máximo.  Entonces el código se conecta a la base de datos y recupera los datos.  Cuando la página está cargada y la aplicación se está ejecutando, ASP.NET recuperará datos de la caché, lo cual podrá comprobar si observa que la hora de la página no cambia.  Si los datos que se supervisan cambian, ASP.NET invalida la caché y vuelve a llenar el control `GridView` con datos nuevos, actualizando la hora que se muestra en el control `Label`.  
  
## Crear la aplicación de ejemplo  
 Para crear y ejecutar la aplicación de ejemplo, siga estos pasos:  
  
1.  Cree un nuevo sitio web ASP.NET.  
  
2.  Agregue un control <xref:System.Web.UI.WebControls.Label> y <xref:System.Web.UI.WebControls.GridView> a la página Default.aspx.  
  
3.  Abra el módulo de clase de la página y agregue las siguientes directivas:  
  
    ```vb  
  
    Option Strict On  
    Option Explicit On  
  
    Imports System.Data.SqlClient  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4.  Agregue el siguiente código al evento `Page_Load` de la página:  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#1)]
     [!code-vb[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#1)]  
  
5.  Agregue dos métodos auxiliares: `GetConnectionString` y `GetSQL`.  La cadena de conexión definida utiliza seguridad integrada.  Deberá comprobar que la cuenta que utiliza dispone de los permisos de base de datos necesarios y que la base de datos de ejemplo, **AdventureWorks**, tiene habilitadas las notificaciones.  Para obtener más información, consulta [Special Considerations When Using Query Notifications](http://msdn.microsoft.com/es-es/a83c8dc8-4fb9-4ffd-a2a5-c07cf4a203c7).  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#2)]
     [!code-vb[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#2)]  
  
### Probar la aplicación  
 La aplicación almacena en caché los datos mostrados en el formulario web y los actualiza cada tres minutos si no hay ninguna actividad  Si se produce un cambio en la base de datos, la caché se actualiza inmediatamente.  Ejecute la aplicación desde Visual Studio, que carga la página en el explorador.  La hora de actualización de la caché que se muestra indica la hora de la última actualización.  Espere tres minutos y, a continuación, actualice la página, lo que dará lugar a un evento postback de datos.  Observe que la hora que se muestra en la página ha cambiado.  Si actualiza la página sin esperar los tres minutos, la hora mostrada será la misma.  
  
 A continuación, actualice los datos de la base de datos mediante un comando UPDATE deTransact\-SQL y actualice la página.  La hora que se muestra indica ahora que la caché se ha actualizado con los datos nuevos de la base de datos.  Tenga en cuenta que, aunque la caché está actualizada, la hora que se muestra en la página no cambia hasta que se produce un evento postback de datos.  
  
## Vea también  
 [Notificaciones de consulta en SQL Server](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)