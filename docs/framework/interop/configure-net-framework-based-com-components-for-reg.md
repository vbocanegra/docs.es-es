---
title: "How to: Configure .NET Framework-Based COM Components for Registration-Free Activation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "components [.NET Framework], manifest"
  - "application manifests [.NET Framework]"
  - "manifests [.NET Framework]"
  - "registration-free COM interop, configuring .NET-based components"
  - "activation, registration-free"
ms.assetid: 32f8b7c6-3f73-455d-8e13-9846895bd43b
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Configure .NET Framework-Based COM Components for Registration-Free Activation
La activación sin registro de los componentes de .NET Framework solo es un poco más complicada que la de los componentes COM.  La configuración requiere dos manifiestos:  
  
-   Las aplicaciones COM deben tener un manifiesto de aplicación de estilo Win32 para identificar el componente administrado.  
  
-   Los componentes de .NET Framework deben tener un manifiesto de componente con la información de activación que se necesita en tiempo de ejecución.  
  
 En este tema se describe cómo asociar un manifiesto de aplicación a una aplicación, cómo asociar un manifiesto de componente a un componente y cómo incrustar un manifiesto de componente en un ensamblado.  
  
### Para crear un manifiesto de aplicación  
  
1.  Mediante un editor XML, cree \(o modifique\) el manifiesto de aplicación propiedad de la aplicación COM que está interoperando con uno o más componentes administrados.  
  
2.  Inserte el siguiente encabezado estándar al principio del archivo:  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
     Para obtener información sobre los elementos del manifiesto y sus atributos, busque "Referencia de manifiestos de aplicación" en MSDN Library.  
  
3.  Identifique al propietario del manifiesto.  En el ejemplo siguiente, la versión 1 de `myComApp` es el propietario del archivo de manifiesto.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="msil"   
      />  
    ```  
  
4.  Identifique los ensamblados dependientes.  En el ejemplo siguiente, `myComApp` depende de `myManagedComp`.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="x86"   
                        publicKeyToken="8275b28176rcbbef"  
      />  
      <dependency>  
        <dependentAssembly>  
          <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myManagedComp"   
                        version="6.0.0.0"   
                        processorArchitecture="X86"   
                        publicKeyToken="8275b28176rcbbef"  
          />  
        </dependentAssembly>  
      </dependency>  
    </assembly>  
    ```  
  
5.  Nombre el archivo de manifiesto y guárdelo.  El nombre de un manifiesto de aplicación es el nombre del ensamblado ejecutable seguido de la extensión .manifest.  Por ejemplo, el nombre del archivo de manifiesto de la aplicación de myComApp.exe es myComApp.exe.manifest.  
  
 El manifiesto de aplicación se puede instalar en el mismo directorio que la aplicación COM.  Opcionalmente, se puede agregar como recurso al archivo .exe de la aplicación.  Para obtener más información, busque "Ensamblados en paralelo" en MSDN Library.  
  
#### Para crear un manifiesto de componente  
  
1.  Mediante un editor XML, cree un manifiesto de componente para describir el ensamblado administrado.  
  
