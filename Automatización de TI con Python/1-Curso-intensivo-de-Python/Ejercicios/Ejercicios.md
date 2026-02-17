# Ejercicios

En este archivo se iran colocando algunos ejercicios vistos en el curso separandolos por Módulos

## Módulo 2

### Ejercicio 1

En este escenario, tenemos un directorio con 5 ficheros. Cada archivo tiene un tamaño diferente: 2048, 4357, 97658, 125 y 8. Rellena los espacios en blanco para calcular el tamaño medio de los ficheros haciendo que Python sume todos los valores por ti, y luego establece la variable ficheros al número de ficheros. Finalmente, muestra un mensaje que dice "The average size is: " seguido del número resultante. Recuerde utilizar la función str() para convertir el número en una cadena.

```Python
total = 2048 + ___ + ___ + ___ + ___
files = ___
average = total / files
print("___" + str(___))
```

**Solución:**

```Python
total = 2048 + 4357 + 97658 + 125 + 8
files = 5
average = total / files
print("The average size is: " + str(average))
"""
Here is your output:
The average size is: 20839.2

Nice job! We’re tackling trickier concepts now and you’re
doing great!
"""
```

### Ejercicios de tipado

#### 1

- Utilizar variables para almacenar valores

- Utilizar operadores aritméticos básicos con variables para crear expresiones

- Utilizar la conversión explícita para cambiar un tipo de dato de flotante a cadena

```Python
# The following lines assign the variable to the left of the =
# assignment operator with the values and arithmetic expressions
# on the right side of the = assignment operator.
hotel_room = 100
tax = hotel_room * 0.08
total = hotel_room + tax
room_guests = 4
share_per_person = total/room_guests


# This line outputs the result of the final calculation stored
# in the variable "share_per_person"
print("Each person needs to pay: " + share_per_person) # change a data type
```

**Solución:**

```Python
print("Each person needs to pay: " + str(share_per_person))
#Each person needs to pay: 27.0
```

#### 2

- Imprimir varias variables de cadena en una sola línea para formar una frase

- Utilizar el conector más (+) o una coma para conectar cadenas en una función print()

- Creación de espacios entre variables en una función de print()

```Python
# The following 5 lines assign strings to a list of variables.
salutation = "Dr."
first_name = "Prisha"
middle_name = "Jai"
last_name = "Agarwal"
suffix = "Ph.D."

print(salutation + " " + first_name + " " + middle_name + " " + last_name + ", " + suffix)
# The comma as a string ", " adds the conventional use of a comma plus a
# space to separate the last name from the suffix.

# Alternatively, you could use commas in place of the + connector:
print(salutation, first_name, middle_name, last_name,",", suffix)
# However, you will find that this produces a space before a comma within a string.
```

#### 3

- Resolver TypeError causado por un problema de desajuste de tipo de datos

- Utilizar una función de conversión explícita

```Python
# The following code causes a type error between a string
# and an integer:

print("5 * 3 = " + (5*3))


# Resolution:
# print("5 * 3 = " + str(5*3))
#
# To avoid a type error between the string and the integer within the
# print() function, you can make an explicit data type conversion by
# using the str() function to convert the integer to a string.
```

#### 4

- Resolver un ZeroDivisionError causado por un intento de dividir por 0

```Python
numerator = 7
denominator = 0   # Possible resolution: Change the denominator value
result = numerator / denominator
print(result)


# One possible assumption for a number divided by zero error might
# include the issue of a null value as a denominator (could happen when
# using a loop to iterate over values in a database). In such cases, the
# desired outcome may be to leave the numerator value intact. The
# numerator value can be preserved by reassigning the denominator with
# the integer value of 1. The result would then equal the numerator.
```

**Solución:**

```Python
numerator = 7
denominator = 0
if denominator:
    result = numerator / denominator
else:
    result = "Error Division by zero not allowed"
print(result)
```

## Módulo 3

### Ejercicio Bucle `while`

El siguiente código provoca un bucle infinito. ¿Puedes averiguar qué falla y cómo solucionarlo?

```python
def print_range(start, end):
    # Loop through the numbers from start to end
    n = start
    while n <= end:
        print(n)

print_range(1, 5)  # Should print 1 2 3 4 5 (each number on its own line)
```

**Solución:**

la variable n nunca cambia de valor por lo cual se queda en un bucle infinito.

```python
def print_range(start, end):
    # Loop through the numbers from start to end
    n = start
    while n <= end:
        print(n)
        n += 1

print_range(1, 5)  # Should print 1 2 3 4 5 (each number on its own line)
```

## Módulo 4

### ejercicio con index

Utilizando el método del índice, averigua la posición de "x" en "supercalifragilisticexpialidocious"

```Python
word = "supercalifragilisticexpialidocious"
print(___)
# Solución
print(word.index("x"))
"""
Here is your output:
21

Right on! The index method is a very useful way of working
with strings, and not having to do the hard work manually.
"""
```

### Ejercicio de formato

Modifique la función student_grade utilizando el método format, de forma que devuelva la frase "X recibió Y% en el examen". Por ejemplo, student_grade("Reed", 80) debería devolver "Reed recibió 80% en el examen".

```Python
def student_grade(name, grade):
    return ""
    #Solución
    return "{name} received {grade}% on the exam".format(name=name, grade=grade)

print(student_grade("Reed", 80))
print(student_grade("Paige", 92))
print(student_grade("Jesse", 85))

"""
Here is your output:
Reed received 80% on the exam
Paige received 92% on the exam
Jesse received 85% on the exam

You got it! Your string formatting skills are coming along
nicely!
"""
```

