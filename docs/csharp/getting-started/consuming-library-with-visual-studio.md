---
title: Consumo de una biblioteca de clases con .NET Core en Visual Studio 2017 | Microsoft Docs
description: "Obtenga información sobre cómo llamar a los miembros de una biblioteca de clases con Visual Studio 2017."
keywords: ".NET Core, biblioteca de clases de .NET Core, .NET Standard, distribución de biblioteca de clases de .NET Standard"
author: BillWagner
ms.author: wiwang
ms.date: 04/17/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: d7b94076-1108-4174-94e7-a18f00072bb7
ms.translationtype: Human Translation
ms.sourcegitcommit: 4437ce5d344cf06d30e31911def6287999fc6ffc
ms.openlocfilehash: 5ad07e4116c75eb9b9d513c2a4fe43dfe62660d5
ms.contentlocale: es-es
ms.lasthandoff: 06/12/2017

---

<a id="consuming-a-class-library-with-net-core-in-visual-studio-2017" class="xliff"></a>

# Consumo de una biblioteca de clases con .NET Core en Visual Studio 2017

Una vez que ha seguido los pasos indicados en [Building a C# class library with .NET Core in Visual Studio 2017](./library-with-visual-studio.md) (Creación de una biblioteca de clases de C# con .NET Core en Visual Studio 2017) y en [Prueba de una biblioteca de clases con .NET Core en Visual Studio 2017](testing-library-with-visual-studio.md) para compilar y probar la biblioteca de clases, y ha creado una versión de lanzamiento de la biblioteca, el paso siguiente consiste en hacer que esté disponible para los llamadores. Existen dos maneras de hacerlo:

* Si una única solución va a usar la biblioteca (por ejemplo, si es un componente de una sola aplicación más grande), se puede incluir como proyecto en la solución.

* Si la biblioteca va a ser accesible con carácter general, puede distribuirla como un paquete NuGet.

<a id="including-a-library-as-a-project-in-a-solution" class="xliff"></a>

## Inclusión de una biblioteca como proyecto en una solución

Así como se incluyen pruebas unitarias en la misma solución que la biblioteca de clases, se puede incluir la aplicación como parte de esa solución. Por ejemplo, se puede usar la biblioteca de clases en una aplicación de consola que pide al usuario que inserte una cadena e informa de si su primer carácter está en mayúsculas:

1. Abra la solución `ClassLibraryProjects` creada en el tema [Building a C# Class Library with .NET Core in Visual Studio 2017](./library-with-visual-studio.md) (Creación de una biblioteca de clases de C# con .NET Core en Visual Studio 2017). En el **Explorador de soluciones**, haga clic con el botón derecho en la solución **ClassLibraryProject** y seleccione **Agregar** > **Nuevo proyecto** en el menú contextual.

1. En el cuadro de diálogo **Agregar nuevo proyecto**, seleccione el nodo **.NET Core** seguido por la plantilla del proyecto **Aplicación de consola (.NET Core)**. En el cuadro de texto **Nombre**, escriba "Presentación" y pulse el botón **Aceptar**.

   ![Cuadro de diálogo Agregar nuevo proyecto](./media/consuming-library-with-visual-studio/addnewproject.png)

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **Presentación** y seleccione **Establecer como proyecto de inicio** en el menú contextual.

   ![Menú contextual de Presentación](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. Inicialmente, el proyecto no tiene acceso a la biblioteca de clases. Para permitir que se llame a métodos de la biblioteca de clases, puede crear una referencia a la biblioteca de clases. En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo **Dependencias** del proyecto `ShowCase` y seleccione **Agregar referencia**.

   ![Menú contextual Dependencias de Presentación](./media/consuming-library-with-visual-studio/addreference.png)

1. En el cuadro de diálogo **Administrador de referencias**, seleccione **StringLibrary**, el proyecto de biblioteca de clases, y pulse el botón **Aceptar**.

   ![Administrador de referencias](./media/consuming-library-with-visual-studio/referencemanager.png)

1. En la ventana de código del archivo *Program.cs*, reemplace todo el código por el código siguiente:

 [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs#1)]

   El código usa la propiedad [Console.WindowHeight](xref:System.Console.WindowHeight) para determinar el número de filas de la ventana de consola. Siempre que la propiedad [Console.CursorTop](xref:System.Console.CursorTop) sea mayor o igual que el número de filas de la ventana de consola, el código borra la ventana de consola y muestra un mensaje al usuario.

   El programa le pide al usuario que escriba una cadena. Indica si la cadena comienza con un carácter en mayúsculas. Si el usuario presiona la tecla Entrar sin especificar una cadena, la aplicación finaliza y la ventana de consola se cierra.

1. Si es necesario, cambie la barra de herramientas para compilar la versión de **depuración** del proyecto `ShowCase`. Compile y ejecute el programa haciendo clic en la flecha verde en el botón **Presentación**.

   ![Imagen](./media/consuming-library-with-visual-studio/toolbar.png)

La aplicación que usa esta biblioteca se puede depurar y publicar siguiendo los pasos indicados en [Debugging your C# Hello World Application with Visual Studio 2017](debugging-with-visual-studio.md) (Depuración de la aplicación Hola a todos en C# con Visual Studio 2017) y [Publishing your Hello World Application with Visual Studio 2017](publishing-with-visual-studio.md) (Publicación de la aplicación Hola a todos con Visual Studio 2017).

<a id="distributing-the-library-in-a-nuget-package" class="xliff"></a>

## Distribución de la biblioteca en un paquete NuGet

Puede hacer que la biblioteca de clases tenga una disponibilidad amplia si la publica como un paquete NuGet. Visual Studio no admite la creación de paquetes NuGet. Para crear uno, se usa la [utilidad de línea de comandos `dotnet`](../../core/tools/dotnet.md):

1. Abra una ventana de consola. Por ejemplo, en el cuadro de texto **Pregúntame cualquier cosa** de la barra de tareas de Windows, escriba `Command Prompt` (o `cmd` para abreviar) y abra una ventana de consola seleccionando la aplicación de escritorio **Símbolo del sistema** o presionando Entrar si está seleccionada en los resultados de búsqueda.

1. Vaya al directorio del proyecto de la biblioteca. A menos que haya reconfigurado la ubicación típica del archivo, se encuentra en el directorio *Documentos\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary*. El directorio contiene el código fuente y un archivo de proyecto, *StringLibrary.csproj*.

1. Emita el comando `dotnet pack --no-build`: La utilidad `dotnet` genera un paquete con una extensión *.nupkg*.

   > [!TIP]
   > Si el directorio que contiene *dotnet.exe* no está en la ruta de acceso, puede encontrar su ubicación escribiendo `where dotnet.exe` en la ventana de consola.

Para más información sobre la creación de paquetes NuGet, consulte [Cómo crear un paquete NuGet con herramientas multiplataforma ](../../core/deploying/creating-nuget-packages.md).