2.  Inserte el siguiente encabezado estándar al principio del archivo:  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
3.  Identifique al propietario del archivo.  El elemento `<assemblyIdentity>` del elemento `<dependentAssembly>` del archivo del manifiesto de aplicación debe coincidir con el del manifiesto del componente.  En el ejemplo siguiente, la versión 1.2.3.4 de `myManagedComp` es el propietario del archivo de manifiesto.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4"  
                        publicKeyToken="8275b28176rcbbef"  
                        processorArchitecture="msil"  
           />  
    ```  
  
4.  Identifique cada clase del ensamblado.  Use el elemento `<clrClass>` para identificar cada clase del ensamblado administrado de manera única.  El elemento, que es un subelemento del elemento `<assembly>`, tiene los atributos que se describen en la tabla siguiente.  
  
    |Atributo|Descripción|Necesario|  
    |--------------|-----------------|---------------|  
    |`clsid`|El identificador que especifica la clase que ha de ser activada.|Sí|  
    |`description`|Cadena que informa al usuario sobre el componente.  De manera predeterminada, es una cadena vacía.|No|  
    |`name`|Cadena que representa la clase administrada.|Sí|  
    |`progid`|Identificador que hay que usar para la activación del enlace en tiempo de ejecución.|No|  
    |`threadingModel`|Modelo de subprocesos COM. El valor predeterminado es "Both".|No|  
    |`runtimeVersion`|Especifica la versión de Common Language Runtime \(CLR\) que se va a utilizar.  Si no especifica este atributo y el CLR aún no se ha cargado, el componente se cargará con la última versión de CLR instalada antes de la versión 4.  Si especifica v1.0.3705, v1.1.4322 o v2.0.50727, la versión se actualizará automáticamente a la última versión de CLR instalada antes de la versión version 4 \(normalmente, v2.0.50727\).  Si ya se ha cargado otra versión de CLR y la versión especificada se puede cargar en paralelo y en el mismo proceso, se cargará la versión especificada; de lo contrario, se usará la versión de CLR ya cargada.  Esto puede dar lugar a un error de carga.|No|  
    |`tlbid`|Identificador de la biblioteca de tipos que contiene información de tipos sobre la clase.|No|  
  
     Todos los atributos distinguen mayúsculas de minúsculas.  Se pueden obtener los CLSID, ProgIDs, modelos de subprocesos y la versión del motor en tiempo de ejecución visualizando la biblioteca de tipos exportada para el ensamblado con OLE\/COM ObjectViewer \(Oleview.exe\).  
  
     El siguiente manifiesto de componente identifica dos clases, `testClass1` y `testClass2`.  
  
    ```  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4" />  
                        publicKeyToken="8275b28176rcbbef"  
           />  
           <clrClass  
                        clsid="{65722BE6-3449-4628-ABD3-74B6864F9739}"  
                        progid="myManagedComp.testClass1"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass1"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <clrClass  
                        clsid="{367221D6-3559-3328-ABD3-45B6825F9732}"  
                        progid="myManagedComp.testClass2"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass2"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <file name="MyManagedComp.dll">  
           </file>  
    </assembly>  
    ```  
  
5.  Nombre el archivo de manifiesto y guárdelo.  El nombre de un manifiesto de componente es el nombre de la biblioteca de ensamblados seguido de la extensión .manifest.  Por ejemplo, myManagedComp.dll es myManagedComp.manifest.  
  
 Es necesario incrustar el manifiesto de componente como recurso en el ensamblado  
  
#### Para incrustar un manifiesto de componente en un ensamblado administrado  
  
1.  Cree un script de recursos que contenga la siguiente instrucción:  
  
     `RT_MANIFEST 1 myManagedComp.manifest`  
  
     En esta instrucción, `myManagedComp.manifest` es el nombre del manifiesto de componente que se incrusta.  En este ejemplo, el archivo de script se denomina `myresource.rc`.  
  
2.  Compile el script mediante el compilador de recursos de Microsoft Windows \(Rc.exe\).  En el símbolo del sistema, escriba el siguiente comando:  
  
     `rc myresource.rc`  
  
     Rc.exe produce el archivo de recursos `myresource.res`.  
  
3.  Compile de nuevo el archivo de origen del ensamblado y especifique el archivo de recursos usando la opción **\/win32res**:  
  
    ```  
    /win32res:myresource.res  
    ```  
  
     Una vez más, `myresource.res` es el nombre del archivo de recursos que contiene el recurso incrustado.  
  
## Vea también  
 [Registration\-Free COM Interop](../../../docs/framework/interop/registration-free-com-interop.md)   
 [Requirements for Registration\-Free COM Interop](http://msdn.microsoft.com/es-es/0c43bc57-eecf-4e6c-8114-490141cce4da)   
 [Configuring COM Components for Registration\-Free Activation](http://msdn.microsoft.com/es-es/bfe9b02f-d964-4784-960e-a1f94692fbfe)   
 [Tutorial de la activación sin registro de componentes .NET](http://go.microsoft.com/fwlink/?LinkId=158812)