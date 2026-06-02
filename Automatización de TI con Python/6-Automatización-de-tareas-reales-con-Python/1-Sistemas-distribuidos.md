# Sistemas distribuidos

Un sistema distribuido es un conjunto de componentes de software diseñados para trabajar juntos aunque estén en servidores distintos.

Los sistemas distribuidos, también denominados informática distribuida o bases de datos distribuidas, utilizan distintos nodos para interactuar y sincronizarse a través de una red compartida. Estos nodos también pueden representar procesos de software independientes u otros sistemas encapsulados recursivos. También suelen representar elementos físicos de hardware independientes, como servidores. Los Sistemas distribuidos funcionan para eliminar los cuellos de botella del sistema y los puntos de fallo únicos.

Un ejemplo común de un sistema distribuido sería un sitio web que contiene:

- Lógica de presentación: responsable de mostrar la interfaz de usuario y gestionar las interacciones de los usuarios

- Lógica de negocio: gestiona las reglas y procesos de la aplicación, garantizando la correcta manipulación de los datos y su funcionalidad

- Motor de base de datos: almacena y recupera los datos utilizados por el sitio web

- Servidor web: sirve de intermediario entre el navegador del usuario y los distintos componentes

Todos estos elementos podrían ejecutarse en un único servidor, pero es habitual que cada componente funcione en servidores distintos para garantizar la redundancia y la tolerancia a fallos.

## Características clave de un sistema distribuido

Los sistemas informáticos distribuidos tienen las siguientes características:

- Compartición de recursos - Un sistema distribuido puede compartir hardware, software o datos

- Detección de errores - Los errores y las ineficiencias pueden detectarse más fácilmente

- Transparencia - Un nodo del sistema puede interactuar y comunicarse con otros nodos

- Procesamiento simultáneo: varias máquinas pueden procesar la misma función a la vez

- Escalabilidad: si se añaden más máquinas, la potencia de cálculo y procesamiento puede aumentar según sea necesario

- Heterogeneidad: la mayoría de los sistemas distribuidos tienen nodos y componentes asíncronos que utilizan diversos sistemas operativos, middleware, software y hardware, lo que permite ampliar o añadir nuevos componentes

Los Sistemas distribuidos se utilizan en diversas aplicaciones y escenarios, como computación en la nube, Servicios web, redes entre pares, redes de distribución de contenidos (CDN), computación en red, etc. Permiten a las organizaciones aprovechar la potencia de múltiples máquinas y ubicaciones para lograr un alto rendimiento, tolerancia a fallos y escalabilidad en sus entornos informáticos. Sin embargo, el diseño y la gestión de sistemas distribuidos pueden ser complejos y exigir un examen minucioso de los protocolos de comunicación, la coherencia de los datos y las estrategias de tolerancia a fallos. Veamos las ventajas e inconvenientes de utilizar un sistema distribuido.

## Ventajas de un sistema distribuido

Los sistemas informáticos distribuidos tienen las siguientes ventajas:

- **Flexibilidad** - Puede ajustar las características de cada servidor al componente que vaya a alojar. Por ejemplo, un servidor de aplicaciones puede necesitar más memoria o CPU; un servidor de base de datos necesita más disco y rendimiento de E/S.

- **Gran volumen** - Puede ejecutar múltiples copias de componentes para la tolerancia a fallos o para manejar mayores cantidades de tráfico.

- **Redundancia de nodos** - Los nodos de un sistema distribuido proporcionan redundancia, de modo que si uno falla, hay otros nodos disponibles para intervenir y ocupar su lugar.

- **Toleranciaa los fallos** - Al reducir los riesgos asociados a la existencia de un único punto de fallo, los sistemas distribuidos mejoran la fiabilidad y la tolerancia a los fallos.

## Desventajas de un sistema distribuido

Los sistemas informáticos distribuidos presentan las siguientes desventajas:

- **Mayor complejidad** - En comparación con los entornos informáticos convencionales, los sistemas distribuidos son más difíciles de diseñar, administrar y comprender.

- **Trabajo extra** - Los componentes tienen que hacer un trabajo extra para encontrarse entre ellos.

- **Introducción potencial de nuevos problemas** - Los problemas de red podrían introducir un nuevo punto de fallo en su aplicación.

- **Posible introducción de retrasos** - La red también podría introducir algunos retrasos.

- **Aumento de los costes** - En contraste con los sistemas centralizados, la escalabilidad de los sistemas distribuidos permite a los administradores añadir rápidamente más capacidad según sea necesario, lo que potencialmente puede aumentar los gastos.

Por un lado, si está diseñando una aplicación que necesita escalarse, debe tener en cuenta la arquitectura de los sistemas distribuidos desde el principio. No debe asumir que todo está en el mismo servidor que usted. Intenta encontrar alguna forma de que cada componente descubra a los demás (desde un archivo de configuración hasta un catálogo de servicios o una malla de servicios completa). Por otro lado, no compliques demasiado las cosas antes de que sea necesario. Los diseños demasiado complicados pueden ser frágiles y difíciles de mantener a largo plazo.

## Puntos clave

Los sistemas distribuidos son cruciales en diversas aplicaciones, pero requieren un diseño y una gestión cuidadosos para abordar sus complejidades y posibles retos.

- **Definición de sistemas distribuidos** - Un sistema distribuido es una colección de componentes de software que colaboran a través de servidores o nodos separados, a menudo utilizando una red compartida. Estos sistemas pretenden eliminar los cuellos de botella y los puntos únicos de fallo distribuyendo tareas y funciones entre múltiples componentes.

- **Características de los sistemas distribuidos** - Los sistemas informáticos distribuidos presentan varias características clave, como el uso compartido de recursos, la detección de errores, la transparencia, el procesamiento simultáneo, la escalabilidad y la heterogeneidad.

- **Ventajas y desventajas** - Los sistemas distribuidos ofrecen ventajas como la flexibilidad, el manejo de grandes volúmenes de tráfico, la redundancia de nodos y la tolerancia a fallos. Sin embargo, también presentan desventajas como el aumento de la complejidad, la necesidad de trabajo adicional para localizar los componentes, la posible introducción de nuevos problemas y retrasos debidos a problemas de red y el aumento de los costes asociados a la escalabilidad.
