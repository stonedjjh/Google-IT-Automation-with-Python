# Python

## Índice de Contenidos

1. [¿Qué es Python?](#python-es)
2. [Operadores](#operadores)
3. [El Zen de Python](#el-zen-de-python)
4. [Comprensión de listas](#comprensión-de-listas)

## Python es

- un lenguaje de scripting de propósito general;

- un lenguaje popular utilizado para codificar una gran variedad de aplicaciones;

- una herramienta de uso frecuente para la automatización

- un lenguaje compatible con varias plataformas;

- un lenguaje fácil de usar para principiantes.

## Python no es

- un lenguaje de scripting específico de la plataforma / del sistema operativo;

- un lenguaje de scripting del lado del cliente;

- un lenguaje de programación puramente orientado a objetos.

## operadores

| Operador | Tipo        | Descripción                                                                      | Ejemplo             | Resultado      |
| -------- | ----------- | -------------------------------------------------------------------------------- | ------------------- | -------------- |
| +        | Aritmético  | Se utiliza para realizar sumas (o concatenar cadenas).                           | 5 + 3               | 8              |
| -        | Aritmético  | Se utiliza para realizar restas.                                                 | 5 - 3               | 2              |
| \*       | Aritmético  | Se utiliza para realizar multiplicaciones.                                       | 5 \* 3              | 15             |
| /        | Aritmético  | Se utiliza para realizar divisiones (resultado de punto flotante).               | 5 / 2               | 2.5            |
| \*\*     | Aritmético  | Se utiliza para realizar potencias o exponenciación.                             | 5 \*\* 2            | 25             |
| %        | Aritmético  | Se utiliza para obtener el módulo (el resto de la división).                     | 5 % 2               | 1              |
| //       | Aritmético  | Se utiliza para realizar la división entera (descarta la parte fraccionaria).    | 5 // 2              | 2              |
| >        | Comparación | Se utiliza para verificar si un valor es mayor que otro.                         | 5 > 3               | True           |
| <        | Comparación | Se utiliza para verificar si un valor es menor que otro.                         | 5 < 3               | False          |
| ==       | Comparación | Se utiliza para verificar si dos valores son iguales (equivalencia).             | 5 == 5              | True           |
| !=       | Comparación | Se utiliza para verificar si dos valores son distintos (no iguales).             | 5 != 3              | True           |
| <=       | Comparación | Se utiliza para verificar si un valor es menor o igual que otro.                 | 3 <= 5              | True           |
| >=       | Comparación | Se utiliza para verificar si un valor es mayor o igual que otro.                 | 5 >= 5              | True           |
| =        | Asignación  | Operador de asignación — asigna un valor a una variable (no es una comparación). | x = 5               | Asigna 5 a `x` |
| and      | Lógico      | Devuelve True si ambos operandos son verdaderos.                                 | (5 > 3) and (2 > 1) | True           |
| or       | Lógico      | Devuelve True si al menos uno de los operandos es verdadero.                     | (5 > 3) or (2 < 1)  | True           |
| not      | Lógico      | Invierte el valor booleano (devuelve False si es True y viceversa).              | not (5 > 3)         | False          |
| in       | Membresía   | Devuelve True si el valor está presente en la secuencia (cadena, lista, etc.).   | 'ho' in 'hola'      | True           |
| not in   | Membresía   | Devuelve True si el valor NO está presente en la secuencia.                      | 'z' not in 'hola'   | True           |
| is       | Identidad   | Devuelve True si ambas variables son el mismo objeto.                            | x is y              | True/False     |
| is not   | Identidad   | Devuelve True si las variables no son el mismo objeto.                           | x is not y          | True/False     |

## El Zen de Python

- Lo bonito es mejor que lo feo.

- Lo explícito es mejor que lo implícito.

- Lo simple es mejor que lo complejo.

- Lo complejo es mejor que lo complicado.

- Plano es mejor que anidado.

- Esparcido es mejor que denso.

- La legibilidad cuenta.

- Los casos especiales no son tan especiales como para romper las reglas.

- Aunque la practicidad gana a la pureza.

- Los errores nunca deben pasar en silencio.

- A menos que se silencien explícitamente.

- Ante la ambigüedad, rechaza la tentación de adivinar.

- Debe haber una -y preferiblemente sólo una- forma obvia de hacerlo.

- Aunque esa manera puede no ser obvia al principio, a menos que seas holandés.

- Ahora es mejor que nunca.

- Aunque a menudo "nunca" es mejor que "ahora mismo".

- Si la aplicación es difícil de explicar, es una mala idea.

- Si la implementación es fácil de explicar, puede ser una buena idea.

- Los espacios de nombres son una gran idea: ¡hagamos más!

## Comprensión de listas

Las comprensiones de listas son una forma concisa de crear listas en Python. Veamos un ejemplo:

```Python
[<expresión> for <elemento> in <iterable>]
```

```Python
numbers = [1, 2, 3, 4, 5]
squared_numbers = [x ** 2 for x in numbers]
print(squared_numbers)
```

Este ejemplo comienza con una lista de números. La segunda línea de código define el tipo de transformación que quieres ejecutar en cada elemento de la lista original. En este caso, estás usando esta línea de código para crear una nueva lista llamada squared_numbers y aplicar x \*\* 2 para elevar al cuadrado cada elemento de la lista numbers. El resultado de cada elemento cuadrado se imprime en una nueva lista:

`[1, 4, 9, 16, 25]`

> [!NOTE]
> Las comprensiones de listas pueden incluir sentencias condicionales y bucles anidados, lo que permite un filtrado adicional de elementos basado en condiciones específicas.

```Python
# Ejemplo: Crear una lista solo con los números pares
numbers = [1, 2, 3, 4, 5, 6]
evens = [x for x in numbers if x % 2 == 0]
print(evens) # [2, 4, 6]
```
