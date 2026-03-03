# Archivos

En este módulo se vera como trabajar con archivos y rutas en python

```python
# instrucción usada para abrir un archivo
file = open("spider.txt")
# lee la linea actual del archivo
print(file.readline())
print(file.readline())
# lee todo el contenido del archivo
print(file.read())
# instrucción usada para cerrar un archivo
file.close()
with open("spider.txt") as file:
    print(file.readline())
```

Estas líneas imprimen las tres primeras líneas del archivo. El método readline() lee una línea del archivo y la devuelve como cadena. El método read() lee el archivo completo y lo devuelve como una cadena. El método close() cierra el archivo.

- **`open()`:** Es la función principal para abrir un archivo. Recibe como primer argumento la ruta del archivo (nombre o dirección) y como segundo el modo de apertura (lectura, escritura, etc.). Crea un "objeto archivo" que sirve como puente entre tu código y los datos en el disco duro.

- **`close():`** Es el método que cierra la conexión con el archivo. Es fundamental usarlo porque libera los recursos del sistema operativo que el archivo estaba ocupando. Si no se cierra un archivo, otros programas podrían no ser capaces de acceder a él o podrías perder datos que aún están en el búfer de escritura.

- **`readline()`:** Lee una sola línea del archivo cada vez que se ejecuta. Es ideal para archivos muy grandes, ya que no carga todo el contenido en la memoria RAM, sino que permite procesar el archivo línea por línea de manera secuencial.

- **`readlines():`** Lee todas las líneas del archivo y las devuelve como una lista de cadenas (una lista de strings). Cada elemento de la lista corresponde a una línea del archivo, incluyendo el carácter de salto de línea \n al final de cada una. Es muy útil cuando necesitas manipular las líneas usando métodos de lista (como sort() o acceder a una línea específica por su índice), pero al igual que read(), consume memoria proporcional al tamaño del archivo.

- **`read()`:** Lee la totalidad del contenido del archivo y lo devuelve como una sola cadena de texto (string). Aunque es muy sencillo de usar, debe manejarse con cuidado en archivos gigantescos para evitar saturar la memoria del sistema.

> [!TIP]
> La lectura la hace donde este el curso actualmente, esto quiere decir que si se han leido varias lineas y se usa `read()` leera desde la linea actual hasta el final

- **`write():`** Es el método utilizado para insertar contenido en un archivo. A diferencia de `print()`, este método no añade automáticamente un salto de línea al final; si deseas que el texto siguiente comience en una nueva línea, debes incluir explícitamente el carácter \n.

> [!TIP]
> Para poder usar este método, el archivo debe haber sido abierto en un modo que permita escritura (`"w"`, `"a"`, o `"r+"`).

- **`with`:** Es una palabra clave que crea un bloque de contexto. Al usar with open(...), Python se encarga de cerrar el archivo automáticamente una vez que el bloque de código termina, incluso si ocurre un error inesperado. Es la forma más segura y recomendada de trabajar con archivos para evitar fugas de memoria o archivos bloqueados.

**Modos de apertura comunes para open():**

| Modo     | Descripción                                                                                                                               |
| :------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| **"r"**  | Read: Abre el archivo para lectura (valor por defecto). Lanza error si no existe.                                                         |
| **"w"**  | Write: Abre para escritura. Sobrescribe todo el contenido o crea el archivo si no existe.                                                 |
| **"a"**  | Append: Abre para añadir contenido al final del archivo sin borrar lo anterior.                                                           |
| **"r+**" | Read/Write: Abre el archivo tanto para leer como para escribir.                                                                           |
| **"rt"** | Read + text: El segundo argumento identifica el modo o la forma en que se utilizará el archivo "t" le indica que es texto                 |
| **"rb"** | Read + binario: El segundo argumento identifica el modo o la forma en que se utilizará el archivo "b" le indica que es un archivo binario |

> [!TIP]
> Si utilizas la estructura with open(...), no necesitas llamar a .close() manualmente, ya que Python lo hace por ti al terminar el bloque de indentación.
> El modo de apertura por defecto es `"r"` (lectura o read).
> Python codificará el archivo como texto ("t") por defecto a menos que se especifique una codificación específica.
> Como tercer parametro se puede pasar `encoding="utf-8"`. Si no se especifica la codificación, la predeterminada depende de la plataforma. Esto significa que se llama a locale.getencoding() para obtener la codificación locale actual `f = open('workfile', 'w', encoding="utf-8")`

