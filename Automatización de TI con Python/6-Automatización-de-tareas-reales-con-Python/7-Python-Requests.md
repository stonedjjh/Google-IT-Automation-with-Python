# Python Requests

Hasta ahora, hemos visto cómo podemos serializar los datos que tenemos en nuestros programas y convertirlos en un formato que podamos almacenar en disco. Una vez que los datos están almacenados, otro proceso puede abrir esos archivos, de-serializarlos, y seguir desde allí.

Esto funciona, pero sólo si el otro proceso tiene acceso al mismo sistema de archivos que utilizaste para almacenar tus datos. ¿Y si quisieras enviar un mensaje a otro ordenador en otra red? ¡HTTP al rescate!

Recuerda que **HTTP (HyperText Transfer Protocol)** es el protocolo de la World Wide Web. Cuando visitas una página web con tu navegador, éste realiza una serie de **peticiones HTTP** a servidores web en algún lugar de Internet. Esos servidores responderán con **respuestas HTTP**. Así es también como vamos a enviar y recibir mensajes con las aplicaciones web desde nuestro código.

La biblioteca [Librería Python Requests](https://requests.readthedocs.io/) hace súper fácil escribir programas que envíen y reciban HTTP. En lugar de tener que entender el protocolo HTTP en gran detalle, puedes simplemente hacer conexiones HTTP muy simples usando objetos Python, y luego enviar y recibir mensajes usando los métodos de esos objetos. Veamos un ejemplo:

```python
>>> import requests
>>> response = requests.get('https://www.google.com')
```

¡Eso es! ¡Esa fue una petición básica para una página web! Usamos la librería Requests para hacer una petición **HTTP GET** para una _URL_ específica , o **Uniform Resource Locator**. La URL le dice a la biblioteca Requests el nombre del recurso(**www.google.com**) y qué protocolo usar para obtener el recurso(**https://**). El resultado que obtenemos es un objeto de tipo [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response).

Muy bien, ¿con qué respondió el servidor web? Echemos un vistazo a los primeros 300 caracteres del archivo [Respuesta.texto](https://requests.readthedocs.io/en/master/api/#requests.Response.text)

```python
>>> print(response.text[:300])
<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="de"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="dZfbIAn803LDGXS9
```

Ahora, puede ser difícil para usted leer el [HTML (Lenguaje de marcado de hipertexto)](https://html.spec.whatwg.org/multipage/) que fue devuelto en esta respuesta, pero su navegador web sabe cómo convertirlo en una página web de aspecto familiar.

Incluso con este simple ejemplo, ¡el módulo Requests ha hecho un montón de trabajo por nosotros! No hemos tenido que escribir ningún código para encontrar el servidor web, hacer una conexión de red, construir un mensaje HTTP, esperar una respuesta, o decodificar la respuesta. No es que el HTML no sea suficientemente complicado por sí mismo, pero veamos los primeros bytes del mensaje en [bruto](https://requests.readthedocs.io/en/master/api/#requests.Response.raw) que recibimos del servidor:

```python
>>> response = requests.get('https://www.google.com', stream=True)
>>> print(response.raw.read()[:100])
b'\x1f\x8b\x08\x00\x00\x00\x00\x00\x02\xff\xc5Z\xdbz\x9b\xc8\x96\xbe\xcfS`\xf2\xb5-\xc6X\x02$t\xc28\xe3v\xdc\xdd\xee\xce\xa9\xb7\xdd;\xe9\x9d\xce\xf6W@\t\x88\x11`@>D\xd6\x9b\xce\xe5<\xc3\\\xcd\xc5\xfc\xab8\x08\xc9Nz\x1f.&\x8e1U\xb5j\xd5:\xfc\xb5jU\x15\x87;^\xe2\x16\xf7)\x97\x82b\x1e\x1d\x1d\xd2S'
```

¿Qué es todo eso? La respuesta estaba **comprimida** con [gzip](https://www.gzip.org/), así que tuvo que ser descomprimida antes de que pudiéramos leer el texto del HTML. ¡Una cosa más que la biblioteca Requests maneja por nosotros!

El [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response) también contiene la petición exacta que se creó para nosotros. Podemos revisar los encabezados almacenados en nuestro objeto para ver que el módulo Requests le dijo al servidor web que estaba bien comprimir el contenido:

```python
>>> response.request.headers['Accept-Encoding']
'gzip, deflate
```

Y luego el servidor nos dijo que el contenido había sido realmente comprimido.

```python
>>> response.headers['Content-Encoding']
'gzip'
```

Y todo esto ocurrió por defecto, sin que tuviéramos que hacer nada especial para que funcionara. Increíble, ¿verdad?

## Operaciones útiles para peticiones en Python

Hay un montón de cosas que podemos hacer con Python Requests. Cubriremos algunas de las características más importantes aquí y te daremos indicaciones para obtener más información al final.

En primer lugar, ¿cómo sabemos si una petición que hemos hecho ha recibido una respuesta satisfactoria? Puedes comprobar el valor de [Response.ok](https://requests.readthedocs.io/en/master/api/#requests.Response.ok), que será **True** si la respuesta fue buena, y **False** si no lo fue.

```PYTHON
>>> response.ok
True
```

Ahora, ten en cuenta que esto sólo te dirá si el servidor web dice que la respuesta cumplió con éxito la solicitud. El módulo de respuesta no puede determinar si los datos que recibiste son del tipo que esperabas. Tendrás que comprobarlo tú mismo

Si el booleano no es lo suficientemente específico para sus necesidades, puede obtener el [Código de respuesta HTTP](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml) que se devolvió consultando [Response.status_code](https://requests.readthedocs.io/en/master/api/#requests.Response.ok):

```PYTHON
>>> response.status_code
200
```

¡Excelente! Para escribir código mantenible y estable, siempre querrás comprobar tus respuestas para asegurarte de que han tenido éxito antes de intentar seguir procesándolas. Por ejemplo, podrías hacer algo como esto:

```PYTHON
response = requests.get(url)
if not response.ok:
    raise Exception("GET failed with status code {}".format(response.status_code))
```

Pero en realidad no necesitas hacer eso. ¡Requests nos tiene cubiertos aquí también! Podemos utilizar el método [Response.raise_para_estado()](https://requests.readthedocs.io/en/master/api/#requests.Response.raise_for_status) que lanzará una excepción **HTTPError** sólo si la respuesta no ha sido satisfactoria.

```PYTHON
response = requests.get(url)
response.raise_for_status()
```

A continuación, veremos los diferentes tipos de métodos de petición HTTP que podemos realizar utilizando este práctico módulo de peticiones.

## Métodos HTTP GET y POST

HTTP soporta varios [métodos HTTP](https://tools.ietf.org/html/rfc7231#section-4.3), como GET, POST, PUT y DELETE. Vamos a dedicar tiempo a las dos peticiones HTTP más comunes: GET y POST.

El [método HTTP GET](https://tools.ietf.org/html/rfc7231#section-4.3.1), por supuesto, recupera u **obtiene** el recurso especificado en la URL. Al enviar una petición GET al servidor web, le estás pidiendo al servidor que obtenga el recurso por ti. Cuando navegas por la web, la mayor parte de lo que haces es utilizar tu navegador para enviar un montón de peticiones GET para el texto, imágenes, vídeos, etc. que tu navegador te mostrará.

Una petición GET puede tener **parámetros**. ¿Has visto alguna vez una URL con este aspecto?

`https://example.com/path/to/api/cat_pictures?search=grey+kitten&max_results=15`

El signo de interrogación separa el recurso URL de los parámetros del recurso. Estos parámetros son uno o más pares clave-valor, formateados como una [cadena de consulta](https://en.wikipedia.org/wiki/Query_string). En el ejemplo anterior, el parámetro de **búsqueda** es "grey+kitten", y el parámetro **max_results** es 15.

Pero no tienes que escribir tu propio código para crear una URL como esa. Con [requests.get()](https://requests.readthedocs.io/en/master/api/#requests.get)
puedes proporcionar un diccionario de parámetros, y el módulo Requests construirá la URL correcta para ti

```PYTHON
>>> p = {"search": "grey kitten",
...      "max_results": 15}
>>> response = requests.get("https://example.com/path/to/api", params=p)
>>> response.request.url
'https://example.com/path/to/api?search=grey+kitten&max_results=15'
```

Puedes notar que el uso de parámetros en Requests es otra forma de serialización de datos. Las cadenas de consulta son útiles cuando queremos enviar pequeños fragmentos de información, pero a medida que nuestros datos se vuelven más complejos, puede resultar difícil representarlos utilizando cadenas de consulta.

Una alternativa en ese caso es utilizar el [método HTTP POST](https://tools.ietf.org/html/rfc7231#section-4.3.3). Este método envía datos a un servicio web. Cada vez que rellenas un formulario web y pulsas un botón para enviarlo, estás utilizando el método POST para devolver esos datos al servidor web. Este método suele utilizarse cuando hay muchos datos que transmitir.

En nuestros scripts, una petición POST se parece mucho a una petición GET. En lugar de establecer el atributo **params**, que se convierte en una cadena de consulta y se anexa a la URL, utilizamos el atributo **data**, que contiene los datos que se enviarán como parte de la solicitud POST.

```PYTHON
>>> p = {"description": "white kitten",
...      "name": "Snowball",
...      "age_months": 6}
>>> response = requests.post("https://example.com/path/to/api", data=p)
```

Veamos la URL generada para esta petición:

```PYTHON
>>> response.request.url
'https://example.com/path/to/api'
```

¿Ves cómo ahora la URL de este POST es mucho más simple? WHERE ¿dónde van todos los parámetros? Forman parte del **cuerpo** del mensaje HTTP. Podemos verlos comprobando el atributo **body**.

```PYTHON
>>> response.request.body
'description=white+kitten&name=Snowball&age_months=6'
```

¡Ah, ja! Ahí están

Así que, si necesitamos enviar y recibir datos de un servicio web, podemos convertir nuestros datos en diccionarios y luego pasarlos como el atributo **data** de una petición POST.

Hoy en día, es súper común enviar y recibir datos específicamente en formato JSON, por lo que el módulo Requests puede hacer la conversión directamente por nosotros, usando el parámetro **json**.

```PYTHON
>>> response = requests.post("https://example.com/path/to/api", json=p)
>>> response.request.url
'https://example.com/path/to/api'
>>> response.request.body
b'{"description": "white kitten", "name": "Snowball", "age_months": 6}'
```

Y hasta aquí nuestra breve introducción al módulo Requests. Si quieres aprender más, siéntete libre de trabajar con el módulo [Requests Quickstart](https://requests.readthedocs.io/en/master/user/quickstart/).

En el proyecto al final de este módulo, utilizarás el módulo Requests para interactuar con una aplicación web. Esta sencilla aplicación fue creada usando el framework web Django. ¿Qué es eso exactamente? Sigue leyendo para saber más
