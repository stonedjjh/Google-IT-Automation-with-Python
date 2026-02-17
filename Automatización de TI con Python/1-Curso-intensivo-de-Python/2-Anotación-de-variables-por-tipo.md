# Anotación de variables por tipo

La anotación Type permite comunicar claramente los tipos de argumento y de retorno de las funciones en el código. Es como darte a ti mismo y a otros desarrolladores pistas sobre qué tipo de datos se supone que debe contener la variable. Esto tiene varias ventajas: Reduce la posibilidad de cometer errores comunes, ayuda a documentar el código para que otros puedan reutilizarlo y permite que el software de desarrollo integrado (IDE) y otras herramientas ofrezcan una mejor información.

En esta lectura, aprenderás más sobre la anotación de variables por tipo y las mejores prácticas.

## Cómo anotar una variable

Piense en la anotación de una variable como si fuera a poner una etiqueta en un contenedor, y cualquier cosa en ese contenedor debería contener lo que la etiqueta está describiendo. Veamos un ejemplo:

`nombre: str = "Betty"`

El nombre de la variable se declara con dos puntos (:) y se anota con el tipo str, que indica que la variable nombre debe contener un valor de cadena. Y mira, así es Betty -o cualquier nombre- es una cadena, y sabemos que es una cadena porque está entre comillas. Veamos otro ejemplo en el que una variable contiene un valor entero.

`age: int = 34`

En este ejemplo, age es la variable, y int es la anotación de tipo que le proporciona a usted y a otros desarrolladores una pista de que la variable de edad debe almacenar un valor entero.

> [!TIP]
> Si una función espera una lista de enteros, debe anotarla como `List[int]`, no sólo `List`. Ser específico con los tipos puede detectar más errores potenciales y malentendidos.

## Tipado dinámico

Muchos lenguajes, como C# o Java, requieren que declares los tipos de las variables, pero no Python. Una de las grandes cosas de Python es que el tipo de variable puede cambiar con el tiempo a medida que se le asignan nuevos valores. Por ejemplo:

`a = 3                  #a is an integer`

`a = "Hello world"      #a is now a string`

El tipado dinámico permite a los programadores escribir código más rápidamente y ofrece flexibilidad porque no tienes que declarar explícitamente el tipo de variable.

> [!NOTE]
> Python decide cuál de los tipos incorporados es la variable y, por tanto, cómo debe comportarse. Para más información, consulta este artículo sobre [Tipos incorporados](https://docs.python.org/3/library/stdtypes.html).

## Tipado de pato

Esta forma de tipado viene del dicho "Si camina como un pato y grazna como un pato, debe ser un pato" Python inferirá el tipo de la variable en tiempo de ejecución y decidirá qué comportamientos están disponibles para el objeto dado.

`a = "Hello world" #looks like a string`

## Anotar variables con comentarios de tipo

Otra forma de anotar variables es usar comentarios de tipo donde el intérprete ignorará los comentarios.

`captain = "Picard" # type: str`

> [!NOTE]
> Esta forma de anotar variables puede ser útil para casos en los que necesite saber qué tipos pertenecen a qué variables, pero no quiera la sobrecarga de usar un intérprete de línea (linter) o IDE en esta variable específica.

## Anotar variables directamente

Usemos el mismo ejemplo anterior para anotar una variable directamente.

`captain: str = "Picard"`

> [!NOTE]
> Puede que escuche que anotar variables directamente es la forma más "moderna" de anotar una variable.

Otra ventaja es que puedes usar herramientas automatizadas como linters, o mypy, para comprobar tipos y hacer el código más resistente. La mayoría de los IDEs modernos, como VS Code y JetBrains PyCharm, escanean el código en busca de anotaciones de tipo y pueden usarlo para ayudarte a escribir mejor código más rápidamente

## Cómo afectan las anotaciones de tipo al comportamiento en tiempo de ejecución

Cada vez que se llama a una librería, o un IDE trabaja para escanear tu código, se requiere más sobrecarga computacional.

> [!TIP]
> Sea estratégico cuando anote variables por tipo. Esto puede añadir una sobrecarga innecesaria cuando se usa en exceso.

La anotación por tipo es menos común entre los usuarios de Python en la ciencia de datos, ya que puede ser pesado mapear manualmente los datos cada vez que llega un nuevo conjunto de datos. Por otro lado, cuando se hace programación orientada a objetos o se escriben funciones, el uso de anotaciones de tipo se vuelve extremadamente importante porque ayuda a clarificar el código ya que se está tratando con algo más que los tipos incorporados.

## Puntos clave

Anotar variables por tipo proporciona a los programadores beneficios para hacer el código más fácil de leer y entender. Python proporciona diferentes opciones sobre cómo anotar variables, así que elige cómo quieres anotarlas. Sólo ten cuidado de no anotar demasiado, creando una sobrecarga innecesaria en tu código.

## Variables Anotadas por Tipo

Las anotaciones de tipo son opcionales en Python. Sin embargo, pueden ser muy útiles porque facilitan la lectura del código. Las anotaciones hacen que los tipos de variables sean claros para los que leen el código. También pueden ayudar a detectar errores durante la compilación. En el siguiente ejemplo, estamos utilizando el módulo de tipado para anotar los diferentes tipos de variables.

```python
import typing
# Define a variable of type str
z: str = "Hello, world!"
# Define a variable of type int
x: int = 10
# Define a variable of type float
y: float = 1.23
# Define a variable of type list
list_of_numbers: typing.List[int] = [1, 2, 3]
# Define a variable of type tuple
tuple_of_numbers: typing.Tuple[int, int, int] = (1, 2, 3)
# Define a variable of type dict
dictionary: typing.Dict[str, int] = {"key1": 1, "key2": 2}
# Define a variable of type set
set_of_numbers: typing.Set[int] = {1, 2, 3}
```