## Iterar sobre archivo

```Python
#En este ejericio se agrega una linea en blanco entre lineas por la funcion print
with open("spider.txt") as file:
    for line in file:
        print(line.upper())
"""
THE ITSY BITSY SPIDER CLIMBED UP THE WATERSPOUT.

DOWN CAME THE RAIN

AND WASHED THE SPIDER OUT.

OUT CAME THE SUN

AND DRIED UP ALL THE RAIN

AND THE ITSY BITSY SPIDER CLIMBED UP THE SPOUT AGAIN.
"""

#En este ejemplo se eliminan los espacios usando strip
with open("spider.txt") as file:
    for line in file:
        print(line.strip().upper())
"""
THE ITSY BITSY SPIDER CLIMBED UP THE WATERSPOUT.
DOWN CAME THE RAIN
AND WASHED THE SPIDER OUT.
OUT CAME THE SUN
AND DRIED UP ALL THE RAIN
AND THE ITSY BITSY SPIDER CLIMBED UP THE SPOUT AGAIN.
"""

# Otro metodo de lectura es readlines()
with open("spider.txt") as file:
    lineas = file.readlines()

print(lineas)
"""
['Down came the rain\n', 'Out came the sun\n', 'The itsy bitsy spider climbed up the waterspout.\n', 'and dried up all the rain\n', 'and the itsy bitsy spider climbed up the spout again.\n', 'and washed the spider out.\n']
"""

print(lineas[0]) # Acceso directo a la primera línea
"Down came the rain\n"
```

## Escribir en un archivo

```python
with open("novel.txt", "w") as file:
    file.write("It was a dark and stormy night.")
```

> [!ALERT]
> Si el archivo ya existe con `"w"` se eliminara el mismo
> [!TIP]
> La instrucción write devuelve la cantidad de caracteres escritos

## Rutas (Paths)

Una ruta es la dirección que indica la ubicación de un archivo o directorio dentro de la estructura de carpetas del sistema operativo. En Python, el módulo os y pathlib son los encargados de gestionar estas direcciones.

Existen dos tipos principales de rutas:

1. **Ruta Absoluta (Absolute Path)**
   Es la dirección completa desde la raíz del sistema operativo hasta el archivo. No depende de dónde estés ejecutando tu script.

Ejemplo en Windows: `C:\Users\Admin\Documents\archivo.txt`

Ejemplo en Linux/Mac: `/home/user/documents/archivo.txt`

2. **Ruta Relativa (Relative Path)**

Es la dirección del archivo en relación con la carpeta donde se está ejecutando el script actualmente (el directorio de trabajo).

- Si tu script está en la misma carpeta que el archivo, la ruta relativa es simplemente: `archivo.txt`

- Si el archivo está en una subcarpeta llamada datos: `datos/archivo.txt`

### Conceptos Clave de Rutas

- **Directorio de Trabajo (CWD - Current Working Directory):** Es la carpeta en la que Python "está parado" en este momento. Todas las rutas relativas parten de aquí.

- **.. (Dos puntos):** Se usa en rutas relativas para subir un nivel en la jerarquía de carpetas (ir a la carpeta padre).

- **. (Un punto):** Representa el directorio actual.

Ejemplo con el módulo os:

```Python
import os

# Obtener el directorio de trabajo actual

print(os.getcwd())

# Unir rutas de forma segura (evita problemas entre Windows y Linux)

ruta = os.path.join("carpeta_padre", "subcarpeta", "archivo.txt")
print(ruta)
```

> [!TIP]
> Siempre es recomendable usar os.path.join() en lugar de escribir las rutas manualmente con barras / o \, ya que Python se encargará de poner la barra correcta dependiendo de si tu script corre en Windows, Linux o macOS.

### Obtener ruta actual `os.getcwd()`

getcwd significa "Get Current Working Directory" (Obtener el Directorio de Trabajo Actual).

Esta función devuelve una cadena de texto (string) con la ruta absoluta de la carpeta en la que Python se está ejecutando en ese preciso momento.

```Python
import os

# Supongamos que tu script está en /home/usuario/proyectos
ruta_actual = os.getcwd()

print("Actualmente estoy en: " + ruta_actual)
# Salida: Actualmente estoy en: /home/usuario/proyectos
```

