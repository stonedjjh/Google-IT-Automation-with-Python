# Métrica de Fiabilidad del sitio

## Acuerdos de nivel de servicio ANS

Las palabras "prometo" son poderosas y significativas. Si le dices a alguien que prometes hacer algo, esa persona espera que cumplas tu promesa. En el mundo de las operaciones y la tecnología, estas promesas se denominan Acuerdos de nivel de servicio (ANS).

En esta lectura, aprenderá más sobre los SLA, cómo se relacionan con los objetivos de nivel de servicio (SLO) y los SLA comunes en la industria.

### Acuerdos de nivel de servicio

Un acuerdo de nivel de servicio es un acuerdo entre un proveedor y sus clientes o usuarios que puede ser legalmente vinculante. Normalmente, el SLA se incluye en el contrato de venta, garantizando un nivel mínimo de rendimiento para la aplicación del cliente o usuario. Son como promesas que se hacen a los usuarios. Y como ocurre con cualquier promesa, romperla tiene consecuencias. El SLA especifica las consecuencias si no se cumplen las promesas. Las métricas del SLA pueden incluir el tiempo de actividad, la capacidad de respuesta y las responsabilidades.

### Cómo se relacionan los SLA con los SLO

Un SLA esboza los SLO específicos y las sanciones por violarlos. A menudo, estas consecuencias son una sanción económica o la cancelación del contrato. Por ello, es importante entender qué SLA se han acordado para tomar decisiones informadas sobre cuánto invertir en fiabilidad.

### Ejemplos de SLA

Para ver ejemplos y plantillas de SLA utilizados en el sector, consulte lo siguiente:

