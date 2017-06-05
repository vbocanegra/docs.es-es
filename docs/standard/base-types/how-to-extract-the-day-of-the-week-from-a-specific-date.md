---
title: "C&#243;mo: Extraer el d&#237;a de la semana de una fecha concreta | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "formato [.NET Framework], fechas"
  - "DateTime.DayOfWeek (propiedad)"
  - "DateTime.ToString (método)"
  - "fechas [.NET Framework], recuperar información de la semana"
  - "DateTimeOffset.DayOfWeek (propiedad)"
  - "fechas [.NET Framework], día de la semana"
  - "Weekday (función)"
  - "día de la semana [.NET Framework]"
  - "extraer día de la semana"
  - "nombres de los días de la semana"
  - "WeekdayName (función)"
  - "números [.NET Framework], día de la semana"
  - "dar formato [.NET Framework], hora"
  - "DateTimeOffset.ToString (método)"
  - "nombres completos de los días de la semana"
ms.assetid: 1c9bef76-5634-46cf-b91c-9b9eb72091d7
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# C&#243;mo: Extraer el d&#237;a de la semana de una fecha concreta
.NET Framework permite determinar fácilmente el número de día de la semana correspondiente a una fecha concreta, así como mostrar el nombre localizado del día de la semana para una fecha en particular. Las propiedades <xref:System.DateTime.DayOfWeek%2A> o <xref:System.DateTimeOffset.DayOfWeek%2A> proporcionan un valor enumerado que indica el día de la semana correspondiente a una fecha concreta. Por el contrario, la recuperación del nombre del día de la semana es una operación de formato que puede realizarse con una llamada a un método de formato como, por ejemplo, un método `ToString` de un valor de fecha y hora o un método <xref:System.String.Format%2A?displayProperty=fullName>. En este tema se muestra cómo realizar estas operaciones de formato.  
  
### Para obtener un número que indique el día de la semana a partir de una fecha específica  
  
1.  Cuando trabaje con la representación de cadena de una fecha, conviértala en un valor <xref:System.DateTime> o <xref:System.DateTimeOffset> mediante el método estático <xref:System.DateTime.Parse%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName>.  
  
2.  Use las propiedades <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=fullName> para recuperar un valor <xref:System.DayOfWeek> que indique el día de la semana.  
  
3.  En caso necesario, convierta \(en C\# o en Visual Basic\) el valor <xref:System.DayOfWeek> en un entero.  
  
 En el ejemplo siguiente se muestra un entero que representa el día de la semana de una fecha concreta.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/weekdaynumber7.cs#7)]
 [!code-vb[Formatting.Howto.WeekdayName#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/weekdaynumber7.vb#7)]  
  
### Para obtener el nombre abreviado del día de la semana a partir de una fecha específica  
  
1.  Cuando trabaje con la representación de cadena de una fecha, conviértala en un valor <xref:System.DateTime> o <xref:System.DateTimeOffset> mediante el método estático <xref:System.DateTime.Parse%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName>.  
  
2.  Puede obtener el nombre abreviado de un día de la semana de la referencia cultural actual o de una referencia cultural específica:  
  
    1.  Para obtener el nombre abreviado del día de la semana de la referencia cultural actual, llame al método de instancia <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> del valor de fecha y hora, y pase la cadena "ddd" como parámetro `format`. En el ejemplo siguiente se muestra la llamada al método <xref:System.DateTime.ToString%28System.String%29>.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname1.cs#1)]
         [!code-vb[Formatting.Howto.WeekdayName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname1.vb#1)]  
  
    2.  Para obtener el nombre abreviado del día de la semana de una referencia cultural específica, llame al método de instancia <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> del valor de fecha y hora. Pase la cadena "ddd" como parámetro `format`. Pase un objeto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.DateTimeFormatInfo> que represente la referencia cultural cuyo nombre del día de la semana desee recuperar como parámetro `provider`. En el código siguiente se muestra una llamada al método <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> con un objeto <xref:System.Globalization.CultureInfo> que representa la referencia cultural fr\-FR.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname2.cs#2)]
         [!code-vb[Formatting.Howto.WeekdayName#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname2.vb#2)]  
  
### Para obtener el nombre completo del día de la semana a partir de una fecha específica  
  
1.  Cuando trabaje con la representación de cadena de una fecha, conviértala en un valor <xref:System.DateTime> o <xref:System.DateTimeOffset> mediante el método estático <xref:System.DateTime.Parse%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName>.  
  
2.  Puede obtener el nombre completo de un día de la semana de la referencia cultural actual o de una referencia cultural específica:  
  
    1.  Para obtener el nombre del día de la semana de la referencia cultural actual, llame al método de instancia <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> del valor de fecha y hora, y pase la cadena "dddd" como parámetro `format`. En el ejemplo siguiente se muestra la llamada al método <xref:System.DateTime.ToString%28System.String%29>.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname4.cs#4)]
         [!code-vb[Formatting.Howto.WeekdayName#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname4.vb#4)]  
  
    2.  Para obtener el nombre del día de la semana de una referencia cultural específica, llame al método de instancia <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> del valor de fecha y hora. Pase la cadena "dddd" como parámetro `format`. Pase un objeto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.DateTimeFormatInfo> que represente la referencia cultural cuyo nombre del día de la semana desee recuperar como parámetro `provider`. En el código siguiente se muestra una llamada al método <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> con un objeto <xref:System.Globalization.CultureInfo> que representa la referencia cultural es\-ES.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname5.cs#5)]
         [!code-vb[Formatting.Howto.WeekdayName#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname5.vb#5)]  
  
## Ejemplo  
 En el ejemplo se muestran llamadas a las propiedades <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> y <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=fullName> y los métodos <xref:System.DateTime.ToString%2A?displayProperty=fullName> y <xref:System.DateTimeOffset.ToString%2A?displayProperty=fullName> para recuperar el número que representa el día de la semana, el nombre abreviado del día de la semana y el nombre completo del día de la semana para una fecha en particular.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/example6.cs#6)]
 [!code-vb[Formatting.Howto.WeekdayName#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example6.vb#6)]  
  
 Puede haber lenguajes que ofrezcan una funcionalidad que duplique o complemente a la proporcionada por [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por ejemplo, Visual Basic incluye dos funciones así:  
  
-   `Weekday`, que devuelve un número que indica el día de la semana a partir de una fecha específica. Considera que el valor ordinal del primer día de la semana es uno, mientras que la propiedad <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> considera que es cero.  
  
-   `WeekdayName`, que devuelve el nombre de la semana en la referencia cultural actual que corresponde a un número concreto del día de la semana.  
  
 En el ejemplo siguiente se demuestra el uso de las funciones `Weekday` y `WeekdayName`.  
  
 [!code-vb[Formatting.HowTo.WeekdayName#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example9.vb#9)]  
  
 También se puede usar el valor devuelto por la propiedad <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> para recuperar el nombre del día de la semana de una fecha en particular. Para ello, solo se necesita hacer una llamada al método <xref:System.Enum.ToString%2A> en el valor <xref:System.DayOfWeek> devuelto por la propiedad. Sin embargo, esta técnica no produce el nombre localizado de un día de la semana para la referencia cultural actual, tal como se muestra en el ejemplo siguiente.  
  
 [!code-csharp[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/Howto1.cs#8)]
 [!code-vb[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/Howto1.vb#8)]  
  
## Vea también  
 [Efectuar operaciones de formato](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [Cadenas con formato de fecha y hora estándar](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [Cadenas con formato de fecha y hora personalizado](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)