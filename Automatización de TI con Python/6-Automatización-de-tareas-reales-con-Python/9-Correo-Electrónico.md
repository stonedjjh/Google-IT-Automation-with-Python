# Introducción a la biblioteca de correo electrónico de Python

Los mensajes de correo electrónico parecen sencillos en un cliente de correo electrónico. Pero, entre bastidores, el cliente está haciendo mucho trabajo para que así sea Los mensajes de correo electrónico, incluso los que contienen imágenes y archivos adjuntos, son en realidad complicadas estructuras de texto formadas por cadenas legibles

El sitio [Protocolo simple de transmisión de correo (SMTP)](https://tools.ietf.org/html/rfc2821.html) y [Extensiones Polivalentes de Correo por Internet (MIME)](https://tools.ietf.org/html/rfc2045) definen cómo se construyen los mensajes de correo electrónico. Podrías leer la documentación de los estándares y crear mensajes de correo electrónico por tu cuenta, pero no hace falta que te tomes tantas molestias. El módulo de Python integrado en [módulo de Python incorporado en el correo electrónico](https://docs.python.org/3/library/email.html) nos permite construir fácilmente mensajes de correo electrónico.

Empezaremos usando la clase [email.message.EmailMessage](https://docs.python.org/3/library/email.message.html#email.message.EmailMessage) para crear un mensaje de correo electrónico vacío.

```PYTHON
from email.message import EmailMessage
message = EmailMessage()
print(message)
```

Como de costumbre, imprimir el objeto mensaje nos da la representación de cadena de ese objeto. La biblioteca de correo electrónico tiene una función que convierte el complejo objeto EmailMessage en algo que es bastante legible para los humanos. Como este es un mensaje vacío, no hay nada que ver todavía. Intentemos añadir el remitente y el destinatario al mensaje y veamos cómo queda.

Definiremos un par de variables para poder reutilizarlas más tarde.

```PYTHON
sender = "me@example.com"
recipient = "you@example.com"
```

Y ahora, añádelas a los campos FROM y TO del mensaje.

```PYTHON
message['From'] = sender
message['To'] = recipient
print(message)


From: me@example.com
To: you@example.com
```

Muy bien Esto empieza a parecerse un poco más a un mensaje de correo electrónico. ¿Y el asunto?

```PYTHON
message['Subject'] = 'Greetings from {} to {}!'.format(sender, recipient)
print(message)

From: me@example.com
To: you@example.com
Subject: Greetings from me@example.com to you@example.com!
```

**FROM**, **To** y **Subject** son ejemplos de **campos de cabecera de correo electrónico**. Son **pares clave-valor** de etiquetas e instrucciones utilizadas por los clientes y servidores de correo electrónico para enrutar y mostrar el mensaje. Son independientes del **cuerpo** del **mensaje**, que es el contenido principal del mensaje.

Vamos a añadir un cuerpo de mensaje

```PYTHON
body = """Hey there!

I'm learning to send emails using Python!"""
message.set_content(body)
```

Muy bien, ¿qué aspecto tiene?

```PYTHON
print(message)

From: me@example.com
To: you@example.com
Subject: Greetings from me@example.com to you@example.com!
MIME-Version: 1.0
Content-Type: text/plain; charset="utf-8"
Content-Transfer-Encoding: 7bit

Hey there!
I'm learning to send email using Python!
```

¡El mensaje tiene un cuerpo! El método `set_content( )` también añadió automáticamente un par de cabeceras que la infraestructura de correo electrónico utilizará cuando envíe este mensaje a otra máquina. ¿Recuerdas que en un curso anterior hablamos de **la codificación de caracteres**? Las cabeceras **Content-Type** y **Content-Transfer-Encoding** indican a los clientes y servidores de correo electrónico cómo interpretar los bytes de este mensaje de correo electrónico en una cadena. Ahora bien, ¿qué pasa con esta otra cabecera? ¿Qué es MIME? Lo aprenderemos a continuación.

## Añadir anexos

Recuerda que los mensajes de correo electrónico están formados completamente por cadenas. Cuando añades un adjunto a un correo electrónico, sea del tipo que sea, se codifica como texto. El estándar **MIME (Multipurpose Internet Mail Extensions)** se utiliza para codificar todo tipo de archivos como cadenas de texto que pueden enviarse por correo electrónico.

Veamos cómo funciona.

Para que el destinatario del mensaje sepa qué hacer con un archivo adjunto, hay que etiquetarlo con un **tipo** y **subtipo MIME** que le indique qué tipo de archivo le estamos enviando. **La Autoridad de Asignación de Números de Internet [(IANA)](iana.org)**[alberga un registro de tipos MIME válidos](https://www.iana.org/assignments/media-types/media-types.xhtml). Si conoce el tipo y subtipo correctos de los archivos que va a enviar, puede utilizar esos valores directamente. Si no lo sabes, puedes usar el módulo mimetypes de Python para hacer una buena suposición

```PYTHON
import os.path
attachment_path = "/tmp/example.png"
attachment_filename = os.path.basename(attachment_path)
import mimetypes
mime_type, _ = mimetypes.guess_type(attachment_path)
print(mime_type)
image/png
```

Bien, esa cadena **mime_type** contiene el tipo MIME y el subtipo, separados por una barra. El tipo **EmailMessage** necesita un tipo MIME y subtipos como cadenas separadas, así que dividamos esto:

```PYTHON
mime_type, mime_subtype = mime_type.split('/', 1)
print(mime_type)
image
print(mime_subtype)
png
```

Ahora, ¡por fin! Añadamos el adjunto a nuestro mensaje y veamos qué aspecto tiene.

```PYTHON
with open(attachment_path, 'rb') as ap:
message.add_attachment(ap.read(),
maintype=mime_type,
subtype=mime_subtype,
filename=os.path.basename(attachment_path))

print(message)
Content-Type: multipart/mixed; boundary="===============5350123048127315795=="

--===============5350123048127315795==
Content-Type: image/png
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename="example.png"
MIME-Version: 1.0

iVBORw0KGgoAAAANSUhEUgAAASIAAABSCAYAAADw69nDAAAACXBIWXMAAAsTAAALEwEAmpwYAAAg
AElEQVR4nO2dd3wUZf7HP8/M9k2nKIJA4BCUNJKgNJWIBUUgEggCiSgeVhA8jzv05Gc5z4KHiqin
eBZIIBDKIXggKIeCRCAhjQAqx4UiCARSt83uzDy/PzazTDZbwy4BnHde+9qZydNn97Pf5/uUIZRS
(...We deleted a bunch of lines here...)
wgAAAABJRU5ErkJggg==

--===============5350123048127315795==--
```

Todo el mensaje puede ser serializado como una cadena de texto, ¡incluyendo la imagen que adjuntamos! El mensaje de correo electrónico en su conjunto tiene el tipo MIME "multipart/mixed". Cada parte del mensaje tiene su propio tipo MIME. El cuerpo del mensaje sigue siendo una parte "text/plain", y la imagen adjunta es una parte "image/png". Genial

Ahora, ¿cómo enviamos este mensaje de correo electrónico? Ya lo veremos

## Envío del correo electrónico a través de un servidor SMTP

Como decíamos, para enviar correos electrónicos, nuestros ordenadores utilizan el
[Protocolo simple de transmisión de correo (SMTP)](https://tools.ietf.org/html/rfc2821.html). Este protocolo especifica cómo los ordenadores pueden enviarse correos electrónicos entre sí. Hay que seguir ciertos pasos para hacerlo correctamente. Pero, como de costumbre, no lo haremos manualmente; enviaremos el mensaje utilizando el módulo incorporado de Python [smtplib de Python](https://docs.python.org/3/library/smtplib.html). Empecemos importando el módulo.

`import smtplib`

Con smtplib, crearemos un objeto que representará nuestro servidor de correo, y manejará el envío de mensajes a ese servidor. Si estás usando un ordenador Linux, puede que ya tengas configurado un servidor SMTP como postfix o sendmail. Pero puede que no. Creemos un objeto smtplib.SMTP e intentemos conectarnos a la máquina local.

```PYTHON
mail_server = smtplib.SMTP('localhost')

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  (...We deleted a bunch of lines here...)
ConnectionRefusedError: [Errno 61] Connection refused
```

¡Uy! Este error significa que no hay ningún servidor SMTP local configurado. Pero que no cunda el pánico Aún puedes conectarte al servidor SMTP de tu dirección de correo electrónico personal. La mayoría de los servicios de correo electrónico personales tienen instrucciones para enviar correo electrónico a través de SMTP; sólo tienes que buscar el nombre de tu servicio de correo electrónico y "Configuración de la conexión SMTP".

Al configurar esto, hay un par de cosas que probablemente tendrás que hacer: Utilizar una capa de transporte segura y autenticarte en el servicio utilizando un nombre de usuario y una contraseña. Veamos qué significa esto en la práctica.

Puedes conectarte a un servidor SMTP remoto utilizando **Seguridad de la capa de transporte (TLS)**. Una versión anterior del protocolo TLS se llamaba **Capa de sockets seguros (SSL)**, y a veces verás que TLS y SSL se usan indistintamente. Este SSL/TLS es el mismo protocolo que se utiliza para añadir una capa de transmisión segura a HTTP, convirtiéndolo en HTTPS. Dentro de smtplib, hay dos clases para realizar conexiones a un servidor SMTP: La clase [Clase SMTP](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) hará una conexión SMTP directa, y la clase [Clase SMTP_SSL](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL) hará una conexión SMTP sobre SSL/TLS. Así:

`mail_server = smtplib.SMTP_SSL('smtp.example.com')`

Si quieres ver los mensajes SMTP que están siendo enviados de un lado a otro por el módulo smtplib entre bastidores, puedes establecer el nivel de depuración en el objeto SMTP o SMTP_SSL. Los ejemplos de esta lección no mostrarán la salida de depuración, pero puede que te resulte interesante

`mail_server.set_debuglevel(1)`

Ahora que hemos establecido una conexión con el servidor SMTP, lo siguiente que tenemos que hacer es autenticarnos en el servidor SMTP. Típicamente, los proveedores de correo electrónico quieren que proporcionemos un nombre de usuario y una contraseña para conectarnos. Pongamos la contraseña en una variable para que no sea visible en la pantalla.

```PYTHON
import getpass
mail_pass = getpass.getpass('Password? ')
Password?
```

El ejemplo anterior utiliza el módulo [módulo getpass](https://docs.python.org/3/library/getpass.html) para que los transeúntes no vean la contraseña en la pantalla. Pero cuidado, la variable mail_pass sigue siendo una cadena normal

```PYTHON
print(mail_pass)
It'sASecr3t!
```

Ahora que tenemos configurados el usuario y la contraseña de correo electrónico, podemos autenticarnos en el servidor de correo electrónico utilizando el método
[del objeto SMTP](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.login).

```PYTHON
mail_server.login(sender, mail_pass)
(235, b'2.7.0 Accepted')
```

Si el intento de autenticación tiene éxito, el método devolverá una tupla con el código de estado [Código de estado SMTP](https://tools.ietf.org/html/rfc4954#section-6) y un mensaje explicando la razón del estado. Si el intento de inicio de sesión falla, el módulo generará un error [SMTPAuthenticationError](https://docs.python.org/3.8/library/smtplib.html#smtplib.SMTPAuthenticationError) excepción.

Si escribieras un script para enviar un mensaje de correo electrónico, ¿cómo manejarías esta excepción?

**Envío del mensaje:**

Muy bien Estamos conectados y autenticados en el servidor SMTP. Ahora, ¿cómo enviamos el mensaje?

```PYTHON
mail_server.send_message(message)
{}
```

Bueno, ¡esto último fue bastante fácil! Primero hicimos la parte difícil El método
[método send_message](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.send_message) devuelve un diccionario de los destinatarios que no pudieron recibir el mensaje. Nuestro mensaje fue entregado con éxito, por lo que send_message devolvió un diccionario vacío. Finalmente, ahora que el correo ha sido enviado, cerremos la conexión con el servidor de correo.

`mail_server.quit()`

¡Y ahí lo tienes! Hemos cubierto mucho en esta lección, así que recapitulemos Primero, construimos un mensaje de correo electrónico utilizando el módulo incorporado [módulo de correo](https://docs.python.org/3/library/email.html)'s
[EmailMessage](https://docs.python.org/3/library/email.message.html). A continuación, añadimos un archivo adjunto a nuestro mensaje con la ayuda del módulo incorporado [módulo mimetypes](https://docs.python.org/3/library/mimetypes.html). Por último, nos conectamos a un servidor SMTP y enviamos el correo electrónico utilizando la clase [SMTP_SSL del módulo smtplib](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL).

¿Tenías idea de que todo esto estaba ocurriendo detrás de un simple mensaje de correo electrónico?
