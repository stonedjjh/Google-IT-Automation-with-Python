# Planteamiento del problema del proyecto

Bien, éste es el escenario:

Trabajas para una frutería online, y necesitas desarrollar un sistema que actualice la información del catálogo con los datos proporcionados por tus proveedores. Cuando cada proveedor tiene nuevos productos para tu tienda, te da una imagen y una descripción de cada producto.

Dado un montón de imágenes y descripciones de cada uno de los nuevos productos, usted:

- Sube los nuevos productos a tu tienda online. Las imágenes y las descripciones deben cargarse por separado, utilizando dos puntos finales web diferentes.

- Enviar un informe al proveedor para informarle de lo que ha importado.

Dado que este proceso es clave para el éxito de su negocio, debe asegurarse de que siga funcionando Por lo tanto, también

- Ejecutar un script en su servidor web para monitorear la salud del sistema.

- Enviar un correo electrónico con una alerta si el servidor no está sano en algún momento.

Esperamos que este resumen te haya ayudado a empezar a pensar en cómo abordarás esta tarea. En caso de que te sientas un poco asustado, no te preocupes, ¡definitivamente puedes hacerlo! Tienes todas las herramientas necesarias, y la descripción del laboratorio explicará con más detalle lo que tienes que hacer.

A continuación, te daremos algunos consejos que pueden ayudarte.

## Evaluación de Qwiklabs: Automatizar las actualizaciones de la información del catálogo

**Introducción:**

Usted trabaja para una frutería online y necesita desarrollar un sistema que actualice la información del catálogo con los datos proporcionados por sus proveedores. Los proveedores envían los datos como imágenes grandes con una descripción asociada de los productos en dos archivos (.TIF para la imagen y .txt para la descripción). Las imágenes deben convertirse en imágenes jpeg más pequeñas y el texto debe convertirse en un archivo HTML que muestre la imagen y la descripción del producto. El contenido del archivo HTML debe cargarse en un servicio web que ya se esté ejecutando con Django. También es necesario recoger el nombre y el peso de todas las frutas de los archivos .txt y utilizar una petición Python para subirlo a su servidor Django.

Crearás un script Python que procesará las imágenes y descripciones y luego actualizará el sitio web de tu empresa para añadir los nuevos productos.

Una vez completada la tarea, el proveedor recibirá una notificación por correo electrónico en la que se indicará el peso total de la fruta (en libras) que se ha cargado. El correo electrónico debe contener un PDF adjunto con el nombre de la fruta y su peso total (en libras).

Por último, paralelamente a la ejecución de la automatización, queremos comprobar la salud del sistema y enviar un correo electrónico si algo va mal.

### Lo que hay que hacer

- Escribir un script que resuma y procese los datos de ventas en diferentes categorías

- Generar un PDF utilizando Python

- Enviar automáticamente un PDF por correo electrónico

- Escribir un script para comprobar el estado de salud del sistema

Por favor, tenga en cuenta que hay una prueba calificada que sigue a este laboratorio. Debe completar el laboratorio antes de realizar el cuestionario. El cuestionario evaluará su comprensión de los conceptos y procedimientos clave tratados en el laboratorio.

Esto es lo que puedes hacer para prepararte:

- Preste mucha atención a las instrucciones y explicaciones que se dan durante la sesión de laboratorio.

- Participa activamente en las actividades del laboratorio y toma notas.

- Repasa tus apuntes antes de realizar la prueba.

**Consejo profesional:**

- Puedes consultar tus apuntes de laboratorio durante el examen.

## Repuesta Planteada

136.109.36.199
changeImage.py

