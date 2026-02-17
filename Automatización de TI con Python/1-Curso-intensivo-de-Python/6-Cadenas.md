# Cadenas

Las cadenas de texto en Python se representan con comillas simples (' ') o dobles (" "). Puedes usar cualquiera de las dos, pero es importante ser consistente

Las cadenas de texto son inmutables

```python
greeting = "Hello"
greeting[0] = "h"
# TypeError: 'str' object does not support item assignment
name = "mary'
# SyntaxError: unterminated string literal
print(name)

```

## Cortar y Unir Cadenas

Cuando cortas una cadena, extraes un subconjunto de la cadena original, lo que a veces se denomina indexar una cadena. Unir cadenas es el proceso de unir dos o más cadenas para crear una cadena mayor.

### Cómo cortar cadenas

La Notación entre corchetes, [ ], se utiliza para especificar el inicio del índice, el índice final o ambos. Si no incluye el índice inicial, entonces la rebanada contiene todo desde el principio de la cadena hasta el índice final. Lo mismo ocurre si no se incluye el índice final. Veamos un par de ejemplos:

> [!TIP]
> Recuerda que los índices en Python empiezan por 0, y no por 1.

```Python
string1 = "Greetings, Earthlings"
print(string1[0])   # Prints “G”
print(string1[4:8]) # Prints “ting”
# sino se pasa un segundo argumento se asume hasta la longitud de la cadena
print(string1[11:]) # Prints “Earthlings”
# sino se pasa el primer argumento se asume 0
print(string1[:5])  # Prints “Greet”
print(string1[-10:]) # Prints “Earthlings”
# Si tu índice está más allá del final de la cadena, Python devuelve una cadena vacía.
print(string1[55:]) # Prints “” 
```

### strider

Una forma opcional de trocear un índice es mediante el argumento stride, indicado mediante el uso de dos puntos dobles. Esto te permite saltarte el número correspondiente de caracteres en tu índice, o si estás usando un stride negativo, la cadena se imprime hacia atrás.

```Python
# Prints “Getns atlns”
print(string1[0::2])

# Prints “sgnilhtraE ,sgniteerG”
print(string1[::-1])
```

**Analísis:**

`cadena[inicio:fin:paso]` (donde "paso" es el stride).

Desglose de los ejemplos:

`string1[0::2]:`

Inicio: 0 (empieza en la 'G').

Fin: Vacío (llega hasta el final de la cadena).

Paso (Stride): 2 (va saltando de dos en dos).

Resultado: Selecciona los índices 0, 2, 4, 6... y por eso "desaparece" un caracter de por medio.

`string1[::-1]:`

Inicio y Fin: Vacíos (toma toda la cadena).

Paso (Stride): -1 (camina hacia atrás).

Resultado: Invierte el orden completamente.

## Cómo unir cadenas

Para unir cadenas en Python, se utiliza el operador más, +, como si estuvieras sumando dos números. El siguiente ejemplo une tres cadenas.

```Python
# Prints “Hello world”
print("Hello" + " " + "world")
```

### método `join()`

También puedes usar el método join(), que es muy útil cuando quieres concatenar elementos de una lista de cadenas con un delimitador específico. En el siguiente ejemplo, tenemos una lista de cadenas llamada greetings y las unimos con un espacio utilizando .join(greetings). El método join() concatena todas las cadenas de la lista greetings, y coloca un espacio entre cada cadena.

```Python
words = ["Python", "es", "genial"]
sentence = " ".join(words)
print(sentence) # Python es genial
```

## Cómo combinar el corte y la unión de cadenas

Ahora ya sabes cómo cortar y unir cadenas. Ahora, unamos las dos operaciones tomando un número de teléfono sin formato, 2025551212, y devolvámoslo como un número de EE.UU. formateado correctamente. En este ejemplo, utilizaremos phonenum para referirnos al número de teléfono sin formato. Puede definir una función format_phone() para realizar toda la operación. He aquí un desglose de los pasos.

Esto corta los tres primeros números de la cadena:

```Python
phonenum = '2025551212'

# The first 3 digits are the area code:
area_code = "(" + phonenum[:3] + ")"
print(area_code) # Prints “(202)”
```

