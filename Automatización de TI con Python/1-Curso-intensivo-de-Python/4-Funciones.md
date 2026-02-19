# Funciones

Las funciones son bloques de código reutilizables que realizan una tarea específica. En Python, las funciones se definen utilizando la palabra clave `def`, seguida del nombre de la función y paréntesis que pueden incluir parámetros.

```python
def saludar(nombre):
    """Función que saluda a una persona por su nombre."""
    print(f"Hola, {nombre}!")
# Llamada a la función
saludar("Ana")  # Salida: Hola, Ana!
```

```python
#ejemplo tipando las entrada y salida
def saludar(nombre: str)->None:
    """Función que saluda a una persona por su nombre."""
    print(f"Hola, {nombre}!")
# Llamada a la función
saludar("Ana")  # Salida: Hola, Ana!
```

## Parámetros y Argumentos

Los parámetros son variables que se definen en la declaración de la función y que reciben los valores cuando se llama a la función. Los argumentos son los valores reales que se pasan a la función.

```python
def sumar(a, b):
    """Función que suma dos números."""
    return a + b
resultado = sumar(5, 3)  # Llamada a la función con argumentos 5 y 3
print(resultado)  # Salida: 8
```

```python
#ejemplo tipando las entrada y salida
def sumar(a: int, b: int) -> int:
    """Función que suma dos números."""
    return a + b
resultado = sumar(5, 3)  # Llamada a la función con argumentos 5 y 3
print(resultado)  # Salida: 8
```

## Valores de Retorno

Las funciones pueden devolver valores utilizando la palabra clave `return`. Si no se especifica un valor de retorno, la función devuelve `None` por defecto.

```python
def multiplicar(a, b):
    """Función que multiplica dos números."""
    return a * b
resultado = multiplicar(4, 2)
print(resultado)  # Salida: 8
```

```python
#ejemplo tipando las entrada y salida
def multiplicar(a: int, b: int) -> int:
    """Función que multiplica dos números."""
    return a * b
resultado = multiplicar(4, 2)
print(resultado)  # Salida: 8
```

### Lista de Argumentos

- Argumentos posicionales: Son los argumentos que se pasan a una función y se asignan a los parámetros de la función en el orden exacto en que se definieron.
- Argumentos nombrados: Son argumentos que se pasan a una función especificando el nombre del parámetro al que pertenecen.
- Argumentos por defecto: Son argumentos a los que se les asigna un valor predeterminado directamente en la definición de la función.
- Argumentos variables (`*args` y `**kwargs`): Estos permiten que una función acepte un número arbitrario (variable) de argumentos.
  - args: Permite que una función acepte cualquier número de argumentos posicionales adicionales.

> [!IMPORTANT]
> Los argumentos posicionales extra se empaquetan en una tupla.

    ejemplo

    ```python
    def ejemplo_argumentos(arg1, arg2):
        print(f"arg1: {arg1}")
        print(f"arg2: {arg2}")
    ejemplo_argumentos(arg2=10, arg1=5)
    # Salida:
    # arg1: 5
    # arg2: 10
    ```

- kwargs: Permite que una función acepte cualquier número de argumentos nombrados (por palabra clave) adicionales.

> [!IMPORTANT]  
> Los argumentos nombrados extra se empaquetan en un diccionario, donde las claves son los nombres de los argumentos.

```python
def ejemplo_argumentos(arg1, arg2=10, *args, **kwargs):
    print(f"arg1: {arg1}")
    print(f"arg2: {arg2}")
    print(f"args: {args}")
    print(f"kwargs: {kwargs}")
ejemplo_argumentos(5, 20, 1, 2, 3, clave1="valor1", clave2="valor2")
# Salida:
# arg1: 5
# arg2: 20
# args: (1, 2, 3)
# kwargs: {'clave1': 'valor1', 'clave2': 'valor2'}
```

```python
#ejemplo tipando las entrada y salida
def ejemplo_argumentos(arg1: int, arg2: int = 10, *args: int, **kwargs: str) -> None:
    print(f"arg1: {arg1}")
    print(f"arg2: {arg2}")
    print(f"args: {args}")
    print(f"kwargs: {kwargs}")
ejemplo_argumentos(5, 20, 1, 2, 3, clave1="valor1", clave2="valor2")
# Salida:
# arg1: 5
# arg2: 20
# args: (1, 2, 3)
# kwargs: {'clave1': 'valor1', 'clave2': 'valor2'}
```

## Funciones Anónimas (Lambda)

Las funciones lambda son funciones pequeñas y anónimas que se definen utilizando la palabra clave `lambda`. Se utilizan principalmente para operaciones simples y se pueden definir en una sola línea.

```python
# Función lambda que suma dos números
sumar = lambda x, y: x + y
resultado = sumar(3, 5)
print(resultado)  # Salida: 8
```

```python
#ejemplo tipando las entrada y salida
# Función lambda que suma dos números
# Uusando Callable del módulo typing

from typing import Callable

# Definición del tipo: una función que toma dos enteros (int, int)
# y devuelve un entero (int).
sumar: Callable[[int, int], int] = lambda x, y: x + y

resultado = sumar(3, 5)
print(resultado)  # Salida: 8
```
