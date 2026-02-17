# Listas(list), Tuplas, Conjuntos(set) y Diccionarios(dict)

Entre las estructuras de datos que tenemos para trabajar en Python se ecnuentran las **Listas**, **Tuplas**, **Conjuntos** y **Diccionarios**

## Listas

Una lista es una colección ordenada y mutable de elementos. Las listas se definen utilizando corchetes `[]` y los elementos se separan por comas.

```python
x = ["Now", "we", "are", "cooking!"]
type(x)
# <class 'list'>
print(x)
# ['Now', 'we', 'are', 'cooking!']
len(x)
# 4
"are" in x
# True
"Today" in x
# False
print(x[0])
print(x[3])
# Now
# cooking!
print(x[4])
# IndexError: list index out of range
print(x[1:3])
# ['we', 'are']
print(x[:2])
# ['Now', 'we']
x[2:]
# ['are', 'cooking!']
```

> [!WARNING]
> Intentar acceder a un índice que no existe en Python lanza un error, a diferencia de JavaScript que devuelve `undefined`.

---

**Caracteristicas:**

- Heterogeneas

- De tamaño dinamico

- Indexadas

- Mutables

---

### **Métodos de Listas:**

Los métodos permiten modificar el contenido de la lista directamente. A diferencia de las funciones generales como `len()`, estos se llaman usando la notación de punto (`lista.método()`).

#### append

Agrega un elemento al final de la lista. Su equivalente en JavaScript es `.push()`.

```python
fruits = ["Pineapple", "Banana"]
fruits.append("Kiwi")
print(fruits) # ['Pineapple', 'Banana', 'Kiwi']
```

#### insert

Inserta un elemento en una posición específica. El primer argumento es el índice y el segundo el valor.

```python
fruits.insert(0, "Orange")
print(fruits) # ['Orange', 'Pineapple', 'Banana', 'Kiwi']
```

#### remove

Elimina la primera aparición de un elemento específico. Si el elemento no existe, lanza un ValueError.

```Python
fruits.remove("Banana")
print(fruits) # ['Orange', 'Pineapple', 'Kiwi']
```

#### pop

Elimina y devuelve el elemento en el índice dado. Si no se proporciona un índice, elimina y devuelve el último elemento.

```Python
item = fruits.pop(0)
print(item)   # 'Orange'
print(fruits) # ['Pineapple', 'Kiwi']
```

#### clear

Elimina todos los elementos de la lista, dejándola vacía.

```Python
fruits.clear()
print(fruits) # []
```

#### index

Devuelve el índice de la primera aparición de un elemento.

```Python
colors = ["red", "blue", "green"]
print(colors.index("blue")) # 1
```

#### sort

Ordena los elementos de la lista de forma ascendente (por defecto). Este método modifica la lista original (in-place).

```Python
numbers = [5, 2, 8, 1, 9]
numbers.sort()
print(numbers) # [1, 2, 5, 8, 9]

# También puedes ordenar de forma descendente
numbers.sort(reverse=True)
print(numbers) # [9, 8, 5, 2, 1]
```

#### reverse

Invierte el orden de los elementos de la lista. No ordena, solo "da la vuelta" a la lista actual.

```Python
colors = ["red", "green", "blue"]
colors.reverse()
print(colors) # ['blue', 'green', 'red']
```

#### copy

Crea una copia superficial de la lista. Es útil para modificar una lista sin alterar la original.

```Python
original = [1, 2, 3]
nueva = original.copy()
nueva.append(4)
print(original) # [1, 2, 3]
print(nueva)    # [1, 2, 3, 4]
```

#### extend

Añade todos los elementos de un iterable (como otra lista) al final de la lista actual. A diferencia de append, que añade la lista completa como un solo elemento, extend añade cada elemento individualmente.

```Python
list1 = [1, 2, 3]
list2 = [4, 5]
list1.extend(list2)
print(list1) # [1, 2, 3, 4, 5]
```

##### Funciones de Transformación (Avanzado)

Estas funciones no son métodos de lista, sino funciones integradas que trabajan con ellas.

###### map

Aplica una función a cada elemento de una lista. Para ver el resultado como lista, debemos convertirlo con list().

```Python
def cuadrado(n):
    return n * n

numbers = [1, 2, 3, 4]
resultado = map(cuadrado, numbers)
print(list(resultado)) # [1, 4, 9, 16]
```

###### zip

Combina dos o más iterables elemento a elemento, creando tuplas de pares. Se detiene cuando el iterable más corto se agota.

```Python
names = ["Ana", "Hugo", "Luis"]
ages = [25, 30, 35]

combinado = zip(names, ages)
print(list(combinado)) # [('Ana', 25), ('Hugo', 30), ('Luis', 35)]
```

---

## Tuplas

Una tupla es una colección ordenada e inmutable de elementos. Se definen utilizando paréntesis () y los elementos se separan por comas. Una vez que se crea una tupla, no puedes cambiar, agregar o eliminar sus elementos.

