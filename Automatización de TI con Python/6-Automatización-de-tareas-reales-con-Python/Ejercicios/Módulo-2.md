# Planteamiento del problema del proyecto

Para completar este módulo, escribirá un script que interactúa con un servicio web en ejecución. El servicio web forma parte del sitio web de su empresa y se encarga de almacenar y mostrar las reseñas de los clientes de la empresa.

Las reseñas se almacenan en archivos de texto en el disco local. Su script debe abrir esos archivos, procesar la información para convertirla en el formato esperado por el servicio web y, a continuación, enviarla al servicio web para que la almacene.

Para este laboratorio, el servicio se ejecuta en la misma máquina y, si lo deseas, puedes ver cómo se implementa todo, pero no es necesario que cambies la implementación del servicio para completar el ejercicio.

Recuerda que puedes tomarte tu tiempo para preparar el código que vas a escribir. Puedes empezar el laboratorio más tarde, una vez que tengas una buena idea de lo que harás y cómo lo harás.

Además, no dudes en consultar los recursos que te hemos indicado tantas veces como necesites.

Buena suerte, ¡ya lo tienes!

## Evaluación de Qwiklabs: Procesamiento de Archivos de Texto con Diccionarios de Python y Carga a un Servicio Web

**Introducción:**

Trabajas en una empresa de venta de autos usados que recolecta constantemente comentarios de clientes. Tu manager te pide que tomes esas reseñas (guardadas como archivos `.txt`) y las muestres en el sitio web de la empresa. Para hacerlo, deberás escribir un script que convierta esos archivos `.txt` en diccionarios de Python y luego suba los datos al sitio web (que usa Django).

Lo que harás:

- Usar el módulo `os` de Python para procesar un directorio de archivos de texto.

- Gestionar información almacenada en diccionarios de Python.

- Usar el módulo `requests` de Python para subir contenido a un servicio web en ejecución.

- Entender operaciones básicas de `requests` como los métodos **GET** y **POST**.

**Servidor Web corpweb (Django):**

El servidor ya está configurado. Puedes ver que actualmente no hay comentarios si entras a la IP externa. Si agregas `/feedback` a la URL, verás la interfaz de la API REST donde se pueden ingresar los datos.

**El Formato de los Datos:**

El sistema espera un JSON con estas claves:
`{"title": "...", "name": "...", "date": "...", "feedback": "..."}`

**Procesar archivos y subir al servidor (El Desafío):**

Aquí es donde escribes el código. Los archivos están en /data/feedback.

1. Inspección de los archivos:

   Si haces un `cat 007.txt`, verás que tienen este formato siempre:
   - Línea 1: Título (`title`)
   - Línea 2: Nombre (`name`)
   - Línea 3: Fecha (`date`)
   - Línea 4 en adelante: Comentario (`feedback`)

2. Estructura del script run.py:
   - Debes crear el script en tu home (`nano ~/run.py`) con la siguiente lógica:
   1. Listar archivos: Usa `os.listdir()` para obtener todos los archivos `.txt` en /data/feedback.
   2. Iterar y Convertir: Por cada archivo, debes leer el contenido y crear un diccionario donde las claves sean `title`, `name`, `date` y `feedback`.
   - **Tip de Programador:** Como el feedback puede tener varias líneas, asegúrate de leer bien el archivo.
   3. Enviar vía POST: Usa **requests.post()** para enviar cada diccionario a `http://<IP_EXTERNA>/feedback`.
   4. Validar: Verifica que el código de estado de la respuesta sea 201 (Creado exitosamente).

**Resumen de Pasos en Terminal:**

1. `cd ~` (Ir a tu carpeta personal).

2. `nano run.py` (Crear el archivo).

3. Escribir el código con `import os` e `import requests`.

4. `chmod +x ~/run.py` (Dar permisos de ejecución).

5. ~./run.py~ (Ejecutar).

## Repuesta Planteada

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
        feedback_data = {
            "title": lines[0],
            "name": lines[1],
            "date": lines[2],
            "feedback": " ".join(lines[3:])
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
    SOURCE_DIR = "/data/feedback/"
    # REEMPLAZA ESTO con la IP que te dio el laboratorio
    EXTERNAL_IP = "TU_IP_AQUÍ"
    URL = f"http://{EXTERNAL_IP}/feedback/"

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

---

## Solución dada en el curso

```PYTHON
#! /usr/bin/env python3


import os
import requests

BASEPATH = '/data/feedback/'

folder = os.listdir(BASEPATH)

list = []

for file in folder:
    with open(BASEPATH + file, 'r') as f:
        list.append({"title":f.readline().rstrip("\n"),
                    "name":f.readline().rstrip("\n"),
                    "date":f.readline().rstrip("\n"),
                    "feedback":f.read().rstrip("\n")})

for item in list:
    resp = requests.post('http://127.0.0.1:80/feedback/', json=item)
    if resp.status_code != 201:
        raise Exception('POST error status={}'.format(resp.status_code))
    print('Created feedback ID: {}'.format(resp.json()["id"]))
```