### Ejercicio de listas

Utilizando el método de cadena "split" de la lección anterior, complete la función get_word para devolver la {n}ésima palabra de una sentencia pasada. Para este ejemplo, ejecute las sentencias print de una en una. Borre las otras 3 sentencias print para hacer esto. Por ejemplo, get_word("Esta es una lección sobre listas", 4) debería devolver "lección", que es la 4ª palabra de esta sentencia. Sugerencia: recuerde que los índices de las listas empiezan en 0, no en 1.

```Python
def get_word(sentence, n):
    # Only proceed if n is positive
    if n > 0:
        #words = ___
        words = sentence.split(' ')
        # Only proceed if n is not more than the number of words
        if n <= len(words):
            # return(___)
            return(words[n-1])
    return("")

print(get_word("This is a lesson about lists", 4)) # Should print: lesson
print(get_word("This is a lesson about lists", -4)) # Nothing
print(get_word("Now we are cooking!", 1)) # Should print: Now
print(get_word("Now we are cooking!", 5)) # Nothing
"""
Here is your output:
lesson

Now


Excellent! You're getting comfortable with string
conversions into lists. Now we are really cooking!
"""
```

### Ejercicio tuplas

Utilicemos tuplas para almacenar información sobre un fichero: su nombre, su tipo y su tamaño en bytes. Rellena los huecos de este código para devolver el tamaño en kilobytes (un kilobyte son 1024 bytes) hasta 2 decimales.

```Python
def file_size(file_info):
    #___, ___, ___= file_info
    name, types, size = file_info
    #return("{:.2f}".format(___ / 1024))
    return("{:.2f}".format(size / 1024))

print(file_size(('Class Assignment', 'docx', 17875))) # Should print 17.46
print(file_size(('Notes', 'txt', 496))) # Should print 0.48
print(file_size(('Program', 'py', 1239))) # Should print 1.21
"""
Here is your output:
17.46
0.48
1.21

Well done! Aren't tuples handy to keep the information
nicely organized for when we need it?
"
```

### Ejercicio enumerate

Prueba tú mismo la función enumerar en este rápido ejercicio. Completa la función skip_elements para devolver uno de cada dos elementos de la lista, esta vez utilizando la función enumerate para comprobar si un elemento está en una posición par o impar.

```Python
def skip_elements(elements):
    # code goes here
    # return ___
    new_list = []
    for index, element in enumerate(elements):
        if index % 2 == 0:
            new_list.append(element)
    return new_list


print(skip_elements(["a", "b", "c", "d", "e", "f", "g"])) # Should be ['a', 'c', 'e', 'g']
print(skip_elements(['Orange', 'Pineapple', 'Strawberry', 'Kiwi', 'Peach'])) # Should be ['Orange', 'Strawberry', 'Peach']
```

### Ejercicio comprensión de lista

```Python
def odd_numbers(n):
    # return [x for x in ___ if ___]
    return [x for x in range(1,n+1) if x % 2 == 1]

print(odd_numbers(5)) # Should print [1, 3, 5]
print(odd_numbers(10)) # Should print [1, 3, 5, 7, 9]
print(odd_numbers(11)) # Should print [1, 3, 5, 7, 9, 11]
print(odd_numbers(1)) # Should print [1]
print(odd_numbers(-1)) # Should print []
"""
Here is your output:
[1, 3, 5]
[1, 3, 5, 7, 9]
[1, 3, 5, 7, 9, 11]
[1]
[]

Excellent! You're using the power of list comprehension to
do a lot of work in just one line!
"""
```

Este ejercicio te guiará a través de cómo escribir una comprensión de lista para crear una lista de números al cuadrado (n\*n o n\*\*2). Necesita devolver una lista de cuadrados de números consecutivos entre "inicio" y "fin" inclusive. Por ejemplo, cuadrados(2, 3) debe devolver una lista que contenga [4, 9].

1. La función recibe las variables "inicio" y "fin" a través de los parámetros de la función.

2. En la línea return, comience introduciendo los corchetes de lista [ ] que contendrán la comprensión de la lista.

3. Entre los corchetes [ ]:
   - Introduzca la expresión aritmética para elevar al cuadrado una variable "n".

   - A la derecha de la expresión cuadrada, escriba un bucle for que itere sobre "n" en un range() desde las variables "start" a "end".

   - Asegúrate de que el valor del rango "end" está incluido en range() añadiéndole 1.

4. Ejecuta tu código para ver si funciona. Si lo necesitas, la solución a este código está incluida en la "Guía de Estudio: Operaciones y Métodos de Listas" bajo "Grupo de Habilidades 2" (comprensión de listas).

```Python
def squares(start, end):
    # return ___ 
    return [n*n for n in range(start,end+1)]


print(squares(2, 3))    # Should print [4, 9]
print(squares(1, 5))    # Should print [1, 4, 9, 16, 25]
print(squares(0, 10))   # Should print [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Ejercicio Diccionario

Completa el código para iterar a través de las claves y valores del diccionario cool_beasts. Recuerda que el método items devuelve una tupla de clave, valor para cada elemento del diccionario

```Python
cool_beasts = {"octopuses":"tentacles", "dolphins":"fins", "rhinos":"horns"}
# for ___ in cool_beasts.items():
#     print("{} have {}".format(___))
for k, v in cool_beasts.items():
    print("{} have {}".format(k,v))

"""
Here is your output:
octopuses have tentacles
dolphins have fins
rhinos have horns

Nice job! Your dictionary skills are getting stronger and
stronger!
"""
```