```PYTHON
#!/usr/bin/env python3
import os
from PIL import Image
from concurrent.futures import ProcessPoolExecutor

def rotate_image(img, degrees=270):
    """
    Rota la imagen la cantidad de grados especificada.
    Nota: Para corregir una rotación de 90° a la derecha, se rota 270° o -90°.
    """
    return img.rotate(degrees, expand=True)

def remove_extension(filename):
    """
    Elimina la extensión del nombre de archivo.
    Por ejemplo, 'image.tif' -> 'image'
    """
    return os.path.splitext(filename)[0]


def resize_image(img, size=(128, 128)):
    """
    Redimensiona la imagen al tamaño especificado (ancho, alto).
    """
    return img.resize(size)

def save_image(img, output_path, ext="jpeg"):
    """
    Guarda la imagen en la ruta destino con el formato especificado.
    Asegura que el modo sea RGB si se guarda como jpeg.
    """
    if img.mode != 'RGB':
        img = img.convert('RGB')
    img.save(output_path, ext)

def process_single_image(params):
    """
    Función orquestadora para procesar una sola imagen.
    Diseñada para ser llamada por el pool de procesos.
    """
    filename, input_dir, output_dir = params
    input_path = os.path.join(input_dir, filename)
    output_path = os.path.join(output_dir, remove_extension(filename) + ".jpeg")

    try:
        with Image.open(input_path) as img:
            #img = rotate_image(img)
            img = resize_image(img,(600,400))
            # Generalmente los iconos se piden sin extensión o con .jpg
            save_image(img, output_path)
        print(f"Procesada con éxito: {filename}")
    except Exception as e:
        print(f"Error procesando {filename}: {e}")

def run_batch_processing(input_dir, output_dir):
    """
    Recorre el directorio, filtra archivos y lanza el procesamiento paralelo.
    """
    # Crear directorio de salida si no existe
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    # Listar archivos (evitando carpetas o archivos ocultos)
    images = [f for f in os.listdir(input_dir) if f.endswith('.tiff')]

    # Preparar parámetros para el pool
    tasks = [(f, input_dir, output_dir) for f in images]

    # Ejecución en paralelo usando todos los núcleos disponibles
    with ProcessPoolExecutor() as executor:
        executor.map(process_single_image, tasks)

if __name__ == "__main__":
    # Configura aquí las rutas según las instrucciones de tu Qwiklab
    # Usualmente en estos labs es algo como 'images/' y '/opt/icons/'
    SOURCE_DIR = "./supplier-data/images/"
    DEST_DIR = "./supplier-data/images/"

    run_batch_processing(SOURCE_DIR, DEST_DIR)
```

supplier_image_upload.py

```PYTHON
#! /usr/bin/env python3

import os
import requests
from concurrent.futures import ProcessPoolExecutor

def upload(params):
    """
    Lee el archivo y lo sube vía POST.
    """
    filename, source_dir, url = params
    file_path = os.path.join(source_dir, filename)

    try:
        with open(file_path, 'rb') as f:
            # Realizar el POST
            response = requests.post(url, files={'file':f})

        # Verificación del status 201 (Created)
        if response.status_code == 201:
            return f"Éxito: {filename}"
        else:
            return f"Fallo: {filename} con status {response.status_code}"

    except Exception as e:
        return f"Error en {filename}: {e}"

def main():
    SOURCE_DIR = "./supplier-data/images/"
    # REEMPLAZA ESTO con la IP que te dio el laboratorio
    EXTERNAL_IP = "136.109.36.199"
    URL = f"http://{EXTERNAL_IP}/upload/"

    # Tu lista de archivos filtrada
    reviews = [f for f in os.listdir(SOURCE_DIR) if f.endswith('.jpeg')]

    # Preparar las tareas (tupla de parámetros)
    tasks = [(f, SOURCE_DIR, URL) for f in reviews]

    # Ejecución paralela
    with ProcessPoolExecutor() as executor:
        results = list(executor.map(upload, tasks))

    # Mostrar resultados
    for res in results:
        print(res)

if __name__ == "__main__":
    main()

```

run.py

```PYTHON
#! /usr/bin/env python3
import os
import requests
from concurrent.futures import ProcessPoolExecutor

def process_and_upload(params):
    """
    Lee el archivo, lo convierte en diccionario y lo sube vía POST.
    """
    filename, source_dir, url = params
    file_path = os.path.join(source_dir, filename)

    try:
        with open(file_path, 'r') as f:
            # .splitlines() quita los saltos de línea \n automáticamente
            lines = f.read().splitlines()

        # Estructura del diccionario según el lab
        words = lines[1].split()
        feedback_data = {
            "name": lines[0],
            "weight": int(words[0]),
            "description": " ".join(lines[2:]),
            "image_name": filename.replace(".txt", ".jpeg")
        }

        # Realizar el POST
        response = requests.post(url, json=feedback_data)

        # Verificación del status 201 (Created)
        if response.status_code == 201:
            return f"Éxito: {filename}"
        else:
            return f"Fallo: {filename} con status {response.status_code}"

    except Exception as e:
        return f"Error en {filename}: {e}"

def main():
    SOURCE_DIR = "./supplier-data/descriptions/"
    # REEMPLAZA ESTO con la IP que te dio el laboratorio
    EXTERNAL_IP = "136.109.36.199"
    URL = f"http://{EXTERNAL_IP}/fruits/"

    # Tu lista de archivos filtrada
    reviews = [f for f in os.listdir(SOURCE_DIR) if f.endswith('.txt')]

    # Preparar las tareas (tupla de parámetros)
    tasks = [(f, SOURCE_DIR, URL) for f in reviews]

    # Ejecución paralela
    with ProcessPoolExecutor() as executor:
        results = list(executor.map(process_and_upload, tasks))

    # Mostrar resultados
    for res in results:
        print(res)

if __name__ == "__main__":
    main()

```

reports.py

