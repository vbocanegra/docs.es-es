---
title: "Ejecutar un comando | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Ejecutar un comando
Cada proveedor de datos .NET Framework incluido en .NET Framework dispone de su propio objeto command que hereda de <xref:System.Data.Common.DbCommand>.  El proveedor de datos .NET Framework para OLE DB incluye un objeto <xref:System.Data.OleDb.OleDbCommand>, el proveedor de datos .NET Framework para SQL Server incluye un objeto <xref:System.Data.SqlClient.SqlCommand>, el proveedor de datos .NET Framework para ODBC incluye un objeto <xref:System.Data.Odbc.OdbcCommand> y el proveedor de datos .NET Framework para Oracle incluye un objeto <xref:System.Data.OracleClient.OracleCommand>.  Cada uno de estos objetos expone métodos para ejecutar comandos que se basan en el tipo de comando y el valor devuelto deseado, tal como se describe en la tabla siguiente.  
  
|Comando|Valor devuelto|  
|-------------|--------------------|  
|`ExecuteReader`|Devuelve un objeto `DataReader`.|  
|`ExecuteScalar`|Devuelve un solo valor escalar.|  
|`ExecuteNonQuery`|Ejecuta un comando que no devuelve ninguna fila.|  
|`ExecuteXMLReader`|Devuelve un valor <xref:System.Xml.XmlReader>.  Solo está disponible para un objeto `SqlCommand`.|  
  
 Cada objeto command fuertemente tipado admite también una enumeración <xref:System.Data.CommandType> que especifica cómo se interpreta una cadena de comando, tal como se describe en la tabla siguiente.  
  
|CommandType|Descripción|  
|-----------------|-----------------|  
|`Text`|Comando de SQL que define las instrucciones que se van a ejecutar en el origen de datos.|  
|`StoredProcedure`|Nombre del procedimiento almacenado.  Puede usar la propiedad `Parameters` de un comando para tener acceso a los parámetros de entrada y de salida y a los valores devueltos, independientemente del método `Execute` al que se llame.  Al usar `ExecuteReader`, no es posible el acceso a los valores devueltos y los parámetros de salida hasta que se cierra `DataReader`.|  
|`TableDirect`|Nombre de una tabla.|  
  
## Ejemplo  
 En el ejemplo de código siguiente se muestra cómo se crea un objeto <xref:System.Data.SqlClient.SqlCommand> para ejecutar un procedimiento almacenado mediante el establecimiento de sus propiedades.  Para especificar el parámetro de entrada del procedimiento almacenado se usa un objeto <xref:System.Data.SqlClient.SqlParameter>.  El comando se ejecuta con el método <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> y el resultado de <xref:System.Data.SqlClient.SqlDataReader> se muestra en la ventana de consola.  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### Solución de problemas de comandos  
 El proveedor de datos .NET Framework para SQL Server agrega contadores de rendimiento que permiten detectar problemas intermitentes relacionados con errores en la ejecución de comandos.  Para obtener más información, vea [Contadores de rendimiento](../../../../docs/framework/data/adonet/performance-counters.md).  
  
## Vea también  
 [Comandos y parámetros](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [DataAdapters y DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Working with DataReaders](http://msdn.microsoft.com/es-es/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)