# Ejercicios

## Módulo 1

En este ejemplo:

1. Se instala la libreria request que permite hacer peticiones http a una url
2. Se ingresa a `python3`
3. Se importa la libreria `import requests`
4. Se hace una peticion get al sitio `http://www.google.com`
5. Se imprime la longitud de la respuesta

```bash
sudo apt install python3-request
python3
Python 3.12.3 (main, Jan 22 2026, 20:57:42) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> response = requests.get("http://www.google.com")
>>> len(response.text)
17681
```

**Crear un analizador de estado del sistema:**

1. Se importa shutil para obtener información de los medios de almacenamiento (disco).

2. Se importa psutil para obtener información del procesador (CPU).

3. Se crea una variable de estado error_found para rastrear si alguna comprobación falla.

4. Se define check_disk_usage para verificar si el espacio libre es mayor al 20%.

5. Se define check_cpu_usage para verificar si la carga del procesador es menor al 75% en un intervalo de 1 segundo.

6. Se ejecutan las funciones y, si alguna falla, se cambia el estado de la variable y se muestra un aviso.

```python
#!usr/bin/env python3
import shutil
import psutil
error_found = False = False

def check_disk_usage(disk):
    du = shutil.dik_usage(disk)
    free = du.free / du.total * 100
    return free > 20

def check_cpu_usage():
    usage = psutil.cpu_percent(1)
    return usage < 75

if not check_dick_usage("/"):
    print("Warning: Insufficient disk space detected.")
    error_found = True

if not check_cpu_usage():
    print("Warning: CPU usage is over 75%.")
    error_found = True

if not error_found:
    print("Everything ok.")
```

## Módulo 2

### Práctica: Lectura y Escritura de Archivos

En este ejercicio se pone a prueba el manejo de archivos de texto simulando el sistema de registro de un hotel.

1. Creación del archivo inicial
   Primero, creamos el archivo guests.txt con los primeros huéspedes. Cada nombre se escribe en una línea nueva.

```python
guests = open("guests.txt", "w")
initial_guests = ["Bob", "Andrea", "Manuel", "Polly", "Khalid"]

for i in initial_guests:
    guests.write(i + "\n")

guests.close()
```

Verificación del contenido
Para comprobar que el archivo se generó correctamente, leemos cada línea:

```python
with open("guests.txt") as guests:
    for line in guests:
        print(line)
"""
Bob

Andrea

Manuel

Polly

Khalid
"""
```

---

2. Actualización de archivos (Check-in)
   Cuando llegan nuevos huéspedes, utilizamos el modo "a" (append) para añadir nombres al final del archivo sin borrar los existentes.

```Python
new_guests = ["Sam", "Danielle", "Jacob"]

with open("guests.txt", "a") as guests:
    for i in new_guests:
        guests.write(i + "\n")

guests.close()

with open("guests.txt") as guests:
    for line in guests:
        print(line)

"""
Bob

Andrea

Manuel

Polly

Khalid

Sam

Danielle

Jacob
"""
```

Los nombres actuales en el archivo guest.txt deben ser: Bob, Andrea, Manuel, Polly, Khalid, Sam, Danielle y Jacob.

---

3. Eliminación de registros (Check-out)

Para eliminar huéspedes que ya se retiraron, seguimos este proceso lógico:

1. Abrir el archivo en modo lectura.

2. Almacenar los nombres en una lista temporal.

3. Reabrir el archivo en modo escritura (sobrescribiendo todo).

4. Volver a escribir solo los nombres que no están en la lista de check-out.

```Python
checked_out = ["Andrea", "Manuel", "Khalid"]
temp_list = []

# Paso 1: Leer y guardar en lista
with open("guests.txt", "r") as guests:
    for g in guests:
        temp_list.append(g.strip())

# Paso 2: Sobrescribir filtrando los datos
with open("guests.txt", "w") as guests:
    for name in temp_list:
        if name not in checked_out:
            guests.write(name + "\n")

#Para comprobar si su código eliminó correctamente los invitados retirados del archivo guest.txt, ejecute la siguiente celda.

with open("guests.txt") as guests:
    for line in guests:
        print(line)

"""
Bob

Polly

Sam

Danielle

Jacob
"""

```

Los nombres actuales en el archivo guest.txt deben ser: Bob, Polly, Sam, Danielle y Jacob.

---

4. Búsqueda de datos específicos
   Finalmente, verificamos si ciertos huéspedes siguen registrados leyendo el archivo y comparando los nombres.

```Python
guests_to_check = ['Bob', 'Andrea']
checked_in = []

with open("guests.txt", "r") as guests:
    if "Bob" in guests_to_check:
        checked_in.append("Bob")

    for check in guests_to_check:
        if check in content:
            print("{} is checked in".format(check))
        else:
            print("{} is not checked in".format(check))

"""
Bob is checked in
Andrea is not checked in
"""
```