```PYTHON
#!/usr/bin/env python3

from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer
from reportlab.lib.styles import getSampleStyleSheet

def generate_report(attachment, title, paragraph):
    styles = getSampleStyleSheet()
    report = SimpleDocTemplate(attachment)
    report_title = Paragraph(title, styles["h1"])
    # El 'paragraph' es el string gigante con todos los nombres y pesos
    report_info = Paragraph(paragraph, styles["BodyText"])
    empty_line = Spacer(1, 20)

    report.build([report_title, empty_line, report_info])
```

emails.py

```PYTHON
#!/usr/bin/env python3

import email.message
import mimetypes
import os.path
import smtplib

def generate_email(sender, recipient, subject, body, attachment_path=None): # Agregamos None por defecto
    """Crea un email con un adjunto opcional."""
    message = email.message.EmailMessage()
    message["From"] = sender
    message["To"] = recipient
    message["Subject"] = subject
    message.set_content(body)

    # Solo procesamos el adjunto si attachment_path NO es None ni un string vacío
    if attachment_path:
        attachment_filename = os.path.basename(attachment_path)
        mime_type, _ = mimetypes.guess_type(attachment_path)
        mime_type, mime_subtype = mime_type.split('/', 1)

        with open(attachment_path, 'rb') as ap:
            message.add_attachment(ap.read(),
                                  maintype=mime_type,
                                  subtype=mime_subtype,
                                  filename=attachment_filename)

    return message

def send_email(message):
    """Envía el mensaje al servidor SMTP configurado."""
    mail_server = smtplib.SMTP('localhost')
    mail_server.send_message(message)
    mail_server.quit()
```

report_email.py

```PYTHON
#!/usr/bin/env python3

import os
import datetime
import reports
import emails # Importamos el nuevo módulo

def process_data(directory):
    report_content = ""
    files = sorted(os.listdir(directory))
    for file in files:
        if file.endswith(".txt"):
            with open(os.path.join(directory, file), 'r') as f:
                lines = f.readlines()
                name = lines[0].strip()
                weight = lines[1].strip()
                report_content += "name: " + name + "<br/>" + "weight: " + weight + "<br/><br/>"
    return report_content

if __name__ == "__main__":
    # 1. Configuración de rutas y datos del PDF
    path = os.path.expanduser('~') + '/supplier-data/descriptions/'
    paragraph = process_data(path)
    today = datetime.date.today().strftime("%B %d, %Y")
    title = "Processed Update on " + today
    attachment = '/tmp/processed.pdf'

    # 2. Generar el reporte PDF
    reports.generate_report(attachment, title, paragraph)

    # 3. Configuración para el envío del Email
    sender = "automation@example.com"
    receiver = "student@example.com"
    subject = "Upload Completed - Online Fruit Store"
    body = "All fruits are uploaded to our website successfully. A detailed list is attached to this email."

    # 4. Generar y enviar el correo
    message = emails.generate_email(sender, receiver, subject, body, attachment)
    emails.send_email(message)
```

health_check.py

```PYTHON
#!/usr/bin/env python3

import psutil
import socket
import emails
import os

def check_cpu_usage():
    """Verifica si el uso de CPU es superior al 80%."""
    usage = psutil.cpu_percent(1)
    return usage > 80

def check_disk_usage(disk):
    """Verifica si el espacio disponible en disco es inferior al 20%."""
    du = psutil.disk_usage(disk)
    free = du.free / du.total * 100
    return free < 20

def check_available_memory():
    """Verifica si la memoria disponible es inferior a 500MB."""
    available = psutil.virtual_memory().available
    available_mb = available / (1024 ** 2) # Convertir a MB
    return available_mb < 500

def check_localhost():
    """Verifica si localhost se resuelve a 127.0.0.1."""
    localhost = socket.gethostbyname('localhost')
    return localhost != '127.0.0.1'

def send_alert(subject):
    """Configura y envía el correo de alerta."""
    sender = "automation@example.com"
    receiver = "student@example.com"
    body = "Please check your system and resolve the issue as soon as possible."
    # El health check no lleva adjunto, pasamos None o un string vacío si tu emails.py lo permite
    # Nota: Si tu emails.generate_email exige un adjunto, puedes crear un txt vacío.
    message = emails.generate_email(sender, receiver, subject, body, None)
    emails.send_email(message)

if __name__ == "__main__":
    # Revisar cada condición y enviar alerta si falla
    if check_cpu_usage():
        send_alert("Error - CPU usage is over 80%")

    if check_disk_usage('/'):
        send_alert("Error - Available disk space is less than 20%")

    if check_available_memory():
        send_alert("Error - Available memory is less than 500MB")

    if check_localhost():
        send_alert("Error - localhost cannot be resolved to 127.0.0.1")
```

---

## Solución dada en el curso

```PYTHON

```
