---
title: "Informaci&#243;n general de seguridad | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33e09965-61d5-48cc-9e8c-3b047cc4f194
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Informaci&#243;n general de seguridad
La protección de una aplicación es un proceso continuo.  Es prácticamente imposible que se llegue a un momento en el que un programador pueda garantizar que una aplicación es invulnerable ante todo tipo de ataques, ya que no es posible predecir los tipos de ataques que surgirán en un futuro con las nuevas tecnologías.  Al contrario, el hecho de que nadie haya detectado \(o publicado\) aún brechas de seguridad en un sistema, no quiere decir que éstas no existan o no puedan existir en un futuro.  Por lo tanto, es necesario planificar la seguridad durante la fase de diseño del proyecto, así como la forma en que se mantendrá la seguridad durante el ciclo de vida de la aplicación.  
  
## Diseñar la seguridad  
 Uno de los mayores problemas de la programación de aplicaciones seguras es el hecho de que a menudo la seguridad no se planifica con antelación, sino que se implementa cuando el código de un proyecto se ha completado.  Esta práctica genera aplicaciones poco seguras, ya que no se ha dedicado suficiente tiempo a entender qué hace que una aplicación sea segura.  
  
 La implementación de la seguridad a última hora puede producir nuevos errores, ya que el software falla debido a las nuevas restricciones o hay que volver a escribirlo para albergar funcionalidad no planificada inicialmente.  Cada línea de código revisado incluye la posibilidad de insertar un error nuevo.  En ese sentido, debe tener en cuenta la seguridad al principio del proceso de programación de manera que se desarrolle junto con la programación de nuevas características.  
  
