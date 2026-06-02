# Planteamiento del problema del proyecto

Para completar este módulo, tendrás que escribir un script que procese un montón de imágenes. Resulta que su empresa está actualizando su sitio web y ha contratado a un diseñador para que cree nuevos iconos gráficos para el sitio. Sin embargo, el contratista ha entregado los diseños finales y están en un formato incorrecto, girados 90° y demasiado grandes. No puedes ponerte en contacto con los diseñadores y tu propio plazo de entrega se acerca rápidamente. Tendrás que utilizar Python para que las imágenes estén listas para el lanzamiento

¿Cómo lo harás? Tendrás que revisar una carpeta llena de imágenes y operar con cada una de ellas. En cada imagen, usarás métodos PIL como los que vimos en los ejemplos, y luego escribirás las nuevas imágenes en el lugar correcto.

Si esto te parece complicado, ¡que no cunda el pánico! Ya has visto todo lo que necesitas para hacerlo, y ahora es el momento de ponerlo en práctica.

ASÍ COMO EN LOS CURSOS ANTERIORES, la evaluación se hará sobre una máquina virtual corriendo en la Nube, gracias a la infraestructura de Qwiklabs. Sólo tendrás acceso a la VM durante un tiempo limitado, por lo que te recomendamos que primero escribas el script localmente en tu ordenador, y sólo inicies el laboratorio una vez que tu script esté funcionando correctamente.

Buena suerte, ¡ya lo tienes!

## Evaluación de Qwiklabs: Escalar y convertir imágenes utilizando PIL

Su empresa está actualizando su sitio web y ha contratado a un diseñador para que cree nuevos iconos gráficos. Pero el contratista ha entregado los diseños finales en un formato incorrecto: girados 90° y demasiado grandes. ¡Uf! No puedes ponerte en contacto con los diseñadores y tu propio plazo de entrega se acerca rápidamente. Necesitarás usar Python para tener estas imágenes listas para el lanzamiento.

### Lo que tienes que hacer

Utiliza la Python Imaging Library para hacer lo siguiente a un lote de imágenes:

- Abrir una imagen

- Rotar una imagen

- Redimensionar una imagen

- Guardar una imagen en un formato específico en un directorio separado

## Repuesta planteada

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
    output_path = os.path.join(output_dir, filename + ".jpeg")

    try:
        with Image.open(input_path) as img:
            img = rotate_image(img)
            img = resize_image(img)

            save_image(img, output_path)
        print(f"Procesada con éxito: {filename}")
    except Exception as e:
        print(f"Error procesando {filename}: {e}")

def run_batch_processing(input_dir, output_dir):
    """
    Recorre el directorio, filtra archivos y lanza el procesamiento paralelo.
    """
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    images = [f for f in os.listdir(input_dir) if not f.startswith('.')]
    tasks = [(f, input_dir, output_dir) for f in images]

    with ProcessPoolExecutor() as executor:
        executor.map(process_single_image, tasks)

if __name__ == "__main__":
    # Configura aquí las rutas según las instrucciones de tu Qwiklab
    # Usualmente en estos labs es algo como 'images/' y '/opt/icons/'
    SOURCE_DIR = "images/"
    DEST_DIR = "/opt/icons/"

    run_batch_processing(SOURCE_DIR, DEST_DIR)
```

## Solución dada en el curso

```PYTHON
#!/usr/bin/env python3

import os
from PIL import Image

old_path = os.path.expanduser('~') + '/images/'
new_path = '/opt/icons/'

for image in os.listdir(old_path):
    if '.' not in image[0]:
        img = Image.open(old_path + image)
        img.rotate(-90).resize((128, 128)).convert("RGB").save(new_path + image.split('.')[0], 'jpeg')
        img.close()
```
