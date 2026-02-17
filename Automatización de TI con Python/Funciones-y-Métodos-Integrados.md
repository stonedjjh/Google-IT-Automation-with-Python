# Funciones y Métodos integradas

Son un conjuntos de funciones o métodos que viene ya predefinidas en el lenguaje.

## Indice de Funciones o métodos Generales

- [`len()`](#len)
- [`max()`](#max)
- [`min()`](#min)
- [`print()`](#print)
- [`sorted()`](#sorted)
- [`type()`](#type)
- [`enumerate()`](#enumerate)

## Indice de Funciones o métodos de Conversión

- [`float()`](#float)
- [`int()`](#int)
- [`str()`](#str)

## Indice de métodos de Cadena

- [`join()`](#join)
- [`split()`](#split)
- [`index()`](#index)
- [`upper()`](#upper)
- [`lower()`](#lower)
- [`strip()`](#strip)
- [`lstrip()`](#lstrip)
- [`rstrip()`](#rstrip)
- [`count()`](#count)
- [`endswith()](#endswith)
- [`isnumeric()](#isnumeric)
- [`isalpha()](#isalpha)
- [`replace()`](#replace)

## Indice de Funciones o métodos Numerica

- [`range()`](#range)

## print

la funcion `print()` se utiliza para mostrar información en la consola o salida estándar.

```python
print("Hola, Mundo!")  # Muestra el texto en la consola
print(5 + 3)           # Muestra el resultado de una operación matemática
```

## type

La función `type()` devuelve el tipo de dato de un valor o variable.

```python
print(type(5))          # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type("Hola"))     # <class 'str'>
print(type([1, 2, 3])) # <class 'list'>
```

## len

La función `len()` devuelve la longitud (número de elementos) de un objeto.

```python
print(len("Hola"))        # 4
print(len([1, 2, 3, 4]))  # 4
print(len((1, 2, 3)))     # 3
print(len({"a": 1, "b": 2})) # 2
```

## str

La función `str()` convierte un valor a una cadena de texto (string).

```python
num = 42
texto = str(num)
print(texto)          # "42"
print(type(texto))    # <class 'str'>
```

## int

La función `int()` convierte un valor a un número entero.

```python
num_str = "42"
num = int(num_str)
print(num)          # 42
print(type(num))    # <class 'int'>
num_float = 42.7
num2 = int(num_float)
print(num2)         # 42
print(type(num2))   # <class 'int'>
```

## float

La función `float()` convierte un valor a un número de punto flotante.

```python
num_str = "3.14"
num = float(num_str)
print(num)          # 3.14
print(type(num))    # <class 'float'>
num_int = 5
num2 = float(num_int)
print(num2)         # 5.0
print(type(num2))   # <class 'float'>
```

## max

La función `max()` devuelve el valor máximo de un conjunto de valores o de un iterable.

```python
print(max(5, 10, 3))               # 10
print(max([1, 4, 2, 8, 5]))        # 8
print(max("hola"))                  # 'o' (valor máximo según orden alfabético)
```

## min

La función `min()` devuelve el valor mínimo de un conjunto de valores o de un iterable.

```python
print(min(5, 10, 3))               # 3
print(min([1, 4, 2, 8, 5]))        # 1
print(min("hola"))                  # 'a' (valor mínimo según orden alfabético)
```

## sorted

La función `sorted()` devuelve una nueva lista con los elementos de un iterable ordenados.

```python
print(sorted([5, 2, 9, 1]))        # [1, 2, 5, 9]
print(sorted("python"))             # ['h', 'n', 'o', 'p', 't', 'y']
```

> [!WARNING] > **Limitación de Comparación**: La función sorted() fallará si intenta ordenar un iterable que contenga elementos de tipos incompatibles (por ejemplo, números y cadenas de texto, como [1, 2, "hello"]). Esto se debe a que Python no sabe cómo comparar un entero (int) con una cadena (str) usando operadores como < o > y lanzará un error de tipo (TypeError).

## bool

La función bool() convierte un valor a un valor booleano (True o False). Prácticamente todos los objetos en Python tienen un valor booleano asociado.

Falsy Values (Falso): 0 (entero/flotante), None, cadenas vacías (""), listas vacías ([]), diccionarios vacíos ({}), tuplas vacías (()), etc.

Truthy Values (Verdadero): Cualquier otro valor (cualquier número distinto de cero, cadenas/listas no vacías, etc.).

```python
print(bool(1))        # True (número distinto de cero)
print(bool(0))        # False (cero)
print(bool("hola"))   # True (cadena no vacía)
print(bool(""))       # False (cadena vacía)
print(bool([]))       # False (lista vacía)
```

## range

La función `range()` genera una secuencia de números enteros.

```python
print(list(range(5)))          # [0, 1, 2, 3, 4]
print(list(range(2, 8)))       # [2, 3, 4, 5, 6, 7]
print(list(range(1, 10, 2)))   # [1, 3, 5, 7, 9] incremento positivo
print(list(range(5, 0, -1)))  # [5, 4, 3, 2, 1] incremento negativo
```

La función range puede tener entre 1 y 3 parametros

- `range(stop)`: Genera números desde 0 hasta stop-1.

- `range(start, stop)`: Genera números desde start hasta stop-1.

- `range(start, stop, step)`: Genera números desde start hasta stop-1 con incrementos de step

> [!TIP]
> El límite superior es exclusivo
> En Python 3, range no crea la lista completa en la memoria inmediatamente (por eso usas list() para verla). Es un "objeto de rango" que va entregando los números uno a uno, lo cual es muy útil cuando trabajas con rangos de millones de números.

## join

La función `join()` se utiliza para concatenar elementos de una lista de cadenas en una sola cadena, utilizando un delimitador específico.

```python
greetings = ["Hola", "mundo", "Python"]
result = " ".join(greetings)
print(result)  # "Hola mundo Python"
```

## split

La función `split()` se utiliza para dividir una cadena en una lista de subcadenas, utilizando un delimitador específico.

```python
text = "Hola mundo Python"
result = text.split(" ")
print(result)  # ["Hola", "mundo", "Python"]
```

## index

La función `index()` se utiliza para encontrar la posición de la primera aparición de un elemento en una lista o cadena.

```python
my_list = ['a', 'b', 'c', 'd']
print(my_list.index('c'))  # 2

my_string = 'hello world'
print(my_string.index('o'))  # 4

pets = "Cats & Dogs"
pets.index("Dog") # 7

```

## upper

La función `upper()` se utiliza para convertir todos los caracteres de una cadena a mayúsculas.

```python
"Mountains".upper()
#MOUNTAINS
```

## lower

La función `lower()` se utiliza para convertir todos los caracteres de una cadena a minúsculas.

```python
"Mountains".lower()
# mountains
```

## strip

La función `strip()` se utiliza para eliminar los espacios en blanco al principio y al final de una cadena.

```python
" yes ".strip()
# 'yes'
```

## lstrip

La función `lstrip()` se utiliza para eliminar los espacios en blanco al principio de una cadena.

```python
" yes ".lstrip()
# 'yes '
```

## rstrip

La función `rstrip()` se utiliza para eliminar los espacios en blanco al final de una cadena.

```python
" yes ".rstrip()
# ' yes'
```

## count

La función `count()` se utiliza para contar el número de veces que un elemento específico aparece en una cadena o lista.

```python
"The number of times e occurs in this string is 4".count("e")
# 4
```

## endswith

Método que devuelve True si la cadena termina con el sufijo especificado; de lo contrario, devuelve False.

```Python
"Forest".endswith("rest")
# True
```

## isnumeric

Método que devuelve True si todos los caracteres de la cadena son caracteres numéricos; de lo contrario, devuelve False.

```Python
"Forest".isnumeric()
# False
"12345".isnumeric()
# True
```

## isalpha

Método que devuelve True si todos los caracteres de la cadena son letras del alfabeto; de lo contrario, devuelve False.

```Python
print("xyzzy".isalpha())                # prints True
```

## replace

string.replace(old, new) - Devuelve una nueva cadena donde todas las apariciones de old han sido reemplazadas por new.

```Python
print(test.replace("wood", "plastic"))  # prints "How much plastic would a plasticchuck chuck"
```

## enumerate

La función `enumerate()` toma una colección (como una lista) y devuelve un objeto enumerado. En cada iteración de un bucle, entrega una **tupla** que contiene el índice y el valor del elemento actual. Es la forma eficiente de obtener el índice sin usar `range(len())`.

```python
winners = ["Ashley", "Dylan", "Reese"]

# Uso básico con desempaquetado (unpacking)
for index, person in enumerate(winners):
    print("{} - {}".format(index + 1, person))

# 1 - Ashley
# 2 - Dylan
# 3 - Reese
```

> [!TIP]
> Puedes pasar un segundo argumento opcional a enumerate(iterable, start) para indicar en qué número quieres que empiece a contar el índice.
> `enumerate(winners, start=1)` empezaría a contar desde 1 directamente.
