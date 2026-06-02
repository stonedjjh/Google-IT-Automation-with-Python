# Gestión de excepciones

El manejo de excepciones en Python es un método que permite a los desarrolladores gestionar los errores o excepciones que pueden ocurrir durante la ejecución de un programa. Las excepciones son errores que interrumpen el flujo normal de un programa y de los que el código no puede recuperarse automáticamente.

algunos ejemplos de excepciones son los siguientes

- Intentar dividir por cero

- Hacer referencia a una variable que no existe

- Intento de abrir un archivo que no existe

- Falla la conexión a un servidor remoto

Manejo de excepciones es un código especial que puede añadir a su programa para asegurarse de que un programa no se bloquea cuando se produce un error. Este método también proporciona la oportunidad de responder a los errores de una manera controlada y significativa.

## Tipos de excepciones más comunes

Cuando se produce un error mientras se ejecuta un programa, puede ocurrir una de las excepciones incorporadas en Python. Algunos de los tipos de excepción más comunes en Python son los siguientes:

- `NameError` - normalmente debido a un error tipográfico en el nombre de una variable

- `AttributeError` - también suele deberse a un error tipográfico, al llamar a un método sobre un objeto

- `ValueError` - el valor de un parámetro es incorrecto

- `TypeError` - al enviar una cadena cuando una función espera un int o al llamar a una función con el número o tipo de argumentos incorrectos

- `ImportError` - cuando Python no puede encontrar un módulo que estás intentando importar

- `FileNotFoundError` - al intentar realizar operaciones relacionadas con archivos (abrir, leer, escribir o borrar) en un archivo o directorio que no existe

## `except` sentencias

En Python, se utiliza la sentencia `except` como parte del manejo de excepciones para atrapar y manejar tipos específicos de excepciones que pueden ocurrir durante la ejecución de un programa. Se utiliza para recuperarse del error o notificar al usuario.

Un ejemplo de sentencia `except` es:

```PYTHON
try:
  # Try to append to a file that is normally not writable
  # for anyone other than root
  f = open("/etc/hosts", "w+")
except IOError as ex:
  # The variable "ex" will hold details about the error
  # that occurred
  print("Error appending to file: " + str(ex))
else:
  # If there was no exception, close the file.
```

## Diferencias con los errores de sintaxis y las excepciones

Como su nombre indica, los errores de sintaxis son el resultado de una sintaxis incorrecta en el código. Hacen que Python termine el programa. Los errores de sintaxis normalmente ocurren debido a errores tipográficos en el código, como sangrar incorrectamente una línea o escribir mal el nombre de una variable o función.

Cuando un programa es sintácticamente correcto, pero el código produce un error, se producen excepciones. Aunque este error no impide que la aplicación se ejecute, altera la forma en que el programa se ejecuta normalmente.

Los errores de sintaxis están relacionados con la estructura y la gramática del código y se detectan antes de que el programa se ejecute; en cambio, las excepciones son errores de ejecución que se producen mientras el programa se está ejecutando y suelen estar relacionados con condiciones inesperadas u operaciones no válidas. Los errores de sintaxis impiden que el programa se ejecute, mientras que las excepciones pueden detectarse y gestionarse para que el programa siga ejecutándose a pesar de los errores.

## Evitar el código defensivo

El código defensivo es un tipo de codificación que pretende anticipar y manejar condiciones excepcionales, errores o entradas inesperadas de forma que se evite que el programa se bloquee o se comporte de forma impredecible. Los programadores de Python, también conocidos como Pythonistas, suelen decir que "es mejor pedir perdón que permiso" Esto significa que en lugar de añadir un montón de código defensivo, deberías simplemente operar como de costumbre y atrapar las excepciones si se producen.

Es decir, en lugar de hacer esto

```PYTHON
if isinstance(user, dict) and "first_name" in user:
  first_name = user["first_name"]
```

Haz esto en su lugar:

```PYTHON
try:
  first_name = user["first_name"]
except KeyError:
  print("User does not have a first_name field")
```

## Puntos clave

Manejo de excepciones en Python es un mecanismo que te permite manejar errores y situaciones excepcionales que pueden ocurrir durante la ejecución de un programa. Hay una gran cantidad de tipos de excepción, pero algunas de las más comunes son NameError, AttributeError, ValueError, TypeError, y ImportError. Los errores de sintaxis están relacionados con la estructura y la gramática del código y se detectan antes de que se ejecute el programa. En cambio, las excepciones son errores de ejecución que se producen durante la ejecución del programa, a menudo debido a condiciones inesperadas u operaciones no válidas.
