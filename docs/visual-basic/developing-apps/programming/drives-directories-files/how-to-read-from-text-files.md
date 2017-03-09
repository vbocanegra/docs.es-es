---
title: "C&#243;mo: Leer archivos de texto en Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ejemplos [Visual Basic], leer archivos de texto"
  - "caracteres extendidos, leer"
  - "leer datos, archivos de texto"
  - "leer archivos de texto"
  - "archivos de texto, leer"
ms.assetid: 735fe9d7-0f7a-4185-ba02-f35e580ec4b8
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# C&#243;mo: Leer archivos de texto en Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

El método <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.ReadAllText%2A> del objeto `My.Computer.FileSystem` permite leer de un archivo de texto.  Se puede especificar la codificación del archivo si el contenido del mismo utiliza una codificación como ASCII o UTF\-8.  
  
 Si está leyendo de un archivo que incluye caracteres extendidos, deberá especificar la codificación del archivo.  
  
> [!NOTE]
>  Para leer una única línea de texto de un archivo a la vez, utilice el método <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.OpenTextFileReader%2A> del objeto `My.Computer.FileSystem`.  El método `OpenTextFileReader` devuelve un objeto <xref:System.IO.StreamReader>.  Puede usar el método <xref:System.IO.StreamReader.ReadLine%2A> del objeto `StreamReader` para leer de un archivo una línea a la vez.  Puede buscar el final del archivo con el método <xref:System.IO.StreamReader.EndOfStream%2A> del objeto `StreamReader`.  
  
### Para leer de un archivo de texto  
  
-   Utilice el método `ReadAllText` del objeto `My.Computer.FileSystem` para leer el contenido de un archivo de texto en una cadena, proporcionando la ruta de acceso.  El ejemplo siguiente lee el contenido del archivo test.txt, lo coloca en una cadena y, a continuación, lo muestra en un cuadro de mensaje.  
  
     [!code-vb[VbFileIORead#2](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-text-fi_1_1.vb)]  
  
### Para leer de un archivo de texto que está codificado  
  
-   Utilice el método `ReadAllText` del objeto `My.Computer.FileSystem` para leer el contenido de un archivo de texto en una cadena, proporcionando la ruta de acceso y el tipo de codificación del archivo.  El ejemplo siguiente lee el contenido del archivo UTF32 test.txt, lo coloca en una cadena y, a continuación, lo muestra en un cuadro de mensaje.  
  
     [!code-vb[VbFileIORead#3](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/visualbasic/how-to-read-from-text-fi_1_2.vb)]  
  
## Programación eficaz  
 Las condiciones siguientes pueden provocar una excepción:  
  
-   La ruta de acceso no es válida por una de las razones siguientes: es una cadena de longitud cero, sólo contiene un espacio en blanco, contiene caracteres no válidos o es una ruta de acceso de dispositivo \(<xref:System.ArgumentException>\).  
  
-   La ruta de acceso no es válida porque es `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   El archivo no existe \(<xref:System.IO.FileNotFoundException>\).  
  
-   El archivo está en uso por otro proceso o hay un error de E\/S \(<xref:System.IO.IOException>\).  
  
-   La ruta supera la longitud máxima definida por el sistema \(<xref:System.IO.PathTooLongException>\).  
  
-   Un nombre de archivo o de directorio de la ruta de acceso contiene un signo de dos puntos \(:\) o tiene un formato no válido \(<xref:System.NotSupportedException>\).  
  
-   No hay suficiente memoria para escribir la cadena en el búfer \(<xref:System.OutOfMemoryException>\).  
  
-   El usuario no tiene los permisos necesarios para ver la ruta de acceso \(<xref:System.Security.SecurityException>\).  
  
 No tome ninguna decisión sobre el contenido del archivo basándose en su nombre.  Por ejemplo, es posible que el archivo Form1.vb no sea un archivo de código fuente [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Compruebe todas las entradas antes de utilizar los datos en la aplicación.  Puede que el contenido del archivo no sea el esperado y que los métodos que leen el archivo produzcan un error.  
  
## Vea también  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>   
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>   
 [Leer archivos](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [Cómo: Leer archivos de texto delimitado por comas](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [Cómo: Leer archivos de texto de ancho fijo](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [Cómo: Leer archivos de texto con varios formatos](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)   
 [Solución de problemas: Leer y escribir en archivos de texto](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [Tutorial: Manipular archivos y directorios en Visual Basic](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)   
 [Codificaciones de archivos](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)