[Ejemplos y plantilla de acuerdos de nivel de servicio (SLA)](https://www.bmc.com/blogs/sla-template-examples/)

**Puntos clave:**

Un SLA es un acuerdo de servicio que suele celebrarse entre un proveedor de servicios de TI y un cliente. En él se describen los detalles del servicio, incluido lo que debe conseguir y las consecuencias en caso de incumplimiento del contrato.

## SLO

Todos los servicios tienen un nivel de calidad y rendimiento que intentan obtener o alcanzar. En el mundo de la tecnología y las operaciones, se denominan objetivos de nivel de servicio (OEN).

En esta lectura, aprenderá más sobre los objetivos de nivel de servicio, incluyendo cómo escribir objetivos de nivel de servicio apropiados y cómo los objetivos de nivel de servicio se relacionan con los acuerdos de nivel de servicio (SLA) y los indicadores de nivel de servicio (SLI).

### Definición de los objetivos a nivel de servicio (ODS)

Los SLO se encuentran dentro de un SLA y se centran en métricas específicas y medibles como el tiempo de actividad y el tiempo de respuesta. Los SLO establecen las expectativas de los clientes y comunican a los equipos de TI y DevOps los objetivos que deben alcanzar. Es importante entender e informarse sobre los SLO que se han prometido en el SLA para poder tomar decisiones informadas sobre cómo invertir en fiabilidad y mantener la promesa de alcanzar los objetivos.

Al crear los SLO, escríbalos de la forma más sencilla y clara posible. Si los SLO son vagos o inconmensurables, no servirán a su propósito - y usted se estará preparando para el fracaso.

### Ejemplo de SLO

Imagina que trabajas para una empresa de TI que ha firmado un contrato con un cliente, y ese contrato contiene el siguiente SLA:

Usted mantendrá el 99% del tiempo de actividad de su aplicación, definido como "la página de inicio se carga correctamente el 99% de las veces en 10 segundos o menos."

El SLA le indica qué SLIs deben ser monitorizados, incluyendo el tiempo de carga de la página y si la página se carga correctamente o devuelve un mensaje de error HTTP.

Sus SLO incluyen:

    1. La página se cargará en 10 segundos o menos el 99% de las veces.

    2. La página devolverá un código HTTP 200 (éxito) el 99% de las veces.

Una vez definidos el SLA y los SLO, puede utilizar una combinación de herramientas de supervisión para probar el sitio periódicamente y registrar los resultados para realizar un seguimiento del rendimiento real en relación con los SLO.

**Puntos clave:**

Los SLO son importantes porque ayudan a cumplir las promesas definidas en el SLA. Ayudan a establecer las expectativas del cliente y deben estar claramente redactados y ser medibles y alcanzables.

## SLIs

Un término común utilizado por los ingenieros de DevOps y los desarrolladores de software es indicador de nivel de servicio (SLI). Los SLI miden el rendimiento de una aplicación en un momento dado.

En esta lectura, aprenderá más sobre los SLI, incluyendo qué son, cómo medirlos y supervisarlos, y cómo se relacionan con los acuerdos de nivel de servicio (SLA) y los objetivos de nivel de servicio (SLO).

### Indicadores del nivel de servicio

Un SLI mide el rendimiento de su aplicación con respecto al objetivo, o SLO. Es importante controlar los SLI para determinar si la aplicación cumple el objetivo o incumple el SLA. En pocas palabras, los SLI ayudan a responder a la pregunta "¿Cómo lo hemos hecho?" en términos de tener una promesa y alcanzar esa promesa. Recuerde que los SLI deben ser sencillos y que debe elegir las métricas adecuadas para su seguimiento.

### Ejemplo de SLI

Imagine que trabaja para una empresa de TI y que firma un contrato con los clientes. El contrato contiene el siguiente SLA:

Usted mantendrá el 99% del tiempo de actividad de su aplicación, definido como "la página de inicio se carga correctamente el 99% de las veces en 10 segundos o menos"

El SLA le indica qué SLI debe supervisar, incluido el tiempo de carga de la página y si la página se carga correctamente o devuelve un mensaje de error HTTP.

Herramientas de monitorización como DataDog o AppDynamics pueden medir y registrar estas métricas por usted. Estas herramientas ofrecen la posibilidad de realizar comprobaciones sintéticas, simulando que un usuario accede a su aplicación y registrando los resultados. Los resultados de las comprobaciones sintéticas pueden utilizarse como sus SLI. Estas herramientas de supervisión le ayudan a determinar si está cumpliendo sus objetivos de nivel de servicio.

**Puntos clave:**

Los indicadores de nivel de servicio ayudan a hacer mensurables los objetivos de nivel de servicio. Proporcionan datos reales sobre el rendimiento. Los SLA, los SLO y los SLI desempeñan un papel en la fiabilidad general del servicio.

## Presupuestos de error

¿Recuerdas cuando eras pequeño y alguien te dio veinte dólares para gastar en el supermercado? Puede que te dijeran que trajeras a casa un galón de leche y una docena de huevos, y que el dinero que te sobrara lo gastaras como quisieras. Ese dinero extra -o el cambio- es similar a un presupuesto de error en las operaciones de servicio.

En esta lectura, aprenderá más sobre los presupuestos de errores, cómo se relacionan con las funciones de TI y cómo se puede utilizar un presupuesto de errores en el mundo real.

### Definición de un presupuesto de errores

Un presupuesto de errores es la cantidad máxima de tiempo que un programa de software puede fallar y seguir cumpliendo con el objetivo de nivel de servicio (SLO). Un presupuesto de errores suele representarse mediante un porcentaje. Un ejemplo sencillo es el siguiente: Si un objetivo de nivel de servicio establece que un sitio web debe funcionar correctamente el 99,9% de las veces, el presupuesto de errores es sólo del 0,1%.

Ahora calculemos el presupuesto de errores utilizando el tiempo como medida en la pregunta siguiente. He aquí un ejemplo en el que se calcula un presupuesto de error para un período de tiempo de un mes utilizando la siguiente fórmula:

Presupuesto de errores = Tiempo total \* (1-SLO)

¿Cuál es el presupuesto de errores, en minutos, con un SLO del 99,9% de tiempo de actividad durante un mes?

El tiempo total es el tiempo total en minutos para un periodo de tiempo determinado. (El SLO es el objetivo de nivel de servicio representado como un decimal).

Tiempo total = `30*24*60` = 43.200. Esta fórmula multiplica 30 días por 24 horas en cada día por 60 minutos en cada hora para obtener un total de 43.200 minutos.

SLO = 99,9/100 = 0,999. Este valor representa el SLO como decimal. Sustituya estos valores en la fórmula para obtener:

Presupuesto de error = 43.200 \* (1-0,999)

Presupuesto de error = 43,1 minutos. Esto significa que la cantidad máxima de tiempo que el servicio puede estar caído es de hasta 43 minutos al mes sin violar los estándares de fiabilidad acordados (el SLO).

### El papel de los presupuestos de errores

Los presupuestos de errores forman parte de las operaciones en la nube, la ingeniería de fiabilidad del sitio y los equipos DevOps. Se utilizan como medida para asegurarse de que todo funciona correctamente. Si todo funciona sin problemas y hay una cantidad significativa de tiempo para utilizar del presupuesto de errores, entonces los miembros de DevOps pueden utilizar este tiempo para invertir en innovación en un producto o programa de software. Los presupuestos de errores también ayudan a establecer límites para los equipos de desarrollo y programación. Si no hay mucho presupuesto de errores para utilizar, entonces los desarrolladores saben que no pueden probar cosas nuevas y que su atención debe seguir centrada en la fiabilidad del producto o programa. Los desarrolladores deberían reservar la publicación de nuevas funciones para cuando el presupuesto para errores sea elevado.

**Puntos clave:**

Los presupuestos de errores suelen representarse como la cantidad máxima de tiempo que un programa puede fallar sin violar un acuerdo. El presupuesto de errores se basa en el SLO acordado entre los clientes y el proveedor. Los desarrolladores están a favor de presupuestos de error más altos porque esto les permite innovar y probar cosas nuevas dentro del producto o servicio.
