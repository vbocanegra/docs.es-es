---
title: "Ilasm.exe (IL Assembler) | Microsoft Docs"
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
  - "MSIL generators"
  - "metadata, MSIL Assembler"
  - "MSIL Assembler"
  - "portable executable files, MSIL Assembler"
  - "PE files, MSIL Assembler"
  - "MSIL"
  - "Ilasm.exe"
  - "verifying MSIL performance"
ms.assetid: 4ca3a4f0-4400-47ce-8936-8e219961c76f
caps.latest.revision: 41
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 41
---
# Ilasm.exe (IL Assembler)
El Ensamblador de IL genera un archivo portable ejecutable \(PE\) a partir del lenguaje intermedio \(IL\). \(Para más información sobre IL, vea [Proceso de ejecución administrada](../../../docs/standard/managed-execution-process.md)\). Se puede ejecutar el archivo ejecutable resultante, que contiene IL y los metadatos requeridos, para determinar si IL se comporta de acuerdo con lo esperado.  
  
 Esta herramienta se instala automáticamente con Visual Studio. Para ejecutar la herramienta, utilice el Símbolo del sistema para desarrolladores \(o el Símbolo del sistema de Visual Studio en Windows 7\). Para obtener más información, consulta [Símbolos del sistema](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 En el símbolo del sistema, escriba lo siguiente:  
  
## Sintaxis  
  
```  
  
ilasm [options] filename [[options]filename...]  
```  
  
#### Parámetros  
  
|Argumento|Descripción|  
|---------------|-----------------|  
|*filename*|El nombre del archivo de código fuente con extensión .il. Este archivo consta de directivas de declaraciones de metadatos e instrucciones simbólicas de IL. Con Ilasm.exe se pueden proporcionar varios argumentos de archivo de código fuente para producir un único archivo PE. **Note:**  Asegúrese de que la última línea de código del archivo de código fuente .il tiene un espacio en blanco al final o un carácter de fin de línea.|  
  
|Opción|Descripción|  
|------------|-----------------|  
|**\/32bitpreferred**|Crea una imagen preferida de 32 bits \(PE32\).|  
|**\/alignment**\=*integer*|Establece FileAlignment en el valor especificado por *integer* en el encabezado NT opcional. Si se especifica la directiva IL .alignment en el archivo, esta opción la reemplaza.|  
|**\/appcontainer**|Genera un archivo .dll o .exe que se ejecuta en el contenedor de la aplicación de Windows, como salida.|  
|**\/arm**|Especifica Advanced RISC Machine \(ARM\) como procesador de destino.<br /><br /> Si no se especifican los bits de la imagen, el valor predeterminado es **\/32bitpreferred**.|  
|**\/base**\=*integer*|Establece ImageBase en el valor especificado por *integer* en el encabezado NT opcional. Si se especifica la directiva IL .imagebase en el archivo, esta opción la reemplaza.|  
|**\/clock**|Mide e informa de los siguientes tiempos de compilación en milisegundos para el archivo de código fuente .il especificado:<br /><br /> **Total Run**: tiempo total empleado en la ejecución de todas las operaciones específicas que se muestran a continuación.<br /><br /> **Startup**: carga y apertura del archivo.<br /><br /> **Emitting MD**: emisión de metadatos.<br /><br /> **Ref to Def Resolution**: resolución de referencias a definiciones del archivo.<br /><br /> **CEE File Generation**: generación de la imagen de archivo en memoria.<br /><br /> **PE File Writing**: escritura de la imagen en un archivo PE.|  
|**\/debug**\[\=`IMPL`&#124;`OPT`\]|Incluye información de depuración \(nombres de variables locales y argumentos, y números de línea\). Crea un archivo PDB.<br /><br /> **\/debug** sin ningún valor adicional deshabilita la optimización JIT y usa puntos de secuencia del archivo PDB.<br /><br /> **IMPL** deshabilita la optimización JIT y usa puntos de secuencia implícitos.<br /><br /> **OPT** habilita la optimización JIT y usa puntos de secuencia implícitos.|  
|**\/dll**|Genera un archivo .dll como archivo de salida.|  
|**\/enc**\=`file`|Crea deltas Editar y continuar a partir del archivo de código fuente especificado.<br /><br /> Este argumento es solo para uso académico, no se admite el uso comercial del mismo.|  
|**\/exe**|Genera un archivo ejecutable como archivo de salida. Este es el valor predeterminado.|  
|**\/flags**\=*integer*|Establece ImageFlags en el valor especificado por *integer* en el encabezado de Common Language Runtime. Si se especifica la directiva IL .corflags en el archivo, esta opción la reemplaza. Vea CorHdr.h, COMIMAGE\_FLAGS para obtener una lista de los valores válidos para *integer*.|  
|**\/fold**|Forma un solo cuerpo a partir de cuerpos de método idénticos.|  
|\/**highentropyva**|Genera un archivo ejecutable de salida que admite la selección aleatoria del diseño del espacio de direcciones \(ASLR\) de alta entropía. \(Es el valor predeterminado de **\/appcontainer**\).|  
|**\/include**\=`includePath`|Establece una ruta de acceso para buscar los archivos incluidos con `#include`.|  
|**\/itanium**|Especifica Intel Itanium como procesador de destino.<br /><br /> Si no se especifican los bits de la imagen, el valor predeterminado es **\/pe64**.|  
|**\/key:** *keyFile*|Compila *filename* con una firma segura mediante la clave privada contenida en *keyFile*.|  
|**\/key:@** *keySource*|Compila *filename* con una firma segura mediante la clave privada generada en *keySource*.|  
|**\/listing**|Genera un archivo del lista en la salida estándar. Si se omite esta opción, no se genera ningún archivo de lista.<br /><br /> Este parámetro no es compatible con .NET Framework 2.0 o posterior.|  
|**\/mdv**\=`versionString`|Establece la cadena de versión de metadatos.|  
|**\/msv**\=`major``.``minor`|Establece la versión del flujo de metadatos, donde `major` y `minor` son valores enteros.|  
|**\/noautoinherit**|Deshabilita la herencia predeterminada de <xref:System.Object> cuando no se especifica ninguna clase base.|  
|**\/nocorstub**|Suprime la generación de código auxiliar de CORExeMain.|  
|**\/nologo**|Suprime la presentación de la portada de inicio de Microsoft.|  
|**\/output:** *22*|Especifica el nombre y la extensión del archivo de salida. De forma predeterminada, el nombre del archivo de salida coincide con el nombre del primer archivo de código fuente. La extensión predeterminada es .exe. Si se especifica la opción **\/dll**, la extensión predeterminada es .dll. **Note:**  El hecho de especificar **\/output:**myfile.dll no implica que se establezca la opción **\/dll**. Si no se especifica **\/dll**, el resultado será un archivo ejecutable denominado myfile.dll.|  
|**\/optimize**|Optimiza las instrucciones largas en instrucciones cortas. Por ejemplo, `br` en `br.s`.|  
|**\/pe64**|Crea una imagen de 64 bits \(PE32\+\).<br /><br /> Si no se especifica un procesador de destino, el valor predeterminado es `/itanium`.|  
|**\/pdb**|Crea un archivo PDB sin habilitar un seguimiento de la información de depuración.|  
|**\/quiet**|Especifica el modo silencioso; no se notifica el progreso del ensamblado.|  
|**\/resource:** *file.res*|Incluye el archivo de recursos especificado con formato \*.res en el archivo .exe o .dll resultante. Solo se puede especificar un archivo .res con la opción **\/resource**.|  
|**\/ssver**\=`int`.`int`|Establece el número de versión del subsistema en el encabezado NT opcional. Para **\/appcontainer** y **\/arm** el número de versión mínimo es 6.02.|  
|**\/stack**\=`stackSize`|Establece el valor de SizeOfStackReserve en el encabezado NT opcional en `stackSize`.|  
|**\/stripreloc**|Especifica que no es necesaria ninguna reubicación base.|  
|**\/subsystem**\=*integer*|Establece subsystem en el valor especificado por *integer* en el encabezado NT opcional. Si se especifica la directiva IL .subsystem en el archivo, este comando la reemplaza. Vea winnt.h, IMAGE\_SUBSYSTEM para obtener una lista de los valores válidos para *integer*.|  
|**\/x64**|Especifica un procesador AMD de 64 bits como procesador de destino.<br /><br /> Si no se especifican los bits de la imagen, el valor predeterminado es **\/pe64**.|  
|**\/?**|Muestra las opciones y la sintaxis de los comandos para la herramienta.|  
  
> [!NOTE]
>  Ninguna de las opciones de Ilasm.exe distingue entre mayúsculas y minúsculas, y se reconocen mediante las tres primeras letras. Por ejemplo, **\/lis** equivale a **\/listing** y **\/res:**myresfile.res equivale a **\/resource:**myresfile.res. Las opciones que especifican argumentos aceptan un signo de dos puntos \(:\) o un signo igual \(\=\) como separador entre la opción y el argumento. Por ejemplo, **\/output:** *file.ext* es equivalente a **\/output\=** *file.ext*.  
  
## Comentarios  
 El Ensamblador de IL ayuda a los proveedores de herramientas a diseñar e implementar generadores IL. Mediante el uso de Ilasm.exe, los desarrolladores de herramientas y compiladores se pueden concentrar en la generación de IL y metadatos sin necesidad de preocuparse por la emisión de IL en el formato de archivo PE.  
  
 Al igual que otros compiladores orientados al runtime, como C\# y Visual Basic, Ilasm.exe no genera archivos objeto intermedios y no requiere una etapa de vinculación para crear un archivo PE.  
  
 El Ensamblador de IL puede expresar todos los metadatos existentes y las características de IL que caracterizan a los lenguajes de programación orientados al runtime. Esto permite que el código administrado escrito en cualquiera de estos lenguajes de programación se pueda expresar en el Ensamblador de IL y compilar con Ilasm.exe de forma correcta.  
  
> [!NOTE]
>  Si la última línea de código del archivo de código fuente .il no tiene espacio en blanco al final o un carácter de fin de línea, podría producirse un error en la compilación.  
  
 Se puede usar Ilasm.exe conjuntamente con su herramienta complementaria [Ildasm.exe](../../../docs/framework/tools/ildasm-exe-il-disassembler.md). Ildasm.exe toma un archivo PE que contiene código IL y crea un archivo de texto adecuado como entrada para Ilasm.exe. Esta técnica es muy útil cuando, por ejemplo, se compila código en un lenguaje de programación que no admite todos los atributos de metadatos en tiempo de ejecución. Una vez compilado el código y ejecutada la salida mediante Ildasm.exe, el archivo de texto de IL resultante se puede editar manualmente para agregar los atributos que faltan. A continuación, se puede ejecutar este archivo de texto mediante Ilasm.exe para producir un archivo ejecutable final.  
  
 También se puede usar esta técnica para generar un único archivo PE a partir de varios archivos PE generados originalmente por compiladores diferentes.  
  
> [!NOTE]
>  Actualmente no se puede usar esta técnica con archivos PE que contienen código nativo incrustado \(por ejemplo, archivos PE generados por Visual C\+\+\).  
  
 Para que este uso combinado de Ildasm.exe e Ilasm.exe sea lo más preciso posible, de forma predeterminada, el ensamblador no sustituye las codificaciones cortas por las largas que se hayan podido escribir en los códigos fuente de IL \(o que haya emitido otro compilador\). Use la opción **\/optimize** para sustituir las codificaciones cortas siempre que sea posible.  
  
> [!NOTE]
>  Ildasm.exe solo funciona en archivos existentes en disco. No funciona en archivos instalados en la caché global de ensamblados.  
  
 Para obtener más información sobre la gramática de IL, vea el archivo asmparse.grammar en [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
## Información de versión  
 A partir de [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], se puede asociar un atributo personalizado a una implementación de interfaz mediante código similar al siguiente:  
  
```  
.class interface public abstract auto ansi IMyInterface { .method public hidebysig newslot abstract virtual instance int32 method1() cil managed { } // end of method IMyInterface::method1 } // end of class IMyInterface .class public auto ansi beforefieldinit MyClass extends [mscorlib]System.Object implements IMyInterface { .interfaceimpl type IMyInterface .custom instance void [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 ) …  
  
```  
  
 A partir de [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], se puede especificar un objeto binario grande \(BLOB\) de cálculo de referencias arbitrario mediante su representación binaria sin formato, como se muestra en el código siguiente:  
  
```  
.method public hidebysig abstract virtual instance void marshal({ 38 01 02 FF }) Test(object A_1) cil managed  
  
```  
  
 Para obtener más información sobre la gramática de IL, vea el archivo asmparse.grammar en [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
## Ejemplos  
 El comando siguiente ensambla el archivo IL `myTestFile.il` y genera el archivo ejecutable `myTestFile.exe.`  
  
```  
ilasm myTestFile  
```  
  
 El comando siguiente ensambla el archivo IL `myTestFile.il` y genera el archivo .dll `myTestFile.dll`.  
  
```  
ilasm myTestFile /dll   
```  
  
 El comando siguiente ensambla el archivo IL `myTestFile.il` y genera el archivo .dll `myNewTestFile.dll`.  
  
```  
ilasm myTestFile /dll /output:myNewTestFile.dll  
```  
  
 En el siguiente ejemplo de código se muestra una aplicación muy simple que muestra "Hello World\!" en la consola.  Puede compilar este código y, a continuación, usar la herramienta [Ildasm.exe](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) para generar un archivo IL.  
  
```csharp  
using System; public class Hello { public static void Main(String[] args) { Console.WriteLine("Hello World!"); } }  
```  
  
 El siguiente ejemplo de código IL se corresponde con el ejemplo de código de C\# anterior.  Puede compilar este código en un ensamblado con la herramienta Ensamblador de IL.  Tanto el ejemplo de código IL como el de C\# muestran "Hello World\!" en la consola.  
  
```  
// Metadata version: v2.0.50215 .assembly extern mscorlib { .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4.. .ver 2:0:0:0 } .assembly sample { .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 ) .hash algorithm 0x00008004 .ver 0:0:0:0 } .module sample.exe // MVID: {A224F460-A049-4A03-9E71-80A36DBBBCD3} .imagebase 0x00400000 .file alignment 0x00000200 .stackreserve 0x00100000 .subsystem 0x0003       // WINDOWS_CUI .corflags 0x00000001    //  ILONLY // Image base: 0x02F20000 // =============== CLASS MEMBERS DECLARATION =================== .class public auto ansi beforefieldinit Hello extends [mscorlib]System.Object { .method public hidebysig static void  Main(string[] args) cil managed { .entrypoint // Code size       13 (0xd) .maxstack  8 IL_0000:  nop IL_0001:  ldstr      "Hello World!" IL_0006:  call       void [mscorlib]System.Console::WriteLine(string) IL_000b:  nop IL_000c:  ret } // end of method Hello::Main .method public hidebysig specialname rtspecialname instance void  .ctor() cil managed { // Code size       7 (0x7) .maxstack  8 IL_0000:  ldarg.0 IL_0001:  call       instance void [mscorlib]System.Object::.ctor() IL_0006:  ret } // end of method Hello::.ctor } // end of class Hello  
```  
  
## Vea también  
 [Tools](../../../docs/framework/tools/index.md)   
 [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)   
 [Proceso de ejecución administrada](../../../docs/standard/managed-execution-process.md)   
 [Símbolos del sistema](../../../docs/framework/tools/developer-command-prompt-for-vs.md)