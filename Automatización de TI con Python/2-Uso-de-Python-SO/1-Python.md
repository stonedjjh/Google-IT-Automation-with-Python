# Instalación

**Linux Ubuntu:**

```bash
sudo apt update
sudo apt install python3
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
python3 is already the newest version (3.12.3-0ubuntu2.1).
python3 set to manually installed.
The following package was automatically installed and is no longer required:
  libllvm17t64
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 111 not upgraded.
```

## Ambientes Virtuales

Un entorno virtual en Python es una potente herramienta que te permite crear entornos aislados para tus proyectos Python. Cada entorno actúa como una caja de arena, conteniendo su propio intérprete de Python e instalaciones de librerías. Esto significa que puedes tener múltiples proyectos con diferentes dependencias, asegurando que no interfieran entre sí. En esencia, los entornos virtuales proporcionan una pizarra limpia donde puedes trabajar en tus proyectos sin preocuparte de librerías o versiones conflictivas.

**¿Por qué usar un entorno virtual en Python?**

Imagina que estás trabajando en dos proyectos Python distintos: uno requiere una versión específica de una librería, mientras que el otro depende de una versión más reciente. Sin entornos virtuales, la gestión de estas dependencias podría convertirse en una pesadilla. Aquí es donde los entornos virtuales brillan: le permiten mantener sus proyectos aislados, asegurando que los cambios en un entorno no afecten a otro.

Mediante el uso de entornos virtuales, puede

- Evitar conflictos entre librerías y dependencias.

- Probar diferentes versiones de librerías sin afectar a la instalación de Python en todo el sistema.

- Mantener un entorno de desarrollo limpio y organizado.

- Colaborar con otros mientras aseguras versiones de librerías consistentes.

**Instalación y uso:**

```bash
sudo apt install python3-venv
# Crear el entorno
python3 -m venv mi_entorno
# Activar el entorno
# En Windows:
myenv\Scripts\activate
# En macOS y Linux:
source mi_entorno/bin/activate
```

> [!TIP]
> Una vez activado, el prompt de tu terminal cambiará, indicando que ahora estás trabajando dentro del entorno virtual. Ahora puede instalar paquetes utilizando pip como lo haría normalmente.

**Buenas prácticas y recomendaciones:**

Mientras te sumerges en el mundo de los entornos virtuales, ten en cuenta estas buenas prácticas:

- **Crea un entorno virtual para cada proyecto:** Cada vez que inicies un nuevo proyecto, crea un nuevo entorno virtual. Esto garantiza un espacio de trabajo limpio y aislado.

- **Utilice archivos de requisitos:** Para documentar y gestionar las dependencias de tu proyecto, crea un archivo requirements.txt. Este archivo enumera todas las bibliotecas y sus versiones. Puedes generarlo utilizando pip freeze > requirements.txt e instalarlos posteriormente en un nuevo entorno utilizando pip install -r requirements.txt.

- **Activar y desactivar:** Activa siempre el entorno virtual adecuado antes de trabajar en un proyecto y desactívalo cuando hayas terminado. Esto evita confusiones y posibles conflictos.

- **Control de versión:** Si colaboras con otras personas, incluye las instrucciones de configuración del entorno virtual en tu sistema de control de versiones. Así te aseguras de que todo el mundo utiliza el mismo entorno.

- **Actualiza pip y setuptools:** Cuando crees un nuevo entorno virtual, es una buena práctica actualizar pip y setuptools a la última versión. Así te aseguras de que estás utilizando las herramientas más actualizadas.

## Pip (Package Installer for Python)

Pip es el gestor de paquetes estándar para Python. Es la herramienta de línea de comandos que se comunica con PyPI para descargar e instalar librerías en tu computadora.

**Instalacion:**

`sudo apt install python3-pip`

**Comandos esenciales:**

- **Instalación de paquetes:** Para instalar una librería, se usa el comando install seguido del nombre del paquete.

```Bash
pip install requests
```

- **Listar paquetes instalados:** Muestra todas las librerías que tienes instaladas actualmente y sus versiones.

```Bash
pip list
```

- **Desinstalar paquetes:** Elimina una librería de tu sistema.

```Bash
pip uninstall nombre_del_paquete
```

- **Congelar dependencias (requirements.txt):**Este es un estándar en la industria. Permite generar un archivo de texto con todas las librerías de tu proyecto para que otra persona pueda instalarlas todas de golpe.

```Bash
# Crear el archivo
pip freeze > requirements.txt
# Instalar todo lo que dice el archivo
pip install -r requirements.txt
```

## PyPI (Python Package Index)

PyPI es el repositorio oficial de software para el lenguaje de programación Python. Es una plataforma en la nube donde miles de desarrolladores de todo el mundo suben sus librerías y paquetes para que cualquiera pueda usarlos.

- El "Almacén": Imagina que PyPI es una biblioteca gigante que contiene herramientas para casi cualquier cosa: ciencia de datos, desarrollo web, inteligencia artificial, etc.

- Comunidad: Es lo que hace que Python sea tan potente, ya que no tienes que reinventar la rueda; probablemente alguien ya subió una solución a PyPI.

## Módulos

**comprobar archvivos:**

```bash
(mi_entorno) ubuntu@StoneColombia:~$ ls -l /usr/lib/python3/dist-packages/requests
total 220
-rw-r--r-- 1 root root  4857 Jun 11  2025 __init__.py
drwxr-xr-x 2 root root  4096 Jun 21  2025 __pycache__
-rw-r--r-- 1 root root   435 May 22  2023 __version__.py
-rw-r--r-- 1 root root  1495 May 22  2023 _internal_utils.py
-rw-r--r-- 1 root root 19553 May 22  2023 adapters.py
-rw-r--r-- 1 root root  6449 May 22  2023 api.py
-rw-r--r-- 1 root root 10187 May 22  2023 auth.py
-rw-r--r-- 1 root root   429 May 22  2023 certs.py
-rw-r--r-- 1 root root  1380 Jun 11  2025 compat.py
-rw-r--r-- 1 root root 18560 May 22  2023 cookies.py
-rw-r--r-- 1 root root  3811 May 22  2023 exceptions.py
-rw-r--r-- 1 root root  3806 Jun 11  2025 help.py
-rw-r--r-- 1 root root   733 May 22  2023 hooks.py
-rw-r--r-- 1 root root 35223 May 22  2023 models.py
-rw-r--r-- 1 root root   777 Jun 11  2025 packages.py
-rw-r--r-- 1 root root 30373 May 22  2023 sessions.py
-rw-r--r-- 1 root root  4235 May 22  2023 status_codes.py
-rw-r--r-- 1 root root  2912 May 22  2023 structures.py
-rw-r--r-- 1 root root 33177 Jun 11  2025 utils.py
(mi_entorno) ubuntu@StoneColombia:~$
```

> [!IMPORTANT]
> El archivo `__init__.py` le indica a python que debe tratar el directorio como un móodulos

**personalizados:**

areas.py

```Python
import math

def triangle(base, heigth):
    return base*heigth/2

def rectangle(base, height):
    return base*height

def circle(radius):
    return math.pi*(radius**2)
```

```bash
(mi_entorno) ubuntu@StoneColombia:~$ nano areas.py
(mi_entorno) ubuntu@StoneColombia:~$ python3
Python 3.12.3 (main, Jan 22 2026, 20:57:42) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import areas
>>> areas.triangle(3,5)
7.5
```
