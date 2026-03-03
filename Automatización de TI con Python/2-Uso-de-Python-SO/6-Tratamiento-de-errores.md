# Tratamiento de errores

Has aprendido que, en algunos casos, es mejor generar un error tú mismo, y cómo comprobar que se genera el error correcto cuando eso es lo que esperas. También has aprendido a probar tu código para verificar que hace lo que debe. En esta lectura, aprenderás sobre la sintaxis del manejo de errores, incluyendo el lanzamiento de excepciones, el uso de una sentencia assert, y las cláusulas `try` y `except`.

## Manejo de excepciones

Cuando se realiza el manejo de excepciones, es importante predecir qué excepciones pueden ocurrir. A veces, para averiguar qué excepciones necesitas tener en cuenta, tienes que dejar que tu programa falle.

La forma más simple de manejar excepciones en Python es usando las cláusulas `try` y `except`.

En la cláusula `try`, Python ejecuta todas las sentencias hasta que encuentra una excepción. Usas la cláusula `except` para atrapar y manejar la(s) excepción(es) que Python encuentra en la cláusula `try`.

Este es el proceso de cómo funciona:

1. Python ejecuta la cláusula `try`, por ejemplo, la(s) sentencia(s) entre las palabras clave `try` y `except`.

2. Si no se produce ningún error, Python se salta la cláusula `except` y finaliza la ejecución de la sentencia `try`.

3. Si se produce un error durante la ejecución de la cláusula `try`, Python se salta el resto de la cláusula `try` y transfiere el control al bloque `except` correspondiente. Si el tipo de error coincide con lo que se indica después de la palabra clave `except`, Python ejecuta la cláusula `except`. La ejecución continúa después del bloque `try`/`except`.

4. Si se produce una excepción pero no coincide con lo que aparece en la cláusula `except`, se pasa a las sentencias `try` fuera de ese bloque `try`/`except`. Sin embargo, si no se puede encontrar un manejador para esa excepción, la excepción se convierte en una excepción no manejada, la ejecución se detiene, y Python muestra un mensaje de error designado.

A veces, una sentencia `try` puede tener más de una cláusula `except` para que el código pueda especificar manejadores para diferentes excepciones. Esto puede ayudar a reducir el número de excepciones no manejadas.

Puedes usar excepciones para atrapar casi todo. Es una buena práctica como desarrollador o programador ser tan específico como sea posible con los tipos de excepciones que intentas manejar, especialmente si estás creando tus propias excepciones.

## Lanzar excepciones

Como desarrollador o programador, es posible que quieras lanzar un error tú mismo. Normalmente, esto ocurre cuando algunas de las condiciones necesarias para que una función haga su trabajo correctamente no se cumplen y devolver ninguno o algún otro valor base no es suficiente. Puedes lanzar un error o lanzar una excepción (también conocido como "lanzar una excepción"), que fuerza a que se produzca una excepción en particular, y te notifica que algo en tu código va mal o que se ha producido un error.

He aquí algunos casos en los que lanzar una excepción es una herramienta útil:

- Un archivo no existe

- Falla una conexión de red o de base de datos

- Su código recibe una entrada no válida

En el ejemplo siguiente, el código lanza dos excepciones incorporadas en Python: `raise ValueError` y `raise ZeroDivisionError`. Puedes encontrar más información sobre estas excepciones en el siguiente ejemplo, junto con explicaciones de los errores potenciales que pueden ocurrir durante una excepción.

## Ejemplo de manejo de excepciones

Ahora que ya conoces las cláusulas try y except, las sentencias assert y la generación de excepciones, considera los siguientes ejemplos de código que utilizan todos estos conceptos juntos.

La estructura básica del manejo de excepciones es la siguiente:

```PYTHON
# File reading function with exception handling
def read_file(filename):
    try:
        with open(filename, 'r') as f:
            return f.read()
    except FileNotFoundError:
        return "File not found!"
    finally:
        print("Finished reading file.")
```

Imagine que tiene una función que lee datos de un fichero y luego divide dos números proporcionados dentro de ese fichero. Hay algunos fallos en ella que puedes atrapar con excepciones.

```PYTHON
def faulty_read_and_divide(filename):
    with open(filename, 'r') as file:
        data = file.readlines()
        num1 = int(data[0])
        num2 = int(data[1])
        return num1 / num2
```

Hay varios problemas potenciales aquí:

- El archivo podría no existir, causando un `FileNotFoundError`.

- El fichero podría no tener suficientes líneas de datos, provocando un `IndexError`.

- Los datos del fichero podrían no ser convertibles a números enteros, lo que provocaría un `ValueError`.

- El segundo número podría ser cero, lo que provocaría un `ZeroDivisionError`.

Para solucionar estos posibles problemas, puede añadir el manejo de excepciones adecuado que se ilustra a continuación:

```PYTHON
def enhanced_read_and_divide(filename):
    try:
        with open(filename, 'r') as file:
            data = file.readlines()
            
        # Ensure there are at least two lines in the file
        if len(data) < 2:
            raise ValueError("Not enough data in the file.")
            
        num1 = int(data[0])
        num2 = int(data[1])
            
        # Check if second number is zero
        if num2 == 0:
            raise ZeroDivisionError("The denominator is zero.")
            
        return num1 / num2


    except FileNotFoundError:
             return "Error: The file was not found."
    except ValueError as ve:
             return f"Value error: {ve}"
    except ZeroDivisionError as zde:
             return f"Division error: {zde}"
```

Ahora, la función `enhanced_read_and_divide` está equipada para gestionar las posibles excepciones con elegancia, proporcionando mensajes de error informativos a la persona que llama. De esta forma, el código explicará cuándo falla, ya que ha identificado zonas de fallo potenciales, como cuando se trata de entradas impredecibles o contenido de archivos.

Observa cómo las excepciones se instancian como objetos (como `ValueError ve`) que puedes utilizar para diagnosticar el problema imprimiéndolos.

Los errores deben leerse:

**`File-level issues:`**

**`Value error: Not enough data in the file.`**

**`Error: The file was not found.`**

**`Data-level issues:`**

**`Value error: invalid literal for int() with base 10: 'apple'`**

**`Division error: The denominator is zero.`**

## assert sentencias

**`assert`** las sentencias te ayudan a verificar si se cumple una determinada condición y lanzar una excepción en caso contrario. Como su nombre indica, su propósito es "afirmar" que ciertas condiciones son verdaderas en puntos específicos de su programa.

La sentencia `assert` existe en casi todos los lenguajes de programación y tiene dos usos principales:

- Ayudar a detectar problemas antes en el desarrollo, en lugar de más tarde, cuando falla alguna otra operación. Los problemas que no se abordan hasta más tarde en el proceso de desarrollo pueden resultar más largos y costosos de solucionar.

- Proporcionar una forma de documentación para otros desarrolladores que lean el código.
