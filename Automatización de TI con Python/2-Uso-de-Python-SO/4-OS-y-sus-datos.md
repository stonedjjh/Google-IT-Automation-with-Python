# Sistema Operativo

En este archivo veremos cómo interactuar con el **OS** desde Python.

## `input`

El comando `input` permite capturar entradas de datos de la entrada estándar del **OS**; en una PC sería el teclado.

```python
cat hello.py
#!/usr/bin/env python3

name = input("Please enter your name: ")
print("Hello, " + name)
```

> [!TIP]
> La entrada de datos siempre se considera un string. Para tratarla como otro tipo de dato, hay que hacer una conversión.

```PYTHON
def to_seconds(hours, minutes, seconds):
    return hours*3600+minutes*60+seconds

print("Welcome to this time converter")

cont = "y"
while(cont.lower() == "y"):
    # Se usa int para convertir la entrada a un entero
    hours = int(input("Enter the number of hours: "))
    minutes = int(input("Enter the number of minutes: "))
    seconds = int(input("Enter the number of seconds: "))

    print("That's {} seconds".format(to_seconds(hours, minutes, seconds)))
    print()
    cont = input("Do you want to do another conversion? [y to continue] ")

print("Goodbye!")
```

## Conceptos de I/O Streams en Automatización

Los flujos de datos son la columna vertebral de la interacción con el Sistema Operativo.

Un I/O stream (flujo de entrada/salida) es un canal lógico o abstracción que permite la transferencia secuencial de datos entre un programa y una fuente o destino externo.

En lugar de manejar directamente el hardware, el programador interactúa con el stream, el cual se encarga de mover los bytes de un punto a otro de manera ordenada.

**Conceptos clave:**

- **Input Stream (Flujo de entrada):** Se utiliza para leer datos desde una fuente (teclado, archivo, red) hacia la memoria de la aplicación.

- **Output Stream (Flujo de salida):** Se utiliza para escribir datos desde la aplicación hacia un destino (pantalla, archivo, impresora).

- **Naturaleza secuencial:** Los datos se procesan uno tras otro, como si fuera una cinta o una tubería.

### 1. Abstracción de Hardware

El programa no necesita saber si el dato viene de un disco SSD o de un teclado mecánico; solo sabe que está recibiendo datos de un _stream_.

### 2. Buffering

Muchos streams utilizan un "buffer" (memoria temporal) para acumular datos y transferirlos en bloques, lo que mejora significativamente el rendimiento de la aplicación.

### 3. Cierre de Streams

Es vital cerrar los flujos (como archivos) al terminar de usarlos para liberar recursos del SO y asegurar que el buffer se vacíe correctamente (`flush`).

> [!IMPORTANT]
> En Python, la función `input()` lee del flujo `stdin`, mientras que `print()` escribe en el flujo `stdout`.

## STDIN SDTOUT STDERR

En el contexto de los sistemas operativos y Python, estos son los tres flujos estándar de comunicación (I/O streams) que se crean automáticamente cuando se inicia un proceso.

### Los Tres Flujos Estándar

| Flujo        | Nombre Completo | Descripción                                             | Uso en Python        |
| :----------- | :-------------- | :------------------------------------------------------ | :------------------- |
| **`stdin`**  | Standard Input  | La fuente de entrada (por defecto, el teclado).         | `input()`            |
| **`stdout`** | Standard Output | El destino de la salida (por defecto, la pantalla).     | `print()`            |
| **`stderr`** | Standard Error  | Un canal separado para mensajes de error y diagnóstico. | `sys.stderr.write()` |

---

### Detalles Técnicos

- **Independencia de flujos:** Aunque `stdout` y `stderr` suelen mostrarse ambos en la pantalla, son canales distintos. Esto permite que un administrador de sistemas guarde los resultados de un script en un archivo, pero siga viendo los errores en la pantalla.
- **Redirección:** Es posible redirigir estos flujos usando operadores en la terminal (como `>` para salida o `2>` para errores).
- **Módulo `sys`:** En Python, para interactuar directamente con estos flujos de forma avanzada, se utiliza el módulo `sys` (`sys.stdin`, `sys.stdout`, `sys.stderr`).

---

### Anotación-de-variables-por-tipo.md

```markdown
### Gestión de Flujos Estándar (I/O)

La interacción profesional con el SO requiere entender que la salida de datos no siempre es lineal.

#### 1. Standard Input (stdin)

Es el canal por donde el programa recibe instrucciones externas. En Python, `input()` lee de este flujo y detiene la ejecución hasta recibir un carácter de nueva línea (`\n`).

#### 2. Standard Output (stdout)

Es el canal de datos "limpios". Se usa para los resultados que el usuario o el siguiente programa en una tubería (pipe) esperan recibir.

#### 3. Standard Error (stderr)

Es el canal "sucio". Se reserva para reportar fallos, advertencias o logs de depuración. Separar los errores del resultado principal evita que scripts automatizados procesen mensajes de error como si fueran datos válidos.

> [!TIP]
> Al automatizar, puedes usar `sys.exit("Mensaje de error")` para escribir automáticamente en `stderr` y terminar el programa con un código de error.
```

```PYTHON
cat streams.py
#!/usr/bin/env python3

data = input("This will come from STDIN: ")
print("Now we write it to STDOUT: " + data)
print("Now we generate an error to STDERR: " + data + 1)
```

## Variables de Entorno

Con Python podemos acceder a las variables de entorno almacenadas en el sistema.