Podemos ver que Bob está registrado mientras que Andrea no. ¡Buen trabajo! ¡Has aprendido los conceptos básicos de lectura y escritura de archivos en Python

### Resumen de conceptos aplicados

- **open(file, "w")**: Crea/Sobrescribe el archivo.

- **open(file, "a")**: Añade al final del archivo.

- **strip()**: Limpia los caracteres invisibles como \n al leer.

- **with**: Asegura que el archivo se cierre automáticamente tras la operación.

Estamos trabajando con una lista de flores y alguna información sobre cada una de ellas. La función crear_archivo escribe esta información en un Archivo CSV. La función contents_of_file lee este archivo en registros y devuelve la información en un bloque bien formateado. Rellene los huecos de la función contents_of_file para convertir los datos del Archivo CSV en un diccionario utilizando DictReader.

```PYTHON
import os
import csv

# Create a file with data in it
def create_file(filename):
  with open(filename, "w") as file:
    file.write("name,color,type\n")
    file.write("carnation,pink,annual\n")
    file.write("daffodil,yellow,perennial\n")
    file.write("iris,blue,perennial\n")
    file.write("poinsettia,red,perennial\n")
    file.write("sunflower,yellow,annual\n")


# Read the file contents and format the information about each row
def contents_of_file(filename):
  return_string = ""

  # Call the function to create the file
  create_file(filename)

  # Open the file
  with open(filename,'r') as mi_archivo:
    # Read the rows of the file into a dictionary
    reader = csv.DictReader(mi_archivo)
    # Process each item of the dictionary
    for row in reader:
      return_string += "a {} {} is {}\n".format(row["color"], row["name"], row["type"])
  return return_string


#Call the function
print(contents_of_file("flowers.csv"))
```

Utilizando de nuevo el archivo CSV de flores, rellene los huecos de la función contents_of_file para procesar los datos sin convertirlos en un diccionario. ¿Cómo se salta el registro de cabecera con los nombres de los campos?

```PYTHON
import os
import csv

# Create a file with data in it
def create_file(filename):
  with open(filename, "w") as file:
    file.write("name,color,type\n")
    file.write("carnation,pink,annual\n")
    file.write("daffodil,yellow,perennial\n")
    file.write("iris,blue,perennial\n")
    file.write("poinsettia,red,perennial\n")
    file.write("sunflower,yellow,annual\n")

# Read the file contents and format the information about each row
def contents_of_file(filename):
  return_string = ""

  # Call the function to create the file
  create_file(filename)

  # Open the file
  with open(filename,'r') as mi_archivo:
    # Read the rows of the file
    rows = csv.reader(mi_archivo)
    next(rows)
    # Process each row
    for row in rows:
      name,color,type = row
      # Format the return string for data rows only

      return_string += "a {} {} is {}\n".format(color, name, type)
  return return_string

#Call the function
print(contents_of_file("flowers.csv"))
```

## Módulo 3

- Rellene el código para comprobar si el texto pasado contiene las vocales a, e, e i y cumple los siguientes criterios:
  - las vocales aparecen en el orden a, e, i

  - las vocales tienen exactamente una aparición de cualquier otro carácter entre ellas.

```Python
import re
def check_aei (text):
  # result = re.search(r"___", text)
  result = re.search(r"a.e.i", text)
  return result != None

print(check_aei("academia")) # True
print(check_aei("aerial")) # False
print(check_aei("paramedic")) # True

Here is your output:
True
False
True

Great work! You've written your first regular expression!
```

- Rellene el código para comprobar si el texto pasado contiene signos de puntuación: comas, puntos, dos puntos, punto y coma, signos de interrogación y exclamación.

```Python
import re
def check_punctuation (text):
  #result = re.search(r"___", text)
  result = re.search(r"[.?!]$", text)
  return result != None

print(check_punctuation("This is a sentence that ends with a period.")) # True
print(check_punctuation("This is a sentence fragment without a period")) # False
print(check_punctuation("Aren't regular expressions awesome?")) # True
print(check_punctuation("Wow! We're really picking up some steam now!")) # True
print(check_punctuation("End of the line")) # False
Restablecer
Here is your output:
True
False
True
True
False

Right on! You're seeing the flexibility of character classes
in regular expressions!
```

- La función repetir_letra_a comprueba si el texto pasado incluye la letra "a" (minúscula o mayúscula) al menos dos veces. Por ejemplo, repetir_letra_a("plátano") es True, mientras que repetir_letra_a("piña") es False. Rellene el código para que esto funcione.