```Python
fullname = ('Manny', 'D', 'Vera')
type(fullname)
# <class 'tuple'>

print(fullname[0])
# Manny

# Intentar modificarla lanzará un error:
# fullname[1] = 'B'
# TypeError: 'tuple' object does not support item assignment

def convert_seconds(seconds):
  hours = seconds // 3600
  minutes = (seconds - hours * 3600) // 60
  remaining_seconds = seconds - hours * 3600 - minutes * 60
  return hours, minutes, remaining_seconds
result = convert_seconds(5000)
type(result)
# <class 'tuple'>
print(result)
# (1, 23, 20)
hours, minutes, seconds = result #unpacking
print(hours, minutes, seconds)
# 1 23 20
```

**Características:**

- Heterogéneas: Pueden contener diferentes tipos de datos.

- Inmutables: Su contenido y tamaño no pueden cambiar tras su creación.

- Indexadas: Se accede a los elementos mediante su posición (empezando en 0).

- Rápidas: Al ser inmutables, Python las procesa más rápido que a las listas y ocupan menos espacio en memoria.

> [!TIP]
> Las tuplas son ideales para datos que no deben cambiar a lo largo del programa, como las coordenadas geográficas (latitud, longitud) o los días de la semana.

### Función tuple()

Se utiliza para convertir un iterable (como una lista, una cadena o un conjunto) en una tupla. Es muy útil cuando quieres "congelar" los datos de una lista para que ya no puedan ser modificados.

```Python
# Convirtiendo una lista a tupla
frutas_lista = ["Manzana", "Pera", "Uva"]
frutas_tupla = tuple(frutas_lista)

print(frutas_tupla) # ('Manzana', 'Pera', 'Uva')
print(type(frutas_tupla)) # <class 'tuple'>

# Convirtiendo una cadena a tupla
mensaje = "Hola"
print(tuple(mensaje)) # ('H', 'o', 'l', 'a')
```

### Tuplas con objetos mutables

Aunque las tuplas son inmutables, pueden contener objetos mutables, como las listas. Esto significa que, aunque la tupla no puede modificarse (por ejemplo, no se pueden añadir ni eliminar elementos), los elementos mutables que contiene sí pueden modificarse.

```Python
# A tuple with a list as an element
my_tuple = (1, 2, ['a', 'b', 'c'])

# You can't change the tuple itself
# my_tuple[0] = 3  # This would raise a TypeError

# But you can modify the mutable elements within the tuple
my_tuple[2][0] = 'x'
print(my_tuple)  # Outputs: (1, 2, ['x', 'b', 'c'])
```

## Tuplas de un solo elemento (Singleton Tuples)

Para crear una tupla que contenga un solo elemento, es obligatorio incluir una coma final antes de cerrar el paréntesis. Sin la coma, Python interpretará los paréntesis como una agrupación lógica (como en matemáticas) y no como una estructura de datos.

```Python
# Esto NO es una tupla, es un entero
falso_singleton = (5)
print(type(falso_singleton)) # <class 'int'>

# Esto SÍ es una tupla
singleton = (5,)
print(type(singleton)) # <class 'tuple'>
print(len(singleton))  # 1
```

> [!WARNING]
> Este es un error común al pasar argumentos a funciones que esperan una estructura de datos. Recuerda siempre la coma: (elemento,).

---

## Diccionarios (dict)

Un **Diccionario** es una estructura de datos que almacena elementos en pares de **clave:valor**. A diferencia de las listas o tuplas que usan índices numéricos (0, 1, 2...), los diccionarios utilizan claves únicas para acceder a sus valores. Es lo que en otros lenguajes se conoce como _Mapas_, _Hashes_ o _Arreglos Asociativos_.

**Características:**

- **Asociativos:** Permiten relacionar datos de forma lógica (ej. un nombre con un número de teléfono).
- **Claves Únicas:** No puede haber dos claves iguales. Si agregas una clave que ya existe, el valor antiguo se sobrescribe.
- **Mutables:** Puedes añadir, eliminar o modificar elementos después de crear el diccionario.
- **Eficientes:** Están optimizados para encontrar valores muy rápido, incluso si el diccionario es enorme.

**Anatomía:**

Se definen con llaves `{}`. Cada par se separa por una coma, y la clave del valor se separa por dos puntos `:`.

```python
# Ejemplo: Información de un servidor
servidor = {
    "ip": "192.168.1.1",
    "puerto": 8080,
    "estado": "activo"
}

# Acceso al valor mediante la clave
print(servidor["ip"]) # 192.168.1.1
```

### **Métodos de Diccionarios:**

#### keys()

Devuelve una lista (vista) de todas las claves del diccionario.

```Python
print(servidor.keys()) # dict_keys(['ip', 'puerto', 'estado'])
```

#### values()

Devuelve una lista de todos los valores almacenados.

```Python
print(servidor.values()) # dict_values(['192.168.1.1', 8080, 'activo'])
```

#### items()

Devuelve cada par en una tupla dentro de una lista. Es el método más usado para iterar con un bucle for.

```Python
for clave, valor in servidor.items():
print(f"La clave es {clave} y el valor es {valor}")
```

#### get()

