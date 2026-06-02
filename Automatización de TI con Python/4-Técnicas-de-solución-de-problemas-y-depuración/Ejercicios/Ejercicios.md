# Ejercicios

## Módulo 1

**Se supone que la función compare_strings compara sólo el contenido alfanumérico de dos cadenas, ignorando mayúsculas frente a minúsculas y la puntuación. Pero hay algo que no funciona. Rellene el código para tratar de encontrar los problemas y, a continuación, arréglelos. Su objetivo es buscar el carácter "-", pero - suele reservarse para los rangos. Encuentre una solución que le permita comparar las dos cadenas.**

```PYTHON
import re
def compare_strings(string1, string2):
#Convert both strings to lowercase
#and remove leading and trailing blanks
string1 = string1.lower().strip()
string2 = string2.lower().strip()

#Ignore punctuation
# punctuation = r"[.?!,;:-']" # re.error: bad character range :-' at position 6
punctuation = r"[.?!,;:\-']" # re.error: bad character range :-' at position 6

string1 = re.sub(punctuation, r"", string1)
string2 = re.sub(punctuation, r"", string2)

#DEBUG CODE GOES HERE
#print(string1 == string2)

return string1 == string2

print(compare_strings("Have a Great Day!", "Have a great day?")) # True
print(compare_strings("It's raining again.", "its raining, again")) # True
print(compare_strings("Learn to count: 1, 2, 3.", "Learn to count: one, two, three.")) # False
print(compare_strings("They found some body.", "They found somebody.")) # False
```

---

**El módulo datetime proporciona clases para manipular fechas y horas, y contiene muchos tipos, objetos y métodos. Ya ha visto utilizar algunos de ellos en la función dow, que devuelve el día de la semana para una fecha concreta. Los utilizaremos de nuevo en la función next_date, que toma el parámetro date_string en el formato "año-mes-día", y utiliza la función add_year para calcular el próximo año en que se producirá esta fecha (es 4 años más tarde para el 29 de febrero durante el año bisiesto, y 1 año más tarde para todas las demás fechas). Después devuelve el valor en el mismo formato en el que recibe la fecha: "año-mes-día". ¿Puede encontrar el error en el código? ¿Está en la función next_date o en la función add_year? ¿Cómo puede determinar si la función add_year devuelve lo que se supone que debe devolver? Añada las líneas de depuración que sean necesarias para encontrar los problemas y, a continuación, corrija el código para que funcione como se indica más arriba.**

```PYTHON
import datetime
from datetime import date

def add_year(date_obj):
try:
new_date_obj = date_obj.replace(year = date_obj.year + 1)
 except ValueError: # This gets executed when the above method fails, # which means that we're making a Leap Year calculation
new_date_obj = date_obj.replace(year = date_obj.year + 4)
 return new_date_obj

def next_date(date_string):

# Convert the argument from string to date object

date_obj = datetime.datetime.strptime(date_string, r"%Y-%m-%d")
 next_date_obj = add_year(date_obj)

# Convert the datetime object to string,

# in the format of "yyyy-mm-dd"
# next_date_string = next_date_obj.strftime("yyyy-mm-dd")
next_date_string = next_date_obj.strftime("%Y-%m-%d")

return next_date_string

today = date.today() # Get today's date
print(next_date(str(today)))

# Should return a year from today, unless today is Leap Day

print(next_date("2021-01-01")) # Should return 2022-01-01
print(next_date("2020-02-29")) # Should return 2024-02-29
```

---

**La función find_item utiliza la búsqueda binaria para localizar recursivamente un elemento en una lista, devolviendo True si se encuentra, False en caso contrario. Algo falta en esta función. ¿Puede detectar qué es y solucionarlo? Añada líneas de depuración donde proceda para ayudarle a localizar el problema.**

```PYTHON
def find_item(list, item):
 #Returns True if the item is in the list, False if not.
  if len(list) == 0:
   return False


 #Is the item in the center of the list?
  middle = len(list)//2
  if list[middle] == item:
   return True


 #Is the item in the first half of the list?
  if item < list[middle]:
   #Call the function with the first half of the list
   return find_item(list[:middle], item)
  else:
   #Call the function with the second half of the list
   return find_item(list[middle+1:], item)


  return False


#Do not edit below this line - This code helps check your work!
list_of_names = ["Parker", "Drew", "Cameron", "Logan", "Alex", "Chris", "Terry", "Jamie", "Jordan", "Taylor"]


print(find_item(list_of_names, "Alex")) # True
print(find_item(list_of_names, "Andrew")) # False
print(find_item(list_of_names, "Drew")) # True
print(find_item(list_of_names, "Jared")) # False
```

---

