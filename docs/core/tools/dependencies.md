---
title: "Administración de dependencias en las herramientas de .NET Core | Microsoft Docs"
description: "Explica cómo administrar las dependencias con las herramientas de .NET Core."
keywords: CLI, extensibilidad, comandos personalizados, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 74b87cdb-a244-4c13-908c-539118bfeef9
ms.translationtype: Human Translation
ms.sourcegitcommit: 25847dd6921e547074f4501d34d865dfb1b98b59
ms.openlocfilehash: de496d96120df1ec275bb4a69f01b6266b0b5a89
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---

# <a name="managing-dependencies-with-net-core-sdk-10"></a>Administración de dependencias con el SDK 1.0 de .NET Core

Con el paso de los proyectos .NET Core de project.json a csproj y MSBuild, también se ha producido una inversión significativa que ha dado lugar a la unificación del archivo de proyecto y los recursos que permiten el seguimiento de dependencias. Para los proyectos .NET Core, esto es similar a lo que hizo project.json. No hay ningún archivo independiente JSON o XML que realice el seguimiento de las dependencias de NuGet. Con este cambio, también hemos introducido otro tipo de *referencia* en la sintaxis de csproj llamada `<PackageReference>`. 

Este documento describe el nuevo tipo de referencia. También muestra cómo agregar a su proyecto una dependencia de paquete mediante este nuevo tipo de referencia. 

## <a name="the-new-packagereference-element"></a>El nuevo elemento \<PackageReference>
El elemento `<PackageReference>` tiene la siguiente estructura básica:

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" />
```

Si ya conoce MSBuild, le resultarán familiares los otros tipos de referencia que ya existen. La clave es la instrucción `Include` que especifica el identificador de paquete que desea agregar al proyecto. El elemento secundario `<Version>` especifica la versión que se obtiene. Las versiones se especifican según las como por [reglas de versión de NuGet](https://docs.microsoft.com/nuget/create-packages/dependency-versions#version-ranges).

> [!NOTE]
> Si no está familiarizado con la sintaxis general de `csproj`, puede usar la documentación de [referencia de proyecto de MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference) para obtener más información.  

La adición de una dependencia que solo está disponible en un destino específico se realiza mediante condiciones similares a las del siguiente ejemplo:

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" Condition="'$(TargetFramework)' == 'netcoreapp1.0'" />
```

Lo anterior significa que la dependencia solo será válida si la compilación sucede para ese destino dado. El elemento `$(TargetFramework)` de la condición es una propiedad de MSBuild que se está configurando en el proyecto. Con aplicaciones .NET Core más comunes, no será necesario hacer esto. 

## <a name="adding-a-dependency-to-your-project"></a>Adición de una dependencia al proyecto
Agregar una dependencia a su proyecto es muy sencillo. Este es un ejemplo de cómo agregar la versión `9.0.1` de Json.NET a su proyecto. Por supuesto, es aplicable a cualquier otra dependencia de NuGet. 

Al abrir el archivo de proyecto, verá dos o más nodos `<ItemGroup>`. Observe que uno de los nodos ya contiene elementos `<PackageReference>`. Puede agregar la nueva dependencia a este nodo, o crear uno nuevo; es su decisión, ya que el resultado será el mismo. 

En este ejemplo utilizaremos la plantilla predeterminada que se ha descartado mediante `dotnet new console`. Se trata de una aplicación de consola simple. Cuando se abre el proyecto, primero encontramos el elemento `<ItemGroup>` que ya contiene `<PackageReference>`. A continuación, le agregamos lo siguiente:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
```
Después de esto, guardamos el proyecto y ejecutamos el comando `dotnet restore` para instalar la dependencia. 

El proyecto completo tiene este aspecto:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
</Project>
```

## <a name="removing-a-dependency-from-the-project"></a>Eliminación de una dependencia del proyecto
La eliminación de una dependencia del archivo de proyecto supone simplemente quitar el elemento `<PackageReference>` del archivo de proyecto.