> [!IMPORTANT]
> No siempre es la carpeta donde está guardado el archivo .py. Es la carpeta desde la cual lanzaste el comando en la terminal. Si abres la terminal en el Escritorio y ejecutas un script que está en Documentos, os.getcwd() devolverá la ruta del Escritorio.

### Listar el diirectorio actual `os.listdir()`

La función os.listdir() se utiliza para listar el contenido de un directorio. Devuelve una lista que contiene los nombres de todos los archivos y subcarpetas que se encuentran dentro de la ruta especificada.

**Puntos clave:**

- **Formato:** Devuelve los nombres como cadenas de texto (strings) dentro de una lista de Python.

- **Sin distinción:** No diferencia automáticamente entre un archivo (como documento.txt) y una carpeta; simplemente te da los nombres de ambos.

- **Ruta opcional:** Si no le pasas ninguna ruta entre los paréntesis, por defecto listará el contenido del directorio donde estás parado actualmente (os.getcwd()).

- **Orden:** El orden de la lista es arbitrario (depende del sistema operativo).

Ejemplo de uso:

```Python
import os

# Listar el contenido del directorio actual

contenido = os.listdir()
print(contenido)

# Ejemplo de salida:

# ['archivo1.txt', 'fotos_vacaciones', 'script.py', 'notas.md']

# Listar una ruta específica

carpetas_sistema = os.listdir("/usr/bin")
```

**Combinación común en scripts:**

Normalmente se usa junto con un bucle for para procesar cada archivo de una carpeta:

```Python
import os

for nombre in os.listdir():
    if nombre.endswith(".txt"):
        print("Encontré un archivo de texto:", nombre)
```

### `os.environ.get("PATH")`

Esta función sirve para consultar las variables de entorno del sistema operativo desde Python.

`os.environ.get("PATH")`
Específicamente, este comando accede al diccionario de variables de entorno (`os.environ`) y busca el valor asociado a la clave `"PATH"`.

**¿Qué es el PATH?:**

El **PATH** es una de las variables más importantes del sistema. Contiene una lista de rutas (directorios) donde el sistema operativo busca programas ejecutables cuando escribes un comando en la terminal.

Si un programa (como `python`, `git` o `ls`) está en una de las carpetas listadas en el PATH, puedes ejecutarlo desde cualquier lugar sin escribir su ruta completa.

**Puntos clave de esta instrucción:**

- **os.environ:** Es un objeto tipo diccionario que contiene todas las variables de entorno actuales (usuario, configuración del sistema, rutas, etc.).

- **.get("PATH"):** Es un método seguro para obtener el valor. Si por alguna razón la variable "PATH" no existiera, devolverá `None` en lugar de lanzar un error.

- **Resultado:** Devuelve un string largo donde las rutas están separadas por `:` (en Linux/Mac) o por `;` (en Windows).

**Ejemplo de uso en código:**

```Python
import os

# Obtener la variable PATH

rutas_sistema = os.environ.get("PATH")

# En Linux/Mac, podemos separar las rutas para verlas mejor

print(rutas_sistema.split(":"))
```

### `os.remove()`

La función os.remove() se utiliza para eliminar permanentemente un archivo del sistema de archivos.

**Puntos clave:**

- **Solo para archivos:** Esta función no puede eliminar carpetas (directorios). Si intentas usarla sobre una carpeta, Python lanzará un error de tipo `IsADirectoryError`.

- **Eliminación permanente:** A diferencia de cuando borras un archivo manualmente, `os.remove()` no lo envía a la "Papelera de reciclaje". El archivo desaparece inmediatamente.

- **Error de existencia:** Si intentas borrar un archivo que no existe, el script se detendrá con un `FileNotFoundError`.

**Ejemplo de uso seguro:**

Para evitar que el script falle si el archivo ya no está ahí, se suele verificar su existencia primero:

```Python
import os

archivo = "archivo_temporal.txt"

if os.path.exists(archivo):
    os.remove(archivo)
    print(f"El archivo {archivo} ha sido eliminado.")
else:
    print("El archivo no existe.")
```

**¿Y si quiero borrar una carpeta?:**

Como `os.remove()` es solo para archivos, Python ofrece otras funciones:

- `os.rmdir()`: Borra una carpeta, pero solo si está vacía.

- `shutil.rmtree()`: Borra una carpeta y todo su contenido (archivos y subcarpetas). Esta es la opción más potente y peligrosa.

