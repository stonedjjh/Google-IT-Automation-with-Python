# ¿Qué es la arquitectura REST?

REST son las siglas de Representational State Transfer. La arquitectura REST es un estilo arquitectónico para diseñar aplicaciones y servicios web en red. Se inventó como una forma estándar de comunicación entre clientes y servidores a través de Internet.

REST está diseñado para ser apátrida, lo que significa que el servidor no tiene que recordar ninguna información sobre el cliente entre peticiones. Cada solicitud contiene todos los parámetros y datos necesarios para que el servidor la satisfaga.

## Restricciones de la arquitectura REST

Cada una de las seis restricciones o principios de REST sirve a un propósito específico a la hora de guiar el diseño de sistemas RESTful, contribuyendo a la escalabilidad, simplicidad e interoperabilidad general de la arquitectura. Las seis restricciones son

- **Interfaz uniforme:** debe haber métodos coherentes para que los clientes accedan a los recursos del servidor y los modifiquen utilizando convenciones HTTP (Protocolo de transferencia de hipertexto) estándar.

- **Sin estado** - Toda la información que necesita el servidor para procesar la solicitud debe estar en la solicitud. No debe haber información sobrante en el servidor entre peticiones.

- **Almacenable en caché:** cada respuesta del servidor debe indicar si los datos pueden almacenarse en caché en el cliente y el tiempo necesario para ello.

- **Cliente-servidor** - El cliente y el servidor pueden evolucionar de forma independiente. La interfaz REST sirve de "contrato" entre ambos.

- **Sistema por capas** - Una aplicación debe dividirse en capas. Cada capa de la aplicación se ocupa de un aspecto concreto (acceso a datos, lógica empresarial, presentación, etc.) y actúa independientemente de las demás capas.

- **Código bajo demanda (opcional)** - Los servidores también pueden proporcionar código para ser ejecutado en el cliente. Esto permite al cliente cambiar su comportamiento de forma dinámica.

## Protocolo HTTP con REST

REST también está diseñado para ejecutarse sobre HTTP. Este diseño permite a clientes y servidores comunicarse a través de la Internet pública utilizando convenciones HTTP estándar. Las empresas suelen publicar su API REST (Interfaz de programación de aplicaciones) para que los desarrolladores puedan hacer uso de ella. Casi cualquier lenguaje de programación es capaz de hablar HTTP, por lo que puede utilizar su lenguaje favorito, como Python, para realizar llamadas a la API REST.

Toda la interacción entre el cliente y el servidor tiene lugar a través de HTTP, utilizando las características estándar de HTTP: verbos, cabeceras y cargas útiles de datos. Casi todo lo que el servidor necesita saber está incluido en la propia URL de la solicitud.

Por ejemplo, una aplicación para compartir fotos puede enviar una serie de peticiones HTTP a un servidor API REST con el siguiente aspecto (el comando aparece en primer lugar y la acción que realiza se indica después del guión):

- `GET /api/v1/albums` - obtener la lista de álbumes de fotos

- `GET /api/v1/albums/1234/pictures` - obtener la lista de fotos del álbum 1234

- `GET /api/v1/pictures/5678` - obtener los detalles de la foto 5678

- `GET /api/v1/pictures/5678/comments` - obtener los comentarios de la foto 5678

HTTP permite a los clientes GET, PUT y DELETE. Los clientes también pueden POSTAR consultas con datos complejos, como realizar una búsqueda o transferir dinero entre cuentas. El verbo PATCH permite a los clientes actualizar un recurso simplemente enviando lo que ha cambiado.

Las API REST suelen permitir al cliente ajustar su comportamiento enviando cabeceras adicionales con la solicitud. Las cabeceras pueden incluir autenticación, habilitar funciones opcionales o permitir al cliente solicitar que el servidor envíe datos en formatos específicos (por ejemplo, JavaScript Object Notation, JSON o eXtensible Markup Language).

El cliente puede enviar datos en el cuerpo de su solicitud, y el servidor responde con datos en el cuerpo de la respuesta. El formato de los datos se controla mediante una cabecera (véase más arriba).

## ¿Qué es el modelo de madurez de Richardson?

El Modelo de Madurez de Richardson, también conocido como RMM, es un marco que categoriza y describe diferentes niveles de implementación de API RESTful basados en su adherencia a las seis restricciones mencionadas anteriormente en esta lectura. El RMM es una forma de evaluar la sofisticación de una API REST basándose en su grado de cumplimiento de las restricciones REST.

El modelo de madurez de Richardson consta de cuatro niveles, cada uno de los cuales representa un nivel progresivo de adhesión a los principios de REST:

- **Nivel 0:** un único URI (identificador uniforme de recursos) y un único verbo (normalmente GET o POST)

- **Nivel 1:** varias URI, pero un único verbo

- **Nivel 2:** utiliza URI y varios métodos, pero no es HATEOAS (hipermedia como motor del estado de la aplicación)

- **Nivel 3** - HATEOAS completo

HATEOAS indica que las respuestas del servidor deben incluir hipervínculos para que el cliente acceda a recursos relacionados. Por ejemplo, en el ejemplo de aplicación de galería de imágenes anterior, la solicitud GET para álbumes debe devolver una lista de álbumes. Cada álbum debe incluir su nombre, ID y enlaces para recuperar detalles del álbum, comentarios e imágenes. Con una implementación REST de nivel 3 completa, el cliente no necesitaría codificar los URI de los recursos que necesita. Los URI se pueden encontrar en las respuestas del servidor.