```PYTHON
import re
def repeating_letter_a(text):
  # result = re.search(r"___", text)
  result = re.search(r"[aA].*[aA]", text)
  return result != None

print(repeating_letter_a("banana")) # True
print(repeating_letter_a("pineapple")) # False
print(repeating_letter_a("Animal Kingdom")) # True
print(repeating_letter_a("A is for apple")) # True

Here is your output:
True
False
True
True

You get an A! See how handy the repetition qualifiers can
be, when we're working with lots of different text!
```

- Rellene el código para comprobar si el texto pasado tiene al menos 2 grupos de caracteres alfanuméricos (incluyendo letras, números y guiones bajos) separados por uno o más caracteres de espacio en blanco.

```PYTHON
import re
def check_character_groups(text):
  # result = re.search(r"___", text)
  result = re.search(r"\w\s+", text)
  return result != None

print(check_character_groups("One")) # False
print(check_character_groups("123  Ready Set GO")) # True
print(check_character_groups("username user_01")) # True
print(check_character_groups("shopping_list: milk, bread, eggs.")) # False

Here is your output:
False
True
True
False

You got it! There's no escaping your regular expression
expertise!
```

- Rellene el código para comprobar si el texto pasado se parece a una frase estándar, es decir, si empieza con una letra mayúscula, seguida de al menos algunas letras minúsculas o un espacio, y termina con un punto, un signo de interrogación o de exclamación.

```PYTHON
import re
def check_sentence(text):
  # result = re.search(r"___", text)
  result = re.search(r"^[A-Z].*[.?!]", text)
  return result != None

print(check_sentence("Is this is a sentence?")) # True
print(check_sentence("is this is a sentence?")) # False
print(check_sentence("Hello")) # False
print(check_sentence("1-2-3-GO!")) # False
print(check_sentence("A star is born.")) # True
Here is your output:
True
False
False
False
True

Awesome! You're becoming a regular "regular expression"
writer!
```

- Corrige la expresión regular utilizada en la función reordenar_nombre para que pueda coincidir con segundos nombres, segundas iniciales, así como con apellidos dobles.

```PYTHON
import re
def rearrange_name(name):
  #result = re.search(r"^(\w*), (\w*)$", name)
  result = re.search(r"^(\w*\s?\w+?), (\w*\s?\w*\.?)$", name)
  #version optimizada con IA
  result = re.search(r"^([\w.-]+(?:\s[\w.-]+)*), ([\w.-]+(?:\s[\w.-]+)*)$", name)
  if result == None:
    return name
  return "{} {}".format(result[2], result[1])

name=rearrange_name("Kennedy, John F.")
print(name)
Here is your output:
John F. Kennedy

Nice work! You're doing well using regular expressions to
capture groups.
```

- La función palabras_largas devuelve todas las palabras que tengan al menos 7 caracteres. Rellene la expresión regular para completar esta función.

```PYTHON
import re
def long_words(text):
  # pattern = __________
  pattern = r"\b\w{7,}\b"
  result = re.findall(pattern, text)
  return result

print(long_words("I like to drink coffee in the morning.")) # ['morning']
print(long_words("I also have a taste for hot chocolate in the afternoon.")) # ['chocolate', 'afternoon']
print(long_words("I never drink tea late at night.")) # []

Here is your output:
['morning']
['chocolate', 'afternoon']
[]

Nice job! Your regular expressions are getting more and more
sophisticated!
```

- Añadir a la expresión regular utilizada en la función extract_pid, para devolver el mensaje en mayúsculas entre paréntesis, después del ID de proceso.

```PYTHON
import re
def extract_pid(log_line):
    #     regex = r"\[(\d+)\]___"
    regex = r"\[(\d+)\]: (\b[A-Z]+\b)"
    result = re.search(regex, log_line)
    if result is None:
        return None
    # return "{} ({})".format(___)
    return "{} ({})".format(result[1],result[2])

print(extract_pid("July 31 07:51:48 mycomputer bad_process[12345]: ERROR Performing package upgrade")) # 12345 (ERROR)
print(extract_pid("99 elephants in a [cage]")) # None
print(extract_pid("A string that also has numbers [34567] but no uppercase message")) # None
print(extract_pid("July 31 08:08:08 mycomputer new_process[67890]: RUNNING Performing backup")) # 67890 (RUNNING)
Here is your output:
12345 (ERROR)
None
None
67890 (RUNNING)

You nailed it! You're using the tools you've learned in the
previous lessons, and it shows!
```

- Estamos usando el mismo syslog, y queremos mostrar la fecha, hora e ID de proceso que está dentro de los corchetes. Podemos leer cada línea del syslog y pasar el contenido a la función show_time_of_pid. Rellena los huecos para extraer la fecha, hora e ID de proceso de la línea pasada, y devuelve este formato: Jul 6 14:01:23 pid:29440.

