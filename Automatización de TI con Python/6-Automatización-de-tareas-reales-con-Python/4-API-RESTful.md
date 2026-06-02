# API RESTful

**Las API RESTful** fueron conceptualizadas originalmente por Roy Thomas Fielding en su tesis doctoral de 2000. A diferencia de las API que abren puertos directamente a todo Internet y se conectan directamente, las API RESTful se basan en el protocolo HTTP. El protocolo HTTP, a su vez, puede protegerse aún más mediante HTTPS, y los puntos finales de las API pueden autenticar a los usuarios mediante tokens de autorización, claves API u otros mecanismos de seguridad. Las API RESTful utilizan solicitudes HTTP para realizar operaciones CRUD (crear, leer, actualizar, eliminar) en los recursos.

**Métodos RESTful**

Las API RESTful funcionan asociando métodos (funciones) a los recursos. Algunos de los [métodos de petición HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) más utilizados son:

[GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET): El método GET solicita una representación del recurso especificado. Las solicitudes que utilizan GET sólo deben recuperar datos.

[HEAD](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD): El método HEAD solicita una respuesta idéntica a una solicitud GET, pero sin el cuerpo de la respuesta.

[POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST): El método POST envía una entidad al recurso especificado, provocando a menudo un cambio de estado o efectos secundarios en el servidor.

[PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT): El método PUT sustituye todas las representaciones actuales del recurso de destino por la carga útil de la solicitud.

Puede utilizar GET para obtener información (lo que se denomina una "solicitud") de un punto final de API RESTful, que entregaría una representación del punto final (lo que se denomina una "respuesta"). Cada tipo de respuesta tiene asociado un código de tres dígitos; son los [códigos de respuesta HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). Es posible que ya esté familiarizado con una respuesta 404 (no encontrado). Si una solicitud tiene éxito, el código de estado de la respuesta es 200, y la respuesta contendrá una carga útil de mensaje, normalmente JSON (JavaScript Object Notation). Es importante tener en cuenta que las API RESTful casi siempre utilizan JSON, pero las API RESTful también se pueden utilizar para enviar y recibir archivos, así como para transmitir datos.

## JSON

JSON es un formato de intercambio de datos utilizado en las API RESTful para facilitar la comunicación entre clientes y servidores. En los servicios RESTful, JSON es el formato estándar para transmitir datos. Cuando un cliente realiza una solicitud, el servidor la procesa y envía una respuesta, a menudo en formato JSON. Este formato estructurado facilita el análisis sintáctico y garantiza que tanto el servidor como el cliente puedan interpretar los datos de forma coherente. Con sus pares clave-valor, JSON es legible tanto para el ser humano como para la máquina, lo que lo convierte en una opción popular para las API basadas en web.

## Protección adicional

Otra cosa importante a tener en cuenta es que las API RESTful proporcionan una capa de protección sobre los activos existentes en la nube, como una base de datos. En lugar de permitir que todo Internet consulte su base de datos, puede poner una API delante de ella y permitir que la API sirva de intermediario: un punto final asociado a ese recurso. A continuación, puede forzar la autenticación mediante un JavaScript Web Token (JWT) o un proveedor de autenticación de terceros. Esta capa de protección no sólo proporciona seguridad, sino que también separa la lógica de control de los datos, de modo que la limitación de velocidad, los análisis de uso y el almacenamiento en caché pueden añadirse para mejorar la calidad del servicio.

## Compatibilidad

Por último, las API RESTful son accesibles desde cualquier lenguaje de programación compatible con HTTP o HTTPS. Esto incluye Python, pero también C#, JavaScript, Swift, Go y muchos otros. Las API RESTful, que se basan únicamente en HTTP, permiten que cualquier ordenador moderno se comunique entre sí.

## Puntos clave

Las API RESTful son una parte fundamental y versátil del desarrollo web. Saber cómo diseñarlas, consumirlas y trabajar con ellas es esencial para crear aplicaciones web modernas, garantizando que puedan comunicarse eficazmente con otros servicios.
