# Condicionale y Bucle

Una **condicional** permite establecer una condición para la ejecución de un código

Un **bucle** es una estructura de control que permite repetir un bloque de código varias veces. En Python, existen dos tipos principales de bucles: el bucle `for` y el bucle `while`.

En Python, el flujo de control se maneja mediante la indentación (4 espacios) y el uso de los dos puntos (:). No se usan llaves {}.

## Condicionales (if, elif, else)

La estructura de decisión básica. Es fundamental recordar los : al final de cada condición.

```Python
def mayor_de_edad(edad: int) -> bool:
    if edad >= 18:
        return True
    elif edad < 0:
        print("Edad no válida")
        return False
    else:
        return False

# Nota: El 'elif' es el equivalente a 'else if' de otros lenguajes.
```

### Operador Ternario

En lugar del clásico `condicion ? true : false`, Python usa una sintaxis más cercana al lenguaje natural:

```Python
# Sintaxis: resultado_si_cierto if condicion else resultado_si_falso
estado = "Adulto" if edad >= 18 else "Menor"
```

---

## Bucle `while`

Los bucles while ordenan a tu ordenador que ejecute continuamente tu código basándose en el valor de una condición. Esto funciona de forma similar a las sentencias if de ramificación. La diferencia aquí es que el cuerpo del bloque se puede ejecutar varias veces en lugar de sólo un

**Ejemplo:**

```Python
x =   0
while x < 5:
    print("Not there yet, x=" + str(x))
    x = x + 1
print("x=" + str(x))
"""
Not there yet, x=0
Not there yet, x=1
Not there yet, x=2
Not there yet, x=3
Not there yet, x=4
x=5
"""
```

### Anatomía

Un bucle while ejecutará continuamente código dependiendo del valor de una condición. Comienza con la palabra clave while, seguida de una comparación a evaluar y dos puntos. En la línea siguiente se encuentra el bloque de código a ejecutar, con sangría a la derecha. De forma similar a una sentencia if, el código en el cuerpo sólo se ejecutará si la comparación se evalúa como verdadera. Lo que diferencia a un bucle while, sin embargo, es que este bloque de código seguirá ejecutándose mientras la sentencia de evaluación sea verdadera. Una vez que la sentencia deja de ser cierta, el bucle sale y se ejecuta la siguiente línea de código.

```Python
while <comparison>:
    <body>
```

## Bucle `for`

Los bucles for se utilizan para iterar sobre una secuencia (como una lista, una tupla, un diccionario, un conjunto o una cadena). Esto es útil cuando quieres ejecutar un bloque de código un número específico de veces.

**Ejemplo:**

```Python
for x in range(5):
    print(x)
"""
0
1
2
3
4
"""

friends = ['Taylor', 'Alex', 'Pat', 'Eli']
for friend in friends:
    print("Hi " + friend)
"""
Hi Taylor
Hi Alex
Hi Pat
Hi Eli
"""

values = [ 23, 52, 59, 37, 48 ]
sum = 0
length = 0
for value in values:
    sum += value
    length += 1

print("Total sum: " + str(sum) + " - Average: " + str(sum/length))

# Total sum: 219 - Average: 43.8
```

## break

En algunos casos, es posible que quieras salir de un bucle antes de que la condición deje de ser verdadera. Para esto, puedes usar la palabra clave `break`. Esto hará que el programa salga del bucle inmediatamente.

```Python
x = 0
while x < 5:
    print("Not there yet, x=" + str(x))
    if x == 3:
        break
    x = x + 1
"""
Not there yet, x=0
Not there yet, x=1
Not there yet, x=2
"""
```

## continue

Si quieres saltar el resto del código en el cuerpo del bucle para esa iteración y volver a la evaluación de la condición, puedes usar la palabra clave `continue`. Esto hará que el programa ignore el resto del código en el cuerpo del bucle para esa iteración y vuelva a evaluar la condición.

```Python
x = 0
while x < 5:
    x = x + 1
    if x == 3:
        continue
    print("Not there yet, x=" + str(x))
"""
Not there yet, x=1
Not there yet, x=2
Not there yet, x=4
Not there yet, x=5
"""
# Como si x == 3 tenemos un continue no ejecuta el print
```

## Bucles Anidados

Los bucles también pueden estar anidados dentro de otros bucles. Esto es útil cuando quieres iterar sobre múltiples secuencias o realizar operaciones más complejas.

```Python
for left in range(7):
  for right in range(left, 7):
    print("[" + str(left) + "|" + str(right) + "]", end=" ")
  print()
"""
[0|0] [0|1] [0|2] [0|3] [0|4] [0|5] [0|6]
[1|1] [1|2] [1|3] [1|4] [1|5] [1|6]
[2|2] [2|3] [2|4] [2|5] [2|6]
[3|3] [3|4] [3|5] [3|6]
[4|4] [4|5] [4|6]
[5|5] [5|6]
[6|6]
"""

teams = [ 'Dragons', 'Wolves', 'Pandas', 'Unicorns']
for home_team in teams:
  for away_team in teams:
    if home_team != away_team:
      print(home_team + " vs " + away_team)
"""
Dragons vs Wolves
Dragons vs Pandas
Dragons vs Unicorns
Wolves vs Dragons
Wolves vs Pandas
Wolves vs Unicorns
Pandas vs Dragons
Pandas vs Wolves
Pandas vs Unicorns
Unicorns vs Dragons
Unicorns vs Wolves
Unicorns vs Pandas
"""
```

## Bucles con cadenas de caracteres

Los bucles también pueden iterar sobre cadenas de caracteres, lo que es útil para procesar texto.

```Python
greeting = "Hello"
for c in greeting:
     print("The next character is: ", c)
"""
The next character is:  H
The next character is:  e
The next character is:  l
The next character is:  l
The next character is:  o
"""

index = 0
while index < len(greeting):
    print(greeting[index])
    index += 1
"""
H
e
l
l
o
"""

```
