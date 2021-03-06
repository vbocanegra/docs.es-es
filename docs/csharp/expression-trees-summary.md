---
title: "Resumen de árboles de expresión"
description: "Resumen de árboles de expresión"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: eb687ebd-1149-4453-9fc1-12a084495a66
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 82d4684ed27b23afd4972da6f68d1757472d85b6
ms.contentlocale: es-es
ms.lasthandoff: 05/22/2017

---

# <a name="expression-trees-summary"></a>Resumen de árboles de expresión

[Anterior: Traducción de expresiones](expression-trees-translating.md)

En esta serie, se vio cómo se pueden usar *árboles de expresión* para crear programas dinámicos que interpretan el código como datos y crean nueva funcionalidad basada en ese código.

Se pueden examinar los árboles de expresión para entender el propósito de un algoritmo. No se puede examinar solo ese código. Se pueden crear árboles de expresión nuevos que representen las versiones modificadas del código original.

También se pueden usar árboles de expresión para buscar en un algoritmo y traducirlo a otro lenguaje o entorno. 

## <a name="limitations"></a>Limitaciones

Hay algunos elementos de lenguaje de C# nuevos que no se traducen correctamente en árboles de expresión. Los árboles de expresión no pueden contener expresiones `await` ni expresiones lambda `async`. Muchas de las características agregadas en la versión 6 de C# no aparecen tal y como se escriben en árboles de expresión. En su lugar, se expondrán las características más recientes de los árboles de expresión en la sintaxis equivalente anterior. Es posible que esta limitación no sea tanta como podría parecer. De hecho, significa que el código que interpreta los árboles de expresión probablemente funcionará igual cuando se introduzcan las nuevas características de lenguaje.

Incluso con estas limitaciones, los árboles de expresión permiten crear algoritmos dinámicos que se basan en la interpretación y la modificación del código que se representa como una estructura de datos. Es una herramienta eficaz y es una de las características del ecosistema .NET que permite que las bibliotecas enriquecidas como Entity Framework realicen lo que hacen.