```PYTHON
import re
def show_time_of_pid(line):
  # pattern = _____________
  pattern = r"(^.*\s+)computer.*\[(\d+)\]"
  result = re.search(pattern, line)
  # return ________________
  return result[1] + "pid:" + result[2]

print(show_time_of_pid("Jul 6 14:01:23 computer.name CRON[29440]: USER (good_user)")) # Jul 6 14:01:23 pid:29440

print(show_time_of_pid("Jul 6 14:02:08 computer.name jam_tag=psim[29187]: (UUID:006)")) # Jul 6 14:02:08 pid:29187

print(show_time_of_pid("Jul 6 14:02:09 computer.name jam_tag=psim[29187]: (UUID:007)")) # Jul 6 14:02:09 pid:29187

print(show_time_of_pid("Jul 6 14:03:01 computer.name CRON[29440]: USER (naughty_user)")) # Jul 6 14:03:01 pid:29440

print(show_time_of_pid("Jul 6 14:03:40 computer.name cacheclient[29807]: start syncing from \"0xDEADBEEF\"")) # Jul 6 14:03:40 pid:29807

print(show_time_of_pid("Jul 6 14:04:01 computer.name CRON[29440]: USER (naughty_user)")) # Jul 6 14:04:01 pid:29440

print(show_time_of_pid("Jul 6 14:05:01 computer.name CRON[29440]: USER (naughty_user)")) # Jul 6 14:05:01 pid:29440

Here is your output:
Jul 6 14:01:23 pid:29440
Jul 6 14:02:08 pid:29187
Jul 6 14:02:09 pid:29187
Jul 6 14:03:01 pid:29440
Jul 6 14:03:40 pid:29807
Jul 6 14:04:01 pid:29440
Jul 6 14:05:01 pid:29440

You got it! You're parsing the syslog and extracting just
the information that we need, with nothing extra!
```

- Ejemplo: Trabajar con archivos de registro

**Introducción**
Te has enfrentado a un programa que lanzaba un error continuamente porque el código fuente era demasiado complicado para encontrar rápidamente el error. La buena noticia es que el programa genera un Archivo de registro que usted puede leer Revisemos cómo escribir un script para buscar el error exacto en el archivo de registro, y luego mostrar ese error en un archivo separado para que pueda averiguar qué está mal.

Este ejemplo es un recorrido de la actividad anterior de Qwiklab, incluyendo instrucciones detalladas y soluciones. Puede utilizar este ejemplo si no pudo completar el laboratorio y/o si necesita una guía adicional para realizar las tareas del laboratorio. También puede consultar este ejemplo para preparar el cuestionario de este módulo.

fishy.log

```
July 31 00:06:21 mycomputername kernel[96041]: WARN Failed to start network connection
July 31 00:09:53 mycomputername updater[46711]: WARN Computer needs to be turned off and on again
July 31 00:12:36 mycomputername kernel[48462]: INFO Successfully connected
July 31 00:13:52 mycomputername updater[43530]: ERROR Error running Python2.exe: Segmentation Fault (core dumped)
July 31 00:16:13 mycomputername NetworkManager[63902]: WARN Failed to start application install
July 31 00:26:45 mycomputername CRON[83063]: INFO I'm sorry Dave. I'm afraid I can't do that
July 31 00:27:56 mycomputername cacheclient[75746]: WARN PC Load Letter
July 31 00:33:31 mycomputername system[25588]: ERROR Out of yellow ink, specifically, even though you want grayscale
July 31 00:36:55 mycomputername updater[73786]: WARN Packet loss
July 31 00:37:38 mycomputername dhcpclient[87602]: INFO Googling the answer
July 31 00:37:48 mycomputername utility[21449]: ERROR The cake is a lie!
July 31 00:44:50 mycomputername kernel[63793]: ERROR Failed process [13966]
```

```PYTHON
#!/usr/bin/env python3


import sys
import os
import re

def error_search(log_file):
  error = input("What is the error? ")
  returned_errors = []
  with open(log_file, mode='r',encoding='UTF-8') as file:
    for log in  file.readlines():
      error_patterns = ["error"]
      for i in range(len(error.split(' '))):
        error_patterns.append(r"{}".format(error.split(' ')[i].lower()))
      if all(re.search(error_pattern, log.lower()) for error_pattern in error_patterns):
        returned_errors.append(log)
    file.close()
  return returned_errors

def file_output(returned_errors):
  with open(os.path.expanduser('~') + '/data/errors_found.log', 'w') as file:
    for error in returned_errors:
      file.write(error)
    file.close()


if __name__ == "__main__":
  log_file = sys.argv[1]
  returned_errors = error_search(log_file)
  file_output(returned_errors)
  sys.exit(0)
```