### `os.rename()`

La función os.rename() se utiliza para cambiar el nombre de un archivo o de un directorio. También puede usarse para mover un archivo a una carpeta distinta, siempre y cuando ambas ubicaciones estén en el mismo disco.

**Puntos clave:**

- **Dos argumentos:** Recibe primero el nombre actual (o ruta) y después el nombre nuevo (o ruta nueva).

- **Versatilidad:** Funciona tanto con archivos como con carpetas.

- **Sobrescritura:** En sistemas tipo Unix (Linux/Mac), si el nombre nuevo ya existe y es un archivo, podría sobrescribirlo silenciosamente. En Windows, normalmente lanzará un error si el destino ya existe.

- **Error de origen:** Si el archivo original no existe, lanzará un FileNotFoundError.

**Ejemplo de uso:**

```Python
import os

# 1. Renombrar un archivo simple

os.rename("notas_viejas.txt", "notas_2026.txt")

# 2. Mover y renombrar (si la carpeta 'backup' existe)

os.rename("config.json", "backup/config_old.json")
```

**Un truco útil:**

Si necesitas renombrar muchos archivos a la vez (por ejemplo, añadirles una fecha), puedes combinarlo con `os.listdir()`:

```Python
import os

for nombre in os.listdir():
    if nombre.endswith(".bak"):
        nuevo*nombre = "ANTIGUO*" + nombre
        os.rename(nombre, nuevo_nombre)
```

> [!CAUTION]
> Si intentas usar `os.rename()` para mover un archivo entre diferentes unidades de disco (por ejemplo, del disco `C:` al `D:`), fallará. Para esos casos se utiliza `shutil.move()`.

### `os.path.exists()`

La función `os.path.exists()` comprueba si la ruta especificada (ya sea un archivo o un directorio) existe realmente en el sistema de archivos. Devuelve un valor booleano: `True` si existe o `False` si no.

**Puntos clave:**

- **Versátil:** Funciona tanto para archivos individuales como para carpetas completas.

- **Previene errores:** Es la mejor práctica antes de realizar operaciones destructivas como `os.remove()` o de lectura con `open()`.

- **Rutas relativas y absolutas:** Puedes pasarle solo el nombre del archivo (si está en la carpeta actual) o la dirección completa.

**Ejemplo de uso práctico:**

```Python
import os

ruta = "configuracion.txt"

if os.path.exists(ruta):
    with open(ruta, "r") as file:
        print(file.read())
else:
    print(f"Error: El archivo '{ruta}' no se encuentra.")
```

**Funciones similares para mayor precisión:**

A veces no basta con saber si algo existe, sino qué tipo de cosa es. Para eso existen:

- **os.path.isfile(ruta):** Devuelve True solo si la ruta existe y además es un archivo.

- **os.path.isdir(ruta):** Devuelve True solo si la ruta existe y además es una carpeta.

```Python
import os

if os.path.exists("descargas"):
    if os.path.isdir("descargas"):
         print("Es una carpeta.")
    elif os.path.isfile("descargas"):
         print("Es un archivo.")
```

### `os.path.getsize()`

Devuelve el tamaño del archivo en bytes. Es una forma rápida de verificar si un archivo está vacío o si es demasiado grande para ser procesado.

Ejemplo: `os.path.getsize("spider.txt")` devolvería 192 (bytes).

### `os.path.getmtime()`

Devuelve la fecha de la última modificación del archivo. El resultado es un timestamp de Unix (un número flotante que representa los segundos transcurridos desde el 1 de enero de 1970).

mtime significa "modification time".

### `datetime.datetime.fromtimestamp()`

Aunque pertenece al módulo datetime, se usa frecuentemente con la función anterior. Convierte el número del timestamp en un objeto de fecha y hora legible (año, mes, día, hora, etc.).

### `os.path.abspath()`

Convierte una ruta relativa (o solo el nombre de un archivo) en una ruta absoluta. Esto es extremadamente útil para asegurar que tu script encuentre un archivo sin importar desde qué carpeta se esté ejecutando en la terminal.

```Python
import os
import datetime

archivo = "spider.txt"

# Obtener metadatos
tamano = os.path.getsize(archivo)
timestamp = os.path.getmtime(archivo)
fecha = datetime.datetime.fromtimestamp(timestamp)
ruta_completa = os.path.abspath(archivo)

print(f"El archivo {archivo} mide {tamano} bytes.")
print(f"Última modificación: {fecha}")
print(f"Ubicación exacta: {ruta_completa}")
```

