---
title: "&lt;CompatSortNLSVersion&gt; (Elemento) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
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
  - "<CompatSortNLSVersion> (elemento)"
  - "CompatSortNLSVersion (elemento)"
ms.assetid: 782cc82e-83f7-404a-80b7-6d3061a8b6e3
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# &lt;CompatSortNLSVersion&gt; (Elemento)
Especifica que el runtime debe usar criterios de ordenación heredados al realizar comparaciones de cadenas.  
  
## Sintaxis  
  
```  
<CompatSortNLSVersion    
   enabled="4096"/>  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|`enabled`|Atributo necesario.<br /><br /> Especifica el identificador de configuración regional cuyo criterio de ordenación se va a usar.|  
  
## Atributo enabled  
  
|Valor|Descripción|  
|-----------|-----------------|  
|4096|El identificador de configuración regional que representa un criterio de ordenación alternativo.  En este caso, 4096 representa el criterio de ordenación de [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] y versiones anteriores.|  
  
### Elementos secundarios  
 Ninguno.  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`runtime`|Contiene información sobre las opciones de inicialización del motor en tiempo de ejecución.|  
  
## Comentarios  
 Dado que las operaciones de comparación y ordenación de cadenas, así como de aplicación de mayúsculas y minúsculas, realizadas por la clase <xref:System.Globalization.CompareInfo?displayProperty=fullName> en [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] cumplen el estándar Unicode 5.1, los resultados de los métodos de comparación de cadenas como <xref:System.String.Compare%28System.String%2CSystem.String%29?displayProperty=fullName> y <xref:System.String.LastIndexOf%28System.String%29?displayProperty=fullName> pueden diferir de las versiones anteriores de .NET Framework.  Si la aplicación depende de un comportamiento heredado, puede restaurar las reglas de comparación y ordenación de cadenas usadas en [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)] y versiones anteriores incluyendo el elemento `<CompatSortNLSVersion>` en el archivo de configuración de la aplicación.  
  
> [!IMPORTANT]
>  La restauración de reglas de comparación y ordenación de cadenas heredadas también requiere que la biblioteca de vínculos dinámicos sort00001000.dll esté disponible en el sistema local.  
  
 También puede usar reglas de ordenación y comparación de cadenas heredadas en un dominio de aplicación concreto. Para ello, pase la cadena "NetFx40\_Legacy20SortingBehavior" al método <xref:System.AppDomainSetup.SetCompatibilitySwitches%2A> al crear el dominio de aplicación.  
  
## Ejemplo  
 En el ejemplo siguiente, se crean instancias de dos objetos <xref:System.String> y se llama al método <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=fullName> para compararlas usando las convenciones de la referencia cultural actual.  
  
 [!code-csharp[String.BreakingChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/string.breakingchanges/cs/example1.cs#1)]
 [!code-vb[String.BreakingChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/string.breakingchanges/vb/example1.vb#1)]  
  
 Al ejecutar el ejemplo en [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], muestra el siguiente resultado.  
  
```  
sta follows a in the sort order.  
```  
  
 Este es completamente diferente del resultado que se muestra al ejecutar el ejemplo en [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  
  
```  
sta equals a in the sort order.  
```  
  
 Sin embargo, si agrega el siguiente archivo de configuración al directorio del ejemplo y, a continuación, ejecuta el ejemplo en [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], el resultado es idéntico al producido por el ejemplo cuando se ejecuta en [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  
  
```  
<?xml version ="1.0"?>  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
## Vea también  
 [Esquema de la configuración de Common Language Runtime](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Esquema de los archivos de configuración](../../../../../docs/framework/configure-apps/file-schema/index.md)