Busca una clave. Si no existe, en lugar de lanzar un error (KeyError), devuelve None o un valor por defecto que tú definas.

```Python

# Si la clave "usuario" no existe, devuelve "Anónimo"

print(servidor.get("usuario", "Anónimo"))
```

#### update()

Actualiza el diccionario con elementos de otro diccionario o de un iterable de pares clave-valor.

```Python
servidor.update({"ram": "16GB", "estado": "mantenimiento"})
print(servidor) # 'estado' cambia a mantenimiento y se agrega 'ram'
```

#### pop()

Elimina la clave especificada y devuelve el valor asociado.

```Python
puerto = servidor.pop("puerto")
print(puerto) # 8080
```

#### del

Es una palabra clave de Python (no un método) que se utiliza para eliminar una clave y su valor asociado. Si la clave no existe, lanzará un error KeyError.

```Python
# Continuando con el ejemplo del servidor:
servidor = {"ip": "192.168.1.1", "puerto": 8080, "estado": "activo"}

del servidor["puerto"]

print(servidor)
# {'ip': '192.168.1.1', 'estado': 'activo'}

# También puedes usarlo para borrar el diccionario completo de la memoria:
# del servidor
```

### Iterar sobre el contenido de un diccionario

```Python
file_counts = {"jpg":10, "txt":14, "csv":2, "py":23}
for extension in file_counts:
  print(extension)
"""
jpg
txt
csv
py
"""

for ext, amount in file_counts.items():
  print("There are {} files with the .{} extension".format(amount, ext))

"""
There are 10 files with the .jpg extension
There are 14 files with the .txt extension
There are 2 files with the .csv extension
There are 23 files with the .py extension
"""

file_counts.keys()
# dict_keys(['jpg', 'txt', 'csv', 'py'])

file_counts.values()
#dict_values([10, 14, 2, 23])

for value in file_counts.values():
  print(value)

"""
10
14
2
23
"""

def count_letters(text):
  result = {}
  for letter in text:
    if letter not in result:
      result[letter] = 0
    result[letter] += 1
  return result
count_letters("aaaaa")
#{'a': 5}
count_letters("tenant")
#{'t': 2, 'e': 1, 'n': 2, 'a': 1}
count_letters("a long string with a lot of letters")
# {'a': 2, ' ': 7, 'l': 3, 'o': 3, 'n': 2, 'g': 2, 's': 2, 't': 5, 'r': 2, 'i': 2, 'w': 1, 'h': 1, 'f': 1, 'e': 2}

```

---

## Conjuntos (set)

Un conjunto es una colección desordenada de elementos únicos. Los conjuntos se definen utilizando llaves {} (similar a los diccionarios, pero sin pares clave:valor) o mediante la función set().

**Características:**

- Unicidad: No permite elementos duplicados. Si intentas agregar un valor que ya existe, Python simplemente lo ignora.

- Desordenados: No mantienen un orden específico, por lo que no soportan indexación (no puedes hacer conjunto[0]).

- Eficiencia: Son extremadamente rápidos para verificar si un elemento pertenece al conjunto (item in set) y para realizar operaciones matemáticas.

**Ejemplo:**

```Python
# Creación de un conjunto
paises = {"España", "México", "Colombia", "España"}
print(paises)
# Resultado: {'España', 'México', 'Colombia'} -> Eliminó el duplicado automáticamente.

# Convertir una lista para limpiar duplicados
numeros_sucios = [1, 2, 2, 3, 4, 4, 4]
numeros_limpios = set(numeros_sucios)
print(numeros_limpios) # {1, 2, 3, 4}
```

### Métodos y Operaciones

#### add() y discard()

Para añadir o eliminar elementos individuales. Se recomienda discard() sobre remove() porque no lanza un error si el elemento no existe.

```Python
paises.add("Venezuela")
paises.discard("España")
```

### Operaciones Matemáticas (Álgebra de conjuntos)

Python permite comparar conjuntos de forma muy sencilla usando operadores:

```Python
set_a = {1, 2, 3}
set_b = {3, 4, 5}


# Unión (|): Todos los elementos de ambos conjuntos
print(set_a | set_b) # {1, 2, 3, 4, 5}

# Intersección (&): Solo los elementos que están en ambos
print(set_a & set_b) # {3}

# Diferencia (-): Elementos que están en A pero no en B
print(set_a - set_b) # {1, 2}
```

## La paradoja de las llaves {}

Si declaras una variable con llaves vacías, Python siempre dará prioridad al diccionario.

```Python
# ¿Qué es esto?
mivariable = {}

print(type(mivariable))
# Resultado: <class 'dict'>
```

**¿Cómo crear un conjunto vacío entonces?**

Para crear un conjunto sin elementos, debes usar obligatoriamente el constructor set().

```Python
# Esto SÍ es un conjunto vacío
mi_conjunto = set()

print(type(mi_conjunto))
# Resultado: <class 'set'>
```

**Resumen de sintaxis:**

lista = [] -> Lista vacía.

tupla = () -> Tupla vacía.

diccionario = {} -> Diccionario vacío.

conjunto = set() -> Conjunto vacío (Única excepción).
