---
title: "Seguridad de acceso del c&#243;digo y ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Seguridad de acceso del c&#243;digo y ADO.NET
.NET Framework ofrece seguridad basada en roles y seguridad de acceso del código \(CAS\); ambas se implementan utilizando una infraestructura común proporcionada por Common Language Runtime \(CLR\).  En el mundo del código no administrado, la mayoría de las aplicaciones se ejecutan mediante los permisos del usuario o de la entidad de seguridad.  Por consiguiente, los sistemas de equipos pueden resultar dañados y se pueden poner en peligro los datos privados si un usuario con un nivel elevado de privilegios ejecuta software malintencionado o que contenga errores.  
  
 El código administrado que se ejecuta en .NET Framework, sin embargo, incluye seguridad de acceso del código, que se aplica únicamente al código.  El permiso para que el código se ejecute o no depende de su origen o de otros aspectos de la identidad del código, y no solo de la identidad de la entidad de seguridad.  De esta forma, se reduce la probabilidad de que se utilice el código de manera incorrecta.  
  
## Permisos de acceso a código  
 Cuando se ejecuta el código, éste presenta evidencia de que lo evalúa el sistema de seguridad Common Language Runtime CLR.  Este tipo de evidencia normalmente contiene el origen del código, incluidos la dirección URL, el sitio, la zona y las firmas digitales que determinan la identidad del ensamblado.  
  
 CLR permite que el código realice únicamente las operaciones para las que tiene permiso.  El código puede solicitar permisos y las peticiones se aceptan en función de la directiva de seguridad que haya establecido un administrador.  
  