### Modelo de amenazas  
 No se puede proteger un sistema de ataques a menos que comprenda todos los posibles ataques a los que está expuesto.  El proceso de evaluación de amenazas a la seguridad, llamado *modelo de amenazas*, es necesario para determinar la probabilidad y las ramificaciones de las infracciones de seguridad en la aplicación ADO.NET.  
  
 El modelo de amenazas está compuesto de tres pasos principales: comprender la visión del adversario, caracterizar la seguridad del sistema y determinar las amenazas.  
  
 El modelo de amenazas es un enfoque repetitivo en la evaluación de las vulnerabilidades de la aplicación, que se usa para detectar las vulnerabilidades más peligrosas, ya que éstas exponen los datos más confidenciales.  Una vez identificadas, las vulnerabilidades se clasifican en función de su gravedad y se crea un conjunto con prioridades de medidas para contrarrestar las amenazas.  
  
 Para obtener más información, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|El sitio sobre [patrones de amenazas](http://go.microsoft.com/fwlink/?LinkId=98353) del Centro para desarrolladores de seguridad de MSDN.|Los recursos de esta página le ayudarán a entender el proceso de modelo de amenazas y a desarrollar modelos de amenazas que puede usar para proteger sus propias aplicaciones|  
  
## Principio de los privilegios mínimos  
 Cuando diseñe, compile e implemente la aplicación, debe asumir que ésta será objeto de ataques.  Estos ataques suelen proceder de código malintencionado que se activa con los permisos del usuario que ejecuta el código.  Otros pueden provenir de código no dañino, cuyas vulnerabilidades aprovecha un atacante.  Cuando se planifica la seguridad, siempre hay que asumir que se puede producir la peor situación posible.  
  
 Una medida para contrarrestar los ataques consiste en intentar establecer tantos muros en el código como sea posible mediante la ejecución con los privilegios mínimos.  El principio de los privilegios mínimos indica que se deben conceder privilegios para la menor cantidad de código posible durante el tiempo mínimo necesario para conseguir que se realice el trabajo.  
  
 El procedimiento recomendado para crear aplicaciones seguras consiste en comenzar sin ningún permiso y ir agregando los mínimos permisos necesarios para la tarea concreta que se lleva a cabo.  El enfoque opuesto, es decir, comenzar con todos los permisos e ir denegando permisos posteriormente de forma individual, proporciona aplicaciones poco seguras, difíciles de probar y mantener, ya que pueden existir vulnerabilidades de seguridad causados por concesiones no intencionadas de más permisos de los que son necesarios.  
  
 Para obtener más información sobre cómo proteger las aplicaciones, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|[Proteger aplicaciones](../Topic/Securing%20Applications.md)|Contiene vínculos a temas generales de la seguridad.  Asimismo, incluye vínculos a temas sobre la protección de las aplicaciones distribuidas, aplicaciones web, aplicaciones móviles y de escritorio.|  
  
## Seguridad de acceso del código \(CAS\)  
 La seguridad de acceso del código \(CAS\) es un mecanismo que ayuda a limitar el acceso del código a recursos y operaciones protegidos.  En .NET Framework, CAS realiza las funciones siguientes:  
  
-   Define permisos y conjuntos de permisos que representan el derecho de acceso a varios recursos del sistema.  
  
-   Permite a los administradores configurar la directiva de seguridad mediante la asociación de conjuntos de permisos a grupos de código.  
  
-   Permite que el código solicite los permisos que necesita para ejecutarse, así como los permisos que sería útil tener, y especifica los permisos que nunca debe tener el código.  
  
-   Concede permisos a cada ensamblado que se carga, basándose en los permisos solicitados por el código y en las operaciones permitidas por la directiva de seguridad.  
  
-   Permite que el código exija que sus llamadores tengan permisos específicos.  
  
-   Permite que el código exija que sus llamadores posean una firma digital, por lo que solo los llamadores de una organización o un sitio concretos pueden llamar al código protegido.  
  
-   Impone restricciones en el código en tiempo de ejecución mediante la comparación de los permisos concedidos a cada llamador en la pila de llamadas con los permisos que deben poseer.  
  
 Para reducir los daños que se pueden producir cuando un ataque tiene éxito, elija un contexto de seguridad para el código de forma que se conceda acceso única y exclusivamente a los recursos necesarios para realizar el trabajo.  
  
 Para obtener más información, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|[Seguridad de acceso del código y ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)|Describe las interacciones entre la seguridad de acceso del código, la seguridad basada en funciones y los entornos de confianza parcial desde la perspectiva de una aplicación ADO.NET.|  
|[Code Access Security](http://msdn.microsoft.com/es-es/23a20143-241d-4fe5-9d9f-3933fd594c03)|Contiene vínculos a temas adicionales que describen CAS en .NET Framework.|  
  
## Seguridad de la base de datos  
 El principio de privilegios mínimos también se aplica al origen de los datos.  A continuación se citan algunas instrucciones generales para la seguridad de base de datos:  
  
-   Crear cuentas con los privilegios mínimos posibles.  
  
-   No permitir que los usuarios obtengan acceso a cuentas administrativas tan solo para que el código funcione.  
  
-   No devolver mensajes de error de servidor a las aplicaciones cliente.  
  
-   Validar todas las entradas, tanto en el cliente como en el servidor.  
  
-   Usar comandos con parámetros y evitar instrucciones SQL dinámicas.  
  
-   Habilitar el registro y la auditoría de seguridad en la base de datos que se utiliza, de forma que se reciba una alerta en caso de infracciones de seguridad.  
  
 Para obtener más información, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|[Seguridad en SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)|Proporciona una introducción general a la seguridad de SQL Server con escenarios de aplicación que orientan en la creación de aplicaciones ADO.NET seguras dirigidas a SQL Server.|  
|[Recommendations for Data Access Strategies](http://msdn.microsoft.com/es-es/72411f32-d12a-4de8-b961-e54fca7faaf5)|Proporciona recomendaciones para obtener acceso a datos y realizar operaciones de base de datos.|  
  
## Directiva de seguridad y administración  
 La administración inadecuada de la directiva de seguridad de acceso del código \(CAS\) puede crear puntos débiles en la seguridad.  Cuando se utiliza una aplicación, deben seguirse las técnicas de supervisión de seguridad y deben evaluarse los riesgos a medida que surgen nuevas amenazas.  
  
 Para obtener más información, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|-------------|-----------------|  
|[NIB: Security Policy Management](http://msdn.microsoft.com/es-es/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9)|Proporciona información sobre la creación y administración de la directiva de seguridad.|  
|[NIB: Security Policy Best Practices](http://msdn.microsoft.com/es-es/d49bc4d5-efb7-4caa-a2fe-e4d3cec63c05)|Proporciona vínculos a temas que describen cómo administrar la directiva de seguridad.|  
  
## Vea también  
 [Proteger aplicaciones de ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Seguridad del código nativo y del código de .NET Framework](http://msdn.microsoft.com/es-es/bd61be84-c143-409a-a75a-44253724f784)   
 [Seguridad en SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Proveedores administrados de ADO.NET y centro de desarrolladores de conjuntos de datos](http://go.microsoft.com/fwlink/?LinkId=217917)