**The binary_search function returns the position of key in the list if found, or -1 if not found. You want to make sure that it's working correctly, so you need to place debugging lines to let you know each time that the list is cut in half, whether you're on the left or the right. You do not want to print anything when the key is located.**

**For example, the command binary_search([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 3) performs these steps:**

**It determines that the key, 3, is in the left half of the list and prints "Checking the left side".**

**It then determines that 3 is in the right half of the new list and prints "Checking the right side".**

**Finally, it returns the value of 2, which is the position of the key in the list.**

**Add commands to the code to print out "Checking the left side" or "Checking the right side" in the appropriate places.**

```PYTHON
def binary_search(list, key):
    list.sort() # Binary search starts with a sorted list
    left = 0 # The first value of the list
    right = len(list) - 1 # The last value of the list
    while left <= right:
    middle = (left + right) //
    if list[middle] == key:
        # print("Middle element")
        return middle
    elif list[middle] > key:
        # Add debug statement here
        print("Checking the left side")
        right = middle - 1
    else:
        # Add debug statement here
        print("Checking the right side")
        left = middle + 1
    return -1

print(binary_search([10, 2, 9, 6, 7, 1, 5, 3, 4, 8], 1))
print(binary_search([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 5))
print(binary_search([10, 9, 8, 7, 6, 5, 4, 3, 2, 1], 7))
print(binary_search([1, 3, 5, 7, 9, 10, 2, 4, 6, 8], 10))
print(binary_search([5, 1, 8, 2, 4, 10, 7, 6, 3, 9], 11))

```

**La función` best_search` compara las funciones `linear_search` y `binary_search` para localizar una clave en la lista, devuelve cuántos pasos ha necesitado cada método y cuál es el mejor para esa situación. No es necesario ordenar la lista, ya que la función `binary_search` la ordena antes de proceder (y utiliza un paso para hacerlo). Aquí, las funciones `linear_search` y `binary_search` devuelven ambas el número de pasos que se tardó en localizar la clave o en determinar que no está en la lista. Si el número de pasos es el mismo para ambos métodos (incluido el paso extra para ordenar en `binary_search`), entonces el resultado es un empate. Rellene los espacios en blanco para que esto funcione.**

```PYTHON
def linear_search(list, key):
   #Returns the number of steps to determine if key is in the list

   #Initialize the counter of steps
    steps=0
    for i, item in enumerate(list):
        steps += 1
        if item == key:
            break
    #return ___
    return steps

def binary_search(list, key):
    #Returns the number of steps to determine if key is in the list

    #List must be sorted:
    list.sort()

    #The Sort was 1 step, so initialize the counter of steps to 1
    steps=1
    left = 0
    right = len(list) - 1
    while left <= right:
        steps += 1
        middle = (left + right) // 2

        if list[middle] == key:
            break
        if list[middle] > key:
            right = middle - 1
        if list[middle] < key:
            left = middle + 1
    #return ___
    return steps


def best_search(list, key):
    #steps_linear = ___
    #steps_binary = ___
    steps_linear = linear_search(list, key)
    steps_binary = binary_search(list, key)
    results = "Linear: " + str(steps_linear) + " steps, "
    results += "Binary: " + str(steps_binary) + " steps. "
    #if (___):
    if (steps_linear < steps_binary):
        results += "Best Search is Linear."
    #elif (___):
    elif (steps_binary < steps_linear):
        results += "Best Search is Binary."
    else:
        results += "Result is a Tie."

    return results


print(best_search([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 1))
#Should be: Linear: 1 steps, Binary: 4 steps. Best Search is Linear.


print(best_search([10, 2, 9, 1, 7, 5, 3, 4, 6, 8], 1))
#Should be: Linear: 4 steps, Binary: 4 steps. Result is a Tie.

print(best_search([1, 3, 5, 7, 9, 10, 2, 4, 6, 8], 10))
#Should be: Linear: 6 steps, Binary: 5 steps. Best Search is Binary.


print(best_search([5, 1, 8, 2, 4, 10, 7, 6, 3, 9], 11))
#Should be: Linear: 10 steps, Binary: 5 steps. Best Search is Binary.
```

---

### Búsqueda lineal y binaria (Opcional)

```PYTHON
def linear_search(list, key):
  """If key is in the list returns its position in the list,
     otherwise returns -1."""
  for i, item in enumerate(list):
    if item == key:
        return i
  return -1

def binary_search(list, key):
  """Returns the position of key in the list if found, -1 otherwise.
     List must be sorted.
  """
  left = 0
  right = len(list) - 1
  while left <= right:
    middle = (left + right) // 2
    if list[middle] == key:
      return middle
    if list[middle] > key:
      right = middle - 1
    if list[middle] < key:
      left = middle + 1
  return -1
```

---