```bash
echo $PATH
# Salida /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
cat variables.py
#!/usr/bin/env python3
import os
# Al usar el método get se asegura de que no dé error; si no existe la variable, se le da un valor por defecto.
print("HOME: " + os.environ.get("HOME", ""))
print("SHELL: " + os.environ.get("SHELL", ""))
print("FRUIT: " + os.environ.get("FRUIT", ""))
./variables.py
# HOME: /home/user
# SHELL: /bin/bash
# FRUIT:
export FRUIT=Pineapple
./variables.py
# HOME: /home/user
# SHELL: /bin/bash
# FRUIT: Pineapple
```

## Argumentos en la linea de comandos

Con el módulo `sys` se pueden obtener los parámetros que se pasan al ejecutar un script o programa de python

parameters.py

```PYTHON
#!/usr/bin/env python3

import sys
print(sys.argv)
```

```bash
./parameters.py
#Salida ['parameters.py']

./parameters.py one two three
#Salida ['parameters.py', 'one', 'two', 'three']
```

## exit code

Al ejecutar un comando en el **OS**, este devolverá 0 si se ejecutó con éxito u otro número si la ejecución falló. Para obtener el exit code de un programa se puede usar el comando `$?`.

```bash
#wc cuenta las líneas, palabras y caracteres en un archivo
wc variable.py
# salida: 7 19 174 variables.py
echo $?
# salida: 0

# veamos qué pasa cuando hay un error

wc notpresent.py
#salida wc: notpresent.py: No such file or directory
echo $?
# salida: 1
```

> [!IMPORTANT]
> Se puede usar `sys.exit(1)` para devolver un exit code.

### Gestión de Códigos de Salida (Exit Codes)

Entender los códigos de salida es fundamental para escribir scripts que puedan comunicarse con el Sistema Operativo.

#### 1. Código 0 (Éxito)

Representa una ejecución limpia. En Python, si el script llega al final sin excepciones y sin llamar a `sys.exit()`, el SO recibe un 0 por defecto.

#### 2. Códigos 1-255 (Errores)

- **1**: Error general.
- **2**: Mal uso de comandos integrados.
- **126**: El comando invocado no tiene permisos de ejecución.
- **127**: Comando no encontrado.

#### 3. Implementación en Python

Usar `sys.exit(n)` permite que nuestros scripts detengan procesos en cascada si algo falla. Por ejemplo, un script de validación de datos debería devolver `sys.exit(1)` si encuentra datos corruptos.

> [!TIP]
> Puedes verificar el éxito de tu último comando en la terminal ejecutando `echo $?`.

## `subprocess`

El módulo `subprocess` permite ejecutar comandos del **SO** en un ambiente aislado. Este proceso es síncrono, por lo cual, mientras se esté ejecutando el subproceso (que llamaremos hijo), este tomará el flujo de control del script y, cuando termine su ejecución, retornará el flujo al padre.

```PYTHON
import subprocess
subprocess.run(["date"])
subprocess.run(["sleep", "2"])
result = subprocess.run(["ls", "this_file_does_not_exist"])
print(result.returncode)

# Otro ejemplo
result = subprocess.run(["host", "8.8.8.8"], capture_output=True)
print(result.returncode)
# Salida: 0
print(result.stdout)
# Salida: b'8.8.8.8.in-addr.arpa domain name pointer dns.google.\n'
# la b al principio indica que es una matriz de bytes
print(result.stdout.decode().split())
# Salida: ['8.8.8.8.in-addr.arpa', 'domain', 'name', 'pointer', 'dns.google.']

# Qué pasa si el comando falló
result = subprocess.run(["rm", "does_not_exist"], capture_output=True)
print(result.returncode)
# Salida: 1
print(result.stdout)
# Salida: b''
print(result.stderr)
# Salida: b"cannot remove 'does_not_exist': No such file or directory\n"

```

> [!WARNING]
> `capture_output` fue introducido en python 3.7

## Matrices de bytes (`bytes` objects)

Al capturar la salida de un comando con `subprocess`, Python recibe datos binarios del sistema operativo. Estos se representan como una **matriz de bytes**, identificada por el prefijo `b''` delante de las comillas.

### Características principales

- **Naturaleza binaria**: Representan una secuencia de números del 0 al 255. A diferencia de los strings, los bytes no contienen caracteres, sino valores numéricos que el sistema interpreta.
- **Inmutabilidad**: Al igual que los strings de Python, las matrices de bytes no pueden modificarse una vez creadas.
- **Independencia de codificación**: El SO entrega bytes porque no sabe qué tipo de texto (UTF-8, ASCII, etc.) está enviando el proceso hijo; simplemente entrega la información cruda.

### Operaciones esenciales

Para poder trabajar con estos datos como texto legible, es necesario realizar una conversión:

1. **`.decode()`**: Transforma los bytes en un string (caracteres). Es el paso necesario para usar métodos como `.split()`, `.strip()` o búsquedas de texto.
2. **`.encode()`**: Realiza la operación inversa, transformando un string en bytes (necesario si queremos enviar datos a un proceso que espera una entrada binaria).

```python
# Captura de salida (Bytes)
result = subprocess.run(["echo", "Hola"], capture_output=True)
print(result.stdout) # Salida: b'Hola\n'

# Transformación a texto (String)
texto = result.stdout.decode().strip()
print(texto) # Salida: Hola
```

> [!TIP]
> Si quieres que subprocess haga la conversión automáticamente, puedes pasar el argumento encoding="utf-8" o text=True dentro de subprocess.run(). Esto hará que stdout y stderr devuelvan strings en lugar de bytes.

## Gestión Avanzada de subprocesos

```PYTHON
import os
import subprocess

my_env = os.environ.copy()
my_env["PATH"] = os.pathsep.join(["/opt/myapp/", my_env["PATH"]])

result = subprocess.run(["myapp"], env=my_env)
```
