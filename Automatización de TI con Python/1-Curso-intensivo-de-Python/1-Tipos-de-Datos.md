# Tipos de datos en Python

|                 Categoría | Nombre del Tipo         | Descripción                                                                 | Ejemplo                         |
| ------------------------: | ----------------------- | --------------------------------------------------------------------------- | ------------------------------- |
|   [Numéricos](#numéricos) | `int` (Entero)          | Números enteros positivos o negativos, sin decimales.                       | `10`, `-5`, `100000`            |
|   [Numéricos](#numéricos) | `float` (Flotante)      | Números con parte fraccionaria o decimal.                                   | `3.14`, `-0.5`, `1.0`           |
|   [Numéricos](#numéricos) | `complex` (Complejo)    | Números complejos (parte real + parte imaginaria).                          | `1+2j`, `-3.5j`                 |
|           [Texto](#texto) | `str` (Cadena)          | Secuencias inmutables de caracteres (texto), encerradas en comillas.        | `"Hola"`, `'Python 3'`, `"123"` |
|    [Booleano](#booleanos) | `bool`                  | Representa valores lógicos: Verdadero o Falso.                              | `True`, `False`                 |
| [Secuencias](#secuencias) | `list` (Lista)          | Colección ordenada y mutable de elementos. Se define con corchetes `[]`.    | `[1, 'a', 3.14]`                |
| [Secuencias](#secuencias) | `tuple` (Tupla)         | Colección ordenada e inmutable de elementos. Se define con paréntesis `()`. | `(10, 'b', False)`              |
| [Secuencias](#secuencias) | `range` (Rango)         | Secuencia inmutable de números, usada a menudo en bucles.                   | `range(5)` (0,1,2,3,4)          |
|         [Mapeos](#mapeos) | `dict` (Diccionario)    | Colección mutable de pares clave:valor.                                     | `{'nombre': 'Ana', 'edad': 30}` |
|   [Conjuntos](#conjuntos) | `set` (Conjunto)        | Colección mutable y desordenada de elementos únicos.                        | `{'a', 'b', 'c'}`               |
|   [Conjuntos](#conjuntos) | `frozenset` (Inmutable) | Versión inmutable de `set`.                                                 | `frozenset([1, 2, 3])`          |
|       [Ninguno](#ninguno) | `NoneType`              | Representa la ausencia de valor (similar a `null` en otros lenguajes).      | `None`                          |

## Ejemplos

### Numéricos

```python
# Entero
entero: int = 42
# Flotante
flotante: float = 3.14
# Complejo
complejo: complex = 1 + 2j
```

### Texto

```python
# Cadena de texto
cadena: str = "Hola, Mundo!"
```

### Booleanos

```python
booleano: bool = True
```

### Secuencias

```python
# Lista
lista: list = [1, 'a', 3.14]
# Tupla
tupla: tuple = (10, 'b', False)
# Rango
rango: range = range(5)  # 0, 1, 2, 3, 4
```

### Mapeos

```python
# Diccionario
diccionario: dict = {'nombre': 'Ana', 'edad': 30}
```

### Conjuntos

```python
# Conjunto
conjunto: set = {'a', 'b', 'c'}
# Conjunto inmutable
conjunto_inmutable: frozenset = frozenset([1, 2, 3])
```

### Ninguno

```python
# Ninguno
ninguno: NoneType = None
```