### `os.mkdir()`

Crea una nueva carpeta (directorio) en la ruta especificada. Si la carpeta ya existe, Python lanzará un error de tipo FileExistsError.

### `os.chdir()`

Cambia el directorio de trabajo actual del script. Es como ejecutar un comando cd en la terminal; a partir de esa línea, todas las rutas relativas se calcularán desde la nueva carpeta.

### `os.rmdir()`

Elimina un directorio. Nota importante: Esta función solo funciona si la carpeta está completamente vacía. Si contiene archivos o subcarpetas, lanzará un OSError.

## CSV

El formato **CSV** (Comma Separated Values - Valores Separados por Comas) es uno de los estándares más utilizados para almacenar datos tabulares de forma sencilla y ligera.

Es un archivo de texto plano que organiza la información en filas y columnas. Cada línea del archivo representa una fila y cada valor dentro de esa fila está separado por una coma (representando una columna).

Python tiene su propio modulo para trabaja con CSV llamado `csv`

```PYTHON
import csv
 f = open("csv_file.txt")
 csv_f = csv.reader(f)
 for row in csv_f:
     name, phone, role = row
     print("Name: {}, Phone: {}, Role: {}".format(name, phone, role))
f.close()
```

**Conceptos Clave:**

- **Delimitador:** Aunque se llaman "separados por comas", a veces se usan otros caracteres como el punto y coma (;) o tabuladores (\t).

- **Cabecera (Header):** Es la primera línea del archivo que indica el nombre de las columnas.

- **Escalabilidad:** Los CSV son excelentes para datos de tamaño medio, pero para archivos masivos se suelen preferir bibliotecas como pandas.

### Funciones

- **`reader()`**

Para manejar estos archivos, Python incluye el módulo `csv`, que facilita la conversión de líneas de texto a listas o diccionarios.

```PYTHON
import csv

with open("datos.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        # Cada 'row' es una lista de strings
        print("Nombre: {}, Edad: {}, Puesto: {}".format(row[0], row[1], row[2]))
```

- **`writer()`**

Para crear un archivo CSV, usamos un objeto writer. Es fundamental definir el parámetro newline='' al abrir el archivo para evitar filas vacías adicionales en algunos sistemas operativos.

```Python
import csv

hosts = [["workstation.local", "192.168.1.25"], ["webserver.cloud", "10.2.5.33"]]

with open("hosts.csv", "w", newline='') as hosts_csv:
    writer = csv.writer(hosts_csv)
    writer.writerows(hosts)
```

> [!NOTE]
> writer tiene 2 métodos de escritura `writerow()` para escribir linea por linea y `writerows()` para escribir varias lineas juntas.

- **Uso de Diccionarios (`DictReader` y `DictWriter`)**

Esta es la forma más legible de trabajar con CSV, ya que permite acceder a los datos usando el nombre de la cabecera en lugar de índices numéricos.

```bash
cat software.csv 
#Output name,version,status,users
#MailTree,5.34,production,324
#CalDoor,1.25.1,beta,22
#Chatty Chicken,0.34,alpha,4
```

```Python
import csv

# Lectura como diccionario
with open("software.csv") as soft:
    reader = csv.DictReader(soft)
    for row in reader:
        print("{} tiene {} usuarios".format(row["name"], row["users"]))
"""
MailTree tiene 324 usuarios

CalDoor tiene 22 usuarios

Chatty Chicken tiene 4 usuarios
"""

```

```Python
users = [ {"name": "Sol Mansi", "username": "solm", "department": "IT infrastructure"},
 {"name": "Lio Nelson", "username": "lion", "department": "User Experience Research"},
  {"name": "Charlie Grey", "username": "greyc", "department": "Development"}]
keys = ["name", "username", "department"]
with open('by_department.csv', 'w') as by_department:
    writer = csv.DictWriter(by_department, fieldnames=keys)
    writer.writeheader()
    writer.writerows(users)
```

```bash
cat by_department.csv
#Output
"""
Nombre,usuario,departamento

Sol Mansi,solm, infraestructura de TI

Lio Nelson,lion,Investigador de la experiencia del usuario

Charlie Grey,greyc,Desarrollo

"""
```