> [!NOTE]
>  El código que se ejecuta en el CLR no se puede conceder permisos a sí mismo.  Por ejemplo, el código puede solicitar y que se le asignen menos permisos de los que concede una directiva de seguridad, pero no se le concederán más permisos.  A la hora de conceder permisos, comience sin ningún permiso y agregue los mínimos permisos necesarios para la tarea concreta que se lleva a cabo.  Si se comienza con todos los permisos y posteriormente se deniegan permisos de forma individual, se obtienen aplicaciones poco seguras que pueden contener vulnerabilidades de seguridad no intencionadas debido a la concesión de más permisos de los que son necesarios.  Para obtener más información, vea [NIB: Configuring Security Policy](http://msdn.microsoft.com/es-es/0f130bcd-1bba-4346-b231-0bcca7dab1a4) y [NIB: Security Policy Management](http://msdn.microsoft.com/es-es/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9).  
  
 Hay tres tipos de permisos de acceso a código:  
  
-   Los `Code access permissions` derivan de la clase <xref:System.Security.CodeAccessPermission>.  Se requieren permisos para tener acceso a recursos protegidos, como archivos y variables de entorno, y para realizar operaciones protegidas, como el acceso a código no administrado.  
  
-   Los `Identity permissions` representan características que identifican un ensamblado.  Los permisos se conceden al ensamblado en función de la evidencia, que puede incluir elementos como una firma digital o el origen del código.  Los permisos de identidad también derivan de la clase base <xref:System.Security.CodeAccessPermission>.  
  
-   Los `Role-based security permissions` se basan en el hecho de si una entidad de seguridad tiene una identidad especificada o si es miembro de una función especificada.  La clase <xref:System.Security.Permissions.PrincipalPermission> permite comprobar los permisos declarativos e imperativos con la entidad de seguridad activa.  
  
 Para determinar si el código tiene autorización para el acceso a un recurso o para ejecutar una operación, el sistema de seguridad en tiempo de ejecución atraviesa la pila de llamadas y compara los permisos concedidos a cada llamador con el permiso que se exige.  Si algún llamador de la pila de llamadas no tiene el permiso exigido, se iniciará clase <xref:System.Security.SecurityException> y se rechazará el acceso.  
  
### Solicitar permisos  
 La finalidad de solicitar permisos es informar al motor en tiempo de ejecución de los permisos que necesita la aplicación para ejecutarse y garantizar que solo recibe los permisos que realmente necesita.  Por ejemplo, si la aplicación necesita acceso de escritura al disco local, requiere <xref:System.Security.Permissions.FileIOPermission>.  Si este permiso no se ha concedido, se producirán errores en la aplicación al intentar escribir en el disco.  Sin embargo, si la aplicación solicita `FileIOPermission` y el permiso no se concede, generará la excepción al comienzo y no se cargará.  
  
 En un escenario donde la aplicación solo necesita leer datos del disco, puede solicitar que nunca se le concedan permisos de escritura.  En el caso de se produzca un error o un ataque malintencionado, el código no podrá dañar los datos con los que trabaja.  Para obtener más información, consulta [NIB: Requesting Permissions](http://msdn.microsoft.com/es-es/0447c49d-8cba-45e4-862c-ff0b59bebdc2).  
  
## Seguridad basada en roles y CAS  
 La implementación de la seguridad basada en roles y de la seguridad de acceso del código \(CAS\) mejora la seguridad global de la aplicación.  La seguridad basada en roles se puede basar en una cuenta de Windows o en una identidad personalizada, de forma que la información sobre la entidad de seguridad esté disponible en el subproceso actual.  Además, a menudo se requiere a la aplicaciones que proporcionen acceso a datos o recursos basándose en credenciales proporcionadas por el usuario.  Normalmente, dichas aplicaciones comprueban la función de un usuario y proporcionan acceso a los recursos basándose en dichos roles.  
  
 La seguridad basada en roles permite que un componente identifique los usuarios actuales y sus roles asociados en tiempo de ejecución.  Esta información se asigna a continuación mediante una directiva CAS para determinar el conjunto de permisos que se conceden en tiempo de ejecución.  En un dominio de aplicación especificado, el host puede cambiar la directiva de seguridad predeterminada basada en roles y establecer una entidad de seguridad que represente a un usuario y a los roles asociados al usuario.  
  
 CLR usa permisos para implementar su mecanismo a fin de aplicar restricciones en el código administrado.  Los permisos de seguridad basada en roles proporcionan un mecanismo para descubrir si un usuario \(o el agente que actúa en su nombre\) tiene una identidad concreta o es miembro de una función especificada.  Para obtener más información, consulta [Security Permissions](http://msdn.microsoft.com/es-es/b03757b4-e926-4196-b738-3733ced2bda0).  
  
 En función del tipo de aplicación que cree, deberá considerar también la posibilidad de implementar permisos basados en roles en la base de datos.  Para obtener más información sobre la seguridad basada en roles en SQL Server, vea [Seguridad en SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md).  
  
## Ensamblados  
 Los ensamblados componen la unidad fundamental de implementación, control de versiones, reutilización, ámbito de activación y permisos de seguridad en una aplicación de .NET Framework.  Un ensamblado proporciona una colección de tipos y recursos creados para funcionar en conjunto y formar una unidad lógica de funcionalidad.  En CLR, un tipo no existe si no es en el contexto de un ensamblado.  Para obtener más información sobre la creación e implementación de ensamblados, vea [Programar con ensamblados](../../../../docs/framework/app-domains/programming-with-assemblies.md).  
  
### Ensamblados con nombre seguro  
 Un nombre seguro, o firma digital, consta de la identidad del ensamblado, que incluye su nombre de texto sencillo, el número de versión, la información de referencia cultural \(si se proporciona\), así como una clave pública y una firma digital.  La firma digital se genera a partir de un archivo de ensamblado que usa la clave privada correspondiente.  El archivo de ensamblado contiene el manifiesto del ensamblado, que contiene los nombres y códigos hash de todos los archivos que forman el ensamblado.  
  
 La asignación de un nombre seguro al ensamblado proporciona a una aplicación o a un componente una identidad única que puede usar otro software para referirse a ella de manera explícita.  La asignación de nombres seguros protege a los ensamblados de la suplantación por parte de un ensamblado que contenga código malintencionado.  También garantiza la coherencia entre las diferentes versiones de un componente.  Debe usar nombres seguros en los ensamblados que se van a implementar en la caché global de ensamblados \(GAC\).  Para obtener más información, consulta [Crear y utilizar ensamblados con nombre seguro](../../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md).  
  
## Confianza parcial en ADO.NET 2.0  
 En ADO.NET 2.0, se pueden ejecutar los proveedores de datos .NET Framework para SQL Server, OLE DB, ODBC y para Oracle en entornos de confianza parcial.  En versiones anteriores de .NET Framework, solo se admitía el uso de <xref:System.Data.SqlClient> en aplicaciones que no fuesen de plena confianza.  
  
 Una aplicación de confianza parcial que utilice el proveedor de SQL Server debe tener como mínimo permisos de ejecución y <xref:System.Data.SqlClient.SqlClientPermission>.  
  
### Propiedades de atributos de permiso de confianza parcial  
 En las situaciones de confianza parcial, se puede aplicar <xref:System.Data.SqlClient.SqlClientPermissionAttribute> a los miembros a fin de restringir aún más las capacidades disponibles para el proveedor de datos .NET Framework para SQL Server.  
  
 En la siguiente tabla se muestran y se describen las propiedades <xref:System.Data.SqlClient.SqlClientPermissionAttribute> disponibles:  
  
|Propiedad de atributo de permiso|Descripción|  
|--------------------------------------|-----------------|  
|`Action`|Obtiene o establece una acción de seguridad.  Se hereda de <xref:System.Security.Permissions.SecurityAttribute>.|  
|`AllowBlankPassword`|Habilita o deshabilita el uso de una contraseña en blanco en una cadena de conexión.  Los valores válidos son `true` \(para habilitar el uso de contraseñas en blanco\) y `false` \(para deshabilitarlo\).  Se hereda de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`ConnectionString`|Identifica una cadena de conexión admitida.  Se pueden identificar varias cadenas de conexión. **Note:**  No incluya un id. de usuario o una contraseña en la cadena de conexión.  En esta versión no se pueden modificar las restricciones de las cadenas de conexión mediante la herramienta Configuración de .NET Framework. <br /><br /> Se hereda de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictions`|Identifica qué parámetros de las cadenas de conexión están permitidos o no lo están.  Los parámetros de las cadenas de conexión se identifican con el formato *\<nombre de parámetro\=*.  Se pueden especificar varios parámetros separados por punto y coma \(;\). **Note:**  Si no especifica `KeyRestrictions`, pero establece la propiedad `KeyRestrictionBehavior` en `AllowOnly` o `PreventUsage`, no se permitirán parámetros de cadena de conexión adicionales.  Se hereda de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictionBehavior`|Identifica los parámetros de cadenas de conexión como los únicos parámetros adicionales permitidos \(`AllowOnly`\) o bien identifica los parámetros adicionales no permitidos \(`PreventUsage`\).  `AllowOnly` es el valor predeterminado.  Se hereda de <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`TypeID`|Obtiene un identificador único para el atributo cuando se implementa en una clase derivada.  Se hereda de <xref:System.Attribute>.|  
|`Unrestricted`|Indica si se declaran permisos protegidos para el origen.  Se hereda de <xref:System.Security.Permissions.SecurityAttribute>.|  
  
#### Sintaxis de ConnectionString  
 En el siguiente ejemplo se muestra cómo se utiliza el elemento `connectionStrings` de un archivo de configuración para permitir únicamente el uso de una determinada cadena de conexión.  Para obtener más información sobre el almacenamiento de cadenas de conexión en archivos de configuración y recuperación de las mismas, vea [Cadenas de conexión](../../../../docs/framework/data/adonet/connection-strings.md).  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### Sintaxis de KeyRestrictions  
 En el ejemplo siguiente se habilita la misma cadena de conexión, se habilita el uso de las opciones de cadena de conexión `Encrypt` y `Packet``Size`, pero se restringe el uso de otras opciones de cadena de conexión.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### Sintaxis de KeyRestrictionBehavior con PreventUsage  
 En el ejemplo siguiente se habilita la misma cadena de conexión y se permiten todos los demás parámetros de conexión, excepto `User Id`, `Password` y `Persist Security Info`.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### Sintaxis de KeyRestrictionBehavior con AllowOnly  
 En el ejemplo siguiente se habilitan dos cadenas de conexión que contienen los parámetros `Initial Catalog`, `Connection Timeout`, `Encrypt` y `Packet Size`.  El resto de los parámetros de cadenas de conexión están restringidos.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"   
    connectionString="Data Source=SqlServer2;Initial   
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### Habilitar confianza parcial con un conjunto de permisos personalizados  
 Para habilitar el uso de permisos <xref:System.Data.SqlClient> para una zona determinada, un administrador del sistema debe crear un conjunto de permisos personalizados y establecerlo como el conjunto de permisos de dicha zona.  Los conjuntos de permisos predeterminados, como `LocalIntranet`, no se pueden modificar.  Por ejemplo, para incluir permisos <xref:System.Data.SqlClient> para un código que tiene una <xref:System.Security.Policy.Zone> de `LocalIntranet`, un administrador del sistema tendría que copiar el conjunto de permisos para `LocalIntranet`, cambiar el nombre a "CustomLocalIntranet", agregar los permisos <xref:System.Data.SqlClient>, importar el conjunto de permisos CustomLocalIntranet mediante [Caspol.exe \(Code Access Security Policy Tool\)](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md) y establecer el conjunto de permisos de `LocalIntranet_Zone` en CustomLocalIntranet.  
  
### Conjunto de permisos de ejemplo  
 A continuación se muestra un ejemplo de un conjunto de permisos para el proveedor de datos .NET Framework para SQL Server en un escenario que no es de plena confianza.  Para obtener información sobre la creación de conjuntos de permisos, vea [NIB:Configuring Permission Sets Using Caspol.exe](http://msdn.microsoft.com/es-es/94e2625e-21ad-4038-af36-6d1f9df40a57).  
  
```  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"   
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## Comprobar el acceso a código de ADO.NET mediante permisos de seguridad  
 En las situaciones de confianza parcial, puede solicitar privilegios de seguridad de acceso del código para determinados métodos en el código mediante la especificación de <xref:System.Data.SqlClient.SqlClientPermissionAttribute>.  Si la directiva de seguridad restringida no permite el privilegio, se inicia una excepción antes de ejecutarse el código.  Para obtener más información sobre directivas de seguridad, vea [NIB: Security Policy Management](http://msdn.microsoft.com/es-es/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9) y [NIB: Security Policy Best Practices](http://msdn.microsoft.com/es-es/d49bc4d5-efb7-4caa-a2fe-e4d3cec63c05).  
  
### Ejemplo  
 En el siguiente ejemplo se muestra cómo escribir código que requiera una determinada cadena de conexión.  Simula la denegación de permisos sin restricciones para <xref:System.Data.SqlClient>, que podría implementar un administrador del sistema en una situación real mediante una directiva de seguridad CAS.  
  
> [!IMPORTANT]
>  Al diseñar permisos de seguridad CAS en ADO.NET, el procedimiento correcto es comenzar con el caso más restrictivo \(sin ningún permiso\) y agregar a continuación los permisos específicos necesarios para la tarea determinada que el código debe realizar.  El patrón opuesto, que comienza con todos los permisos y deniega a continuación un permiso concreto, no es seguro puesto que existen muchas formas de expresar la misma cadena de conexión.  Por ejemplo, si comienza con todos los permisos y después intenta denegar el uso de la cadena de conexión "servidor\=unServidor", la cadena "servidor\=unServidor.miEmpresa.com" seguirá obteniendo permiso.  Al comenzar siempre por no conceder ningún permiso, se reduce la posibilidad de que haya lagunas en el conjunto de permisos.  
  
 En el siguiente código se muestra cómo `SqlClient` realiza la petición de seguridad, que inicia <xref:System.Security.SecurityException> si los permisos de seguridad CAS adecuados no se encuentran en su lugar.  El resultado <xref:System.Security.SecurityException> se muestra en la ventana de la consola.  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 Debe poder ver este resultado en la ventana de la consola:  
  
```  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,   
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## Interoperabilidad de código no administrado  
 El código que se ejecuta fuera de CLR se denomina código no administrado.  Por lo tanto, los mecanismos de seguridad como CAS no se pueden aplicar en código no administrado.  Los componentes COM, las interfaces ActiveX y las funciones de la API de Win32 son ejemplos de código no administrado.  Cuando se ejecuta código no administrado se aplican consideraciones de seguridad especiales, de forma que no se ponga en peligro la seguridad global de la aplicación.  Para obtener más información, consulta [Interoperating with Unmanaged Code](../../../../docs/framework/interop/index.md).  
  
 .NET Framework también es compatible con versiones anteriores de componentes COM existentes mediante el acceso a través de la interoperabilidad COM.  Se pueden incluir componentes COM en una aplicación de .NET Framework usando las herramientas de la interoperabilidad COM para importar los tipos COM necesarios.  Una vez que se han importado, los tipos COM están listos para su uso.  La interoperabilidad COM también permite que los clientes COM tengan acceso a código administrado mediante la exportación de metadatos de ensamblado a una biblioteca de tipos y mediante el registro del componente administrado como un componente COM.  Para obtener más información, consulta [Advanced COM Interoperability](http://msdn.microsoft.com/es-es/3ada36e5-2390-4d70-b490-6ad8de92f2fb).  
  
## Vea también  
 [Proteger aplicaciones de ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Seguridad del código nativo y del código de .NET Framework](http://msdn.microsoft.com/es-es/bd61be84-c143-409a-a75a-44253724f784)   
 [Code Access Security](http://msdn.microsoft.com/es-es/23a20143-241d-4fe5-9d9f-3933fd594c03)   
 [Role\-Based Security](http://msdn.microsoft.com/es-es/239442e3-5be4-4203-b7fd-793baffea803)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)