## Formateo de cadenas

El formateo de cadenas es el proceso de insertar valores dentro de una cadena. Esto se puede hacer con el método `format()` o con f-strings (cadenas formateadas literales).

### format

El método `format()` se utiliza para insertar valores dentro de una cadena utilizando llaves `{}` como marcadores de posición.

```Python
name = "Manny"
number = len(name) * 3
print("Hello {}, your lucky number is {}".format(name, number))
# Hello Manny, your lucky number is 15

print("Your lucky number is {number}, {name}.".format(name=name, number=len(name)*3))
# Your lucky number is 15, Manny.

price = 7.5
with_tax = price * 1.09
print(price, with_tax)
print("Base price: ${:.2f}. With Tax: ${:.2f}".format(price, with_tax))
# 7.5 8.175
# Base price: $7.50. With Tax: $8.18

def to_celsius(x):
  return (x-32)*5/9

for x in range(0,101,10):
  print("{:>3} F | {:>6.2f} C".format(x, to_celsius(x)))

"""
  0 F | -17.78 C
 10 F | -12.22 C
 20 F |  -6.67 C
 30 F |  -1.11 C
 40 F |   4.44 C
 50 F |  10.00 C
 60 F |  15.56 C
 70 F |  21.11 C
 80 F |  26.67 C
 90 F |  32.22 C
100 F |  37.78 C
"""
```

**Guía de formato dentro de las llaves:**

Para controlar cómo se muestra el texto, puedes añadir expresiones dentro de {} siguiendo esta lógica: {:alineación ancho.precisión tipo}.

- **Alineación**:
  - `>`: Alinea a la derecha (útil para columnas de números).

  - `<`: Alinea a la izquierda (comportamiento por defecto).

  - `^`: Centra el texto.

- **Ancho**: El número que indica cuántos espacios ocupará el valor (ej. {:10}).

- **Precisión**: Se usa con números decimales (ej. .2f para dos decimales).

| Código | Propósito                                 | Ejemplo                  | Resultado   |
| :----- | :---------------------------------------- | :----------------------- | :---------- |
| `:.nf` | Determina **n** decimales fijos           | `"{:.2f}".format(0.5)`   | `0.50`      |
| `:>n`  | Alinea a la derecha en **n** espacios     | `"{:>5}".format("Hi")`   | `   Hi`     |
| `:<n`  | Alinea a la izquierda en **n** espacios   | `"{:<5}".format("Hi")`   | `Hi   `     |
| `:^n`  | Centra el texto en **n** espacios         | `"{:^5}".format("Hi")`   | `Hi `       |
| `:n`   | Define un ancho mínimo de **n** espacios  | `"{:5}".format(10)`      | `   10`     |
| `:,`   | Añade separador de miles (coma)           | `"{:,}".format(1000000)` | `1,000,000` |
| `:.n%` | Formato de porcentaje con **n** decimales | `"{:.1%}".format(0.5)`   | `50.0%`     |

```Python
valor = 1234.567
# Alineado a la derecha (>), 10 espacios de ancho (10), separador de miles (,) y 2 decimales (.2f)
print(f"|{valor:>10,.2f}|")
# Resultado: |  1,234.57|
```

### Literales de cadena formateados (Opcional)

La función de literales de cadena formateados, añadida en Python 3.6, aún no se usa mucho. De nuevo, se incluye aquí en caso de que te encuentres con ella en el futuro, pero no es necesaria para este curso ni para los próximos.

Una cadena con formato literal o f-string es una cadena que comienza con 'f' o 'F' antes de las comillas. Estas cadenas pueden contener marcadores de posición {} utilizando expresiones como las utilizadas para las cadenas de método format().

La diferencia importante entre f-strings y el método format() es que las cadenas f toman el valor de las variables del contexto actual, en lugar de tomar los valores de los parámetros.

Ejemplos:

```Python
nombre = "Miqueas"

print(f'Hola {nombre}')

# Hola Miqueas

item = "Taza morada"

importe = 5

precio = cantidad * 3.25

print(f'Artículo: {artículo} - Importe: {importe} - Precio: {precio:.2f}')

# Artículo: Taza morada - Importe: 5 - Precio: 16.25
```