Para más información sobre cómo crear APIs REST en Python, [consulta](https://auth0.com/blog/developing-restful-apis-with-python-and-flask/) este enlace. Si está interesado en obtener más información sobre las API de REST con GCP, haga clic en [este](https://medium.com/mdblog/creating-a-serverless-rest-api-with-gcp-32cc62188a03) enlace.

## Puntos clave

La arquitectura REST se basa en seis restricciones clave, incluyendo una interfaz uniforme para interacciones consistentes, ausencia de estado para una comunicación eficiente, almacenamiento en caché para mejorar el rendimiento, separación de las preocupaciones del cliente y el servidor, organización del sistema en capas, y la capacidad opcional para que los servidores proporcionen código ejecutable a los clientes. Las API REST suelen estar diseñadas para ejecutarse sobre el protocolo HTTP, utilizando funciones HTTP estándar para la comunicación. Las API son difíciles de modificar una vez publicadas y utilizadas. Invierta tiempo en crear API limpias, racionales y ampliables desde el principio.

## Uso de API REST para acceder a datos web

Acceder a datos web mediante API RESTful implica una serie de pasos que permiten a los clientes (como aplicaciones web o apps para móviles) comunicarse con los servidores y recuperar información. Piense en las API como si fuera el camarero de un restaurante. El camarero toma los pedidos del cliente (front end). Después, el camarero comunica el pedido a los trabajadores de la cocina (back end) y vuelve al cliente con su comida (respuesta de la API). Estos son los pasos clave para acceder a datos web mediante API RESTful:

1. **Identifique el punto final de la API:** Determine el punto final específico de la API o el Identificador Uniforme de Recursos (URI) que corresponde al recurso o a los datos a los que desea acceder. El punto final es la URL a la que enviará su solicitud HTTP.

2. **Seleccione el método HTTP apropiado:** Elija el método HTTP apropiado para la acción que desea realizar en el recurso:
   1. **GET:** Recuperar datos del recurso.

   2. **POST:** Crear un nuevo recurso.

   3. **PUT:** Actualizar un recurso existente o crearlo si no existe (reemplazar todo el recurso).

   4. **PATCH:** Actualiza parcialmente un recurso existente.

   5. **DELETE:** Elimina un recurso.

3. **Configurar las cabeceras de lapetición:**Incluya las cabeceras necesarias en su petición HTTP. Las cabeceras comunes incluyen tokens de autenticación (por ejemplo, claves API o tokens OAuth), tipo de contenido y cabeceras accept (que indican el formato de respuesta deseado, como JSON o XML).

4. **Preparar el cuerpo de la solicitud:**Para métodos HTTP como POST y PUT, es posible que tenga que preparar un cuerpo de solicitud que contenga los datos que se enviarán al servidor. El formato del cuerpo de la solicitud depende de la documentación de la API.

5. **Envíe la solicitud HTTP:**Utilice un lenguaje o herramienta de programación (por ejemplo, la biblioteca de solicitudes de Python, la API Fetch de JavaScript o bibliotecas de cliente de API especializadas) para enviar la solicitud HTTP al punto final de la API. Incluya el método HTTP elegido, las cabeceras y el cuerpo de la solicitud según corresponda.

6. **Recibir la respuesta HTTP:**El servidor procesará su solicitud y responderá con una respuesta HTTP. Esta respuesta incluirá
   1. Código de estado: Indica el resultado de la solicitud (por ejemplo, 200 para éxito, 404 para no encontrado, 500 para error del servidor)

   2. Cabeceras de respuesta: Contiene metadatos sobre la respuesta

   3. Cuerpo de la respuesta: Contiene los datos solicitados, a menudo en un formato estructurado como JSON o XML

7. **Manejar la respuesta:**
   1. Analiza el cuerpo de la respuesta para extraer los datos que necesitas. El formato dependerá de la documentación de la API y del encabezado del tipo de contenido (normalmente JSON o XML).

   2. Compruebe el código de estado para determinar si la solicitud se ha realizado correctamente o si se ha producido un error.

   3. Gestione los errores con elegancia examinando el cuerpo de la respuesta o el código de estado y proporcionando la información adecuada al usuario.

8. **Implementar la paginación y el filtrado (opcional):**si la API admite la paginación o el filtrado, puede incluir parámetros de consulta en la URL para solicitar subconjuntos específicos de datos o controlar el número de registros devueltos.

9. **Autenticación y autorización:**asegúrese de que ha implementado los mecanismos de autenticación y autorización necesarios que exige la API. Esto puede implicar la inclusión de tokens o credenciales de autenticación en las cabeceras de las solicitudes.

10. **Gestión de errores:**implemente una lógica de gestión de errores para gestionar posibles problemas, como errores de red, respuestas no válidas o códigos de estado HTTP que indiquen errores (por ejemplo, códigos 4xx y 5xx). Proporcione mensajes de error informativos al usuario.

11. **Limitación de velocidad (si procede):**Respete los límites de velocidad impuestos por la API para evitar solicitudes excesivas. Aplique estrategias de limitación de velocidad en su extremo para asegurarse de que no supera la velocidad de solicitud permitida.

12. Si necesita acceder a más datos o realizar acciones adicionales,repitalos pasos con los puntos finales, métodos y parámetros de API adecuados.

Si sigue estos pasos, podrá acceder de forma eficaz a datos web mediante API RESTful e integrar esos datos en sus aplicaciones o servicios web. Es esencial consultar la documentación de la API para obtener detalles específicos sobre las URL de los puntos finales, los formatos de solicitud, la autenticación y otros requisitos.
