# NALSD

NALSD, también conocido como diseño no abstracto de grandes sistemas, es una disciplina y un proceso inventado por Google que pretende dotar a los SREs (site reliability engineers) de la capacidad de evaluar, diseñar y valorar grandes sistemas. NALSD es el proceso de diseño de sistemas complejos y sustanciales, tales como aplicaciones de software, sistemas de hardware, o incluso estructuras organizativas, centrándose en detalles prácticos y concretos en lugar de en conceptos abstractos o teóricos. NALSD enfatiza los aspectos tangibles y del mundo real del diseño e implementación de sistemas.

NALSD combina elementos de Planificación de la capacidad, el aislamiento de componentes, y la degradación elegante del sistema que son cruciales para los sistemas de producción de alta disponibilidad.

## Características clave de NALSD

NALSD requiere que los equipos DevOps piensen en la escala y la capacidad de recuperación durante el proceso de diseño. Separa el proceso de diseño en dos fases. Las dos fases tienen las siguientes características clave:

### Fase 1: Diseño técnico

La fase 1 es un proceso iterativo que implica múltiples rondas de diseño y refinamiento. Es habitual crear prototipos, realizar estudios de viabilidad y recabar opiniones de las partes interesadas para perfeccionar continuamente el diseño técnico. En esta fase, el equipo intenta responder a dos preguntas sobre el diseño propuesto:

- ¿Es posible? ¿Funcionará el diseño?

- ¿Podemos hacerlo mejor? ¿Podemos hacerlo más rápido, más sencillo o más barato?

### Fase 2: Ampliación

En la fase 2, el equipo evalúa si el diseño del sistema es viable a escala. Consideran cómo funcionará el sistema cuando se vea sometido a aumentos significativos de carga. La escalabilidad es esencial para garantizar que el sistema pueda adaptarse al crecimiento sin una pérdida drástica de rendimiento. ¿Qué pasa si de repente se añade un millón de usuarios al sistema? ¿Cómo podrá el sistema acomodar un aumento aleatorio de usuarios?

- ¿Es viable? ¿Funcionará a escala? ¿Es rentable?

- ¿Es resistente? ¿Qué pasa si se cae la base de datos?

- ¿Podemos hacerlo mejor? ¿Hay cambios o adiciones que debamos hacer?

## Tres objetivos clave de NALSD

Tres de los objetivos clave de NALSD son los siguientes:

Planificación de la capacidad. Planificación de la capacidad es entender cómo dimensionar adecuadamente cada componente y cómo planificar adecuadamente el crecimiento. Este objetivo implica una cuidadosa supervisión, análisis del rendimiento y predicción de las tendencias de crecimiento para evitar el agotamiento de los recursos o el exceso de aprovisionamiento. Planificación de la capacidad es crucial en el diseño de NALSD, ya que implica la estimación de los recursos necesarios (CPU, memoria, almacenamiento, ancho de banda de red, etc) para satisfacer las demandas actuales y futuras.

El segundo es el aislamiento de componentes. En el diseño de NALSD, un principio fundamental es el aislamiento de componentes, destacando la importancia de diseñar cada elemento del sistema para maximizar la simplicidad, modularidad e independencia entre sí. La filosofía de "hacer una cosa y hacerla bien" anima a los desarrolladores a crear componentes que tengan un propósito claro y específico.

El objetivo final es la degradación elegante. Esta es la idea de que partes del sistema deben seguir funcionando cuando otra parte falla, en lugar de que todo falle a la vez. Por ejemplo, en una aplicación web, si un servidor de base de datos deja de estar disponible, el sistema puede cambiar a un modo de sólo lectura, permitiendo a los usuarios acceder a los datos existentes, pero bloqueando las nuevas actualizaciones hasta que la base de datos se restablezca.

## El Libro de Trabajo NALSD de Google

El Libro de Trabajo NALSD fue creado por el equipo SRE de Google. Está diseñado para ayudar a los ingenieros y desarrolladores con el diseño y la arquitectura de sistemas fiables a gran escala.

El libro de trabajo de NALSD contiene información valiosa, las mejores prácticas y directrices para el diseño y la construcción de sistemas complejos y escalables que pueden manejar grandes cargas y seguir siendo fiable. Los ingenieros a menudo se refieren a estos recursos para mejorar sus habilidades de diseño de sistemas y crear software e infraestructuras más robustas y eficientes. Si está interesado en aprender más sobre el diseño de sistemas a gran escala, este libro de trabajo es un recurso fantástico y puede encontrarlo [aquí](https://static.googleusercontent.com/media/sre.google/en//static/pdf/nalsd-workbook-letter.pdf).

## Puntos clave

He aquí tres puntos clave de esta lectura sobre NALSD:

- **Definición de NALSD:** NALSD, o Non-Abstract Large System Design, es una disciplina y un proceso introducido por Google, destinado principalmente a capacitar a los ingenieros de fiabilidad del sitio (SREs) para evaluar, diseñar y evaluar sistemas a gran escala.

- **NALSD consta de dos fases:** La fase 1 implica el perfeccionamiento continuo a través de la retroalimentación, la creación de prototipos y los estudios de viabilidad. Su objetivo es responder a las preguntas: "¿Es posible?" y "¿Podemos hacerlo mejor?" La fase 2 evalúa la viabilidad y resistencia del sistema a escala, considerando cómo funcionará bajo aumentos significativos de carga.

- **Tres objetivos clave de NALSD:** Planificación de la capacidad, aislamiento de componentes y degradación elegante son los tres objetivos de NALSD. Estos objetivos se establecen para que el sistema pueda seguir funcionando incluso cuando fallen partes individuales.

Como se mencionó anteriormente, si usted está interesado en aprender más acerca de NALSD, revise el [Libro de Trabajo de Diseño de Grandes Sistemas No-Abstractos](https://static.googleusercontent.com/media/sre.google/en//static/pdf/nalsd-workbook-letter.pdf) de Google.
