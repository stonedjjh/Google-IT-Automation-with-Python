# Expresiones Regulares

Una expresión regular, también conocida como expresión regular o expresión regular, es esencialmente una consulta de búsqueda de texto que se expresa mediante un patrón de cadena

---

## 1. Tabla de Metacaracteres (Marcadores)

| Marcador | Nombre              | Descripción                                                   | Ejemplo                              |
| :------- | :------------------ | :------------------------------------------------------------ | :----------------------------------- |
| `.`      | **Punto**           | Coincide con **cualquier** carácter (excepto salto de línea). | `a.b` -> "axb", "a2b"                |
| `^`      | **Ancla de inicio** | El patrón debe estar al **principio** de la línea.            | `^Hola` -> "**Hola** Juan"           |
| `$`      | **Ancla de fin**    | El patrón debe estar al **final** de la línea.                | `fin$` -> "este es el **fin**"       |
| `*`      | **Asterisco**       | El carácter anterior se repite **0 o más veces**.             | `ho*la` -> "hla", "hola", "hooola"   |
| `+`      | **Más**             | El carácter anterior se repite **1 o más veces**.             | `ho+la` -> "hola", "hooola"          |
| `?`      | **Interrogación**   | El carácter anterior es **opcional** (0 o 1 vez).             | `colou?r` -> "color", "colour"       |
| `[]`     | **Clases**          | Coincide con **cualquier** carácter dentro del grupo.         | `[aeiou]` -> cualquier vocal         |
| `[^]`    | **Clase negada**    | Coincide con cualquier carácter **fuera** del grupo.          | `[^0-9]` -> cualquier no-número      |
| `\`      | **Escape**          | Convierte un metacaracter en un carácter literal.             | `\.` -> busca un punto "."           |
| `\|`     | **O (Pipe)**        | Funciona como un operador lógico **OR**.                      | `si\|no` -> coincide con "si" o "no" |
| `{n,m}`  | **Rango**           | Define repeticiones de un mínimo de _n_ a un máximo de _m_.   | `\d{2,4}` -> "12", "123", "1234"     |

## 2. Clases Predefinidas (Shorthands)

Son atajos para no tener que escribir rangos largos:

- **`\d`**: Cualquier dígito (equivalente a `[0-9]`).
- **`\w`**: Cualquier carácter alfanumérico (letras, números y guion bajo).
- **`\s`**: Cualquier espacio en blanco (espacios, pestañas, saltos de línea).
- **`\b`**: Límites de palabra (identifica dónde empieza o termina una palabra).

## 3. Implementación básica en Python

Es fundamental usar **Raw Strings** (`r"..."`) para evitar conflictos con los escapes de Python.

```python
import re

texto = "El código de acceso es 4455 y el usuario es admin_01"

# Buscar todos los dígitos seguidos
digitos = re.findall(r"\d+", texto)
print(digitos)  # Salida: ['4455', '01']

# Buscar si empieza con 'El'
empieza = re.search(r"^El", texto)
if empieza:
    print("La línea es correcta.")
```

> [!IMPORTANT]
> Diferencia Crítica: > \* search(): Busca la primera coincidencia en cualquier parte del texto.

- **findall()**: Devuelve una lista con todas las coincidencias encontradas.

- **search()**: Solo busca coincidencias desde el inicio estricto del texto.

**Ejemplos:**

```PYTHON
import re
result = re.search(r"aza", "plaza")
print(result)
#Salida
<re.Match object; span=(2, 5), match='aza'>

result = re.search(r"aza", "bazaar")
print(result)
#Salida
<re.Match object; span=(1, 4), match='aza'>


result = re.search(r"aza", "maze")
print(result)
#Salida
None
print(re.search(r"^x", "xenon"))
#Salida
<re.Match object; span=(0, 1), match='x'>

print(re.search(r"p.ng", "penguin"))
#Salida
<_sre.SRE_Match object; span=(0, 4), match='peng'>

print(re.search(r"p.ng", "clapping"))
#Salida
<_sre.SRE_Match object; span=(4, 8), match='ping'>

print(re.search(r"p.ng", "sponge"))
#Salida
<_sre.SRE_Match object; span=(1, 5), match='pong'>

print(re.search(r"p.ng", "Pangaea", re.IGNORECASE))
#Salida
<_sre.SRE_Match object; span=(0, 4), match='Pang'>

```

> [!IMPORTANT]
> La r al principio de `re.search(r` es para especificar que se trata de una cadena sin procesar Esto significa que el intérprete de Python no debería intentar interpretar ningún carácter especial, y en su lugar, simplemente debería pasar la cadena a la función tal como está.

```PYTHON
import re

# Comodines y clases de caracteres

# Se especifica que el patron inicia con P o p
print(re.search(r"[Pp]ython", "Python"))
<_sre.SRE_Match object; span=(0, 6), match='Python'>
# Aqui se le pasa un rango de a hasta z minuscula
print(re.search(r"[a-z]way", "The end of the highway"))
print(re.search(r"[a-z]way", "What a way to go"))
#Aqui se le pasa un rango de a hasta z mayusculas y minusculas o cualquier digito
print(re.search("cloud[a-zA-Z0-9]", "cloudy"))
print(re.search("cloud[a-zA-Z0-9]", "cloud9"))
<_sre.SRE_Match object; span=(18, 22), match='hway'>
None
<_sre.SRE_Match object; span=(0, 6), match='cloudy'>
<_sre.SRE_Match object; span=(0, 6), match='cloud9'>

# El ^ se usa para negar
print(re.search(r"[^a-zA-Z]", "This is a sentence with spaces."))
print(re.search(r"[^a-zA-Z ]", "This is a sentence with spaces."))

# El pipe sirve como un o logico
print(re.search(r"cat|dog", "I like cats."))
print(re.search(r"cat|dog", "I love dogs!"))
print(re.search(r"cat|dog", "I like both dogs and cats."))

print(re.search(r"cat|dog", "I like cats."))
print(re.search(r"cat|dog", "I love dogs!"))
print(re.search(r"cat|dog", "I like both dogs and cats."))
print(re.findall(r"cat|dog", "I like both dogs and cats."))
<_sre.SRE_Match object; span=(4, 5), match=' '>
<_sre.SRE_Match object; span=(30, 31), match='.'>
<_sre.SRE_Match object; span=(7, 10), match='cat'>
<_sre.SRE_Match object; span=(7, 10), match='dog'>
<_sre.SRE_Match object; span=(12, 15), match='dog'>
<_sre.SRE_Match object; span=(7, 10), match='cat'>
<_sre.SRE_Match object; span=(7, 10), match='dog'>
<_sre.SRE_Match object; span=(12, 15), match='dog'>
['dog', 'cat']

# Calificcadores de repetición

# * 0 ó mas veces
# + 1 ó mas veces
# ? 0 ó 1 vez

print(re.search(r"Py.*n", "Pygmalion"))
print(re.search(r"Py.*n", "Python Programming"))
print(re.search(r"Py[a-z]*n", "Python Programming"))
print(re.search(r"Py[a-z]*n", "Pyn"))

<_sre.SRE_Match object; span=(0, 9), match='Pygmalion'>
<_sre.SRE_Match object; span=(0, 17), match='Python Programmin'>
<_sre.SRE_Match object; span=(0, 6), match='Python'>
<_sre.SRE_Match object; span=(0, 3), match='Pyn'>

print(re.search(r"o+l+", "goldfish"))
print(re.search(r"o+l+", "woolly"))
print(re.search(r"o+l+", "boil"))
<_sre.SRE_Match object; span=(1, 3), match='ol'>
<_sre.SRE_Match object; span=(1, 5), match='ooll'>
None

print(re.search(r"p?each", "To each their own"))
print(re.search(r"p?each", "I like peaches"))

<_sre.SRE_Match object; span=(3, 7), match='each'>
<_sre.SRE_Match object; span=(7, 12), match='peach'>


# Escape de caracteres

print(re.search(r".com", "welcome"))
print(re.search(r"\.com", "welcome"))
print(re.search(r"\.com", "mydomain.com"))
<_sre.SRE_Match object; span=(2, 6), match='lcom'>
None
<_sre.SRE_Match object; span=(8, 12), match='.com'>

print(re.search(r"\w*", "This is an example"))
print(re.search(r"\w*", "And_this_is_another"))
<_sre.SRE_Match object; span=(0, 4), match='This'>
<_sre.SRE_Match object; span=(0, 19), match='And_this_is_another'>

print(re.search(r"A.*a", "Argentina"))
print(re.search(r"A.*a", "Azerbaijan"))
print(re.search(r"^A.*a$", "Australia"))
<_sre.SRE_Match object; span=(0, 9), match='Argentina'>
<_sre.SRE_Match object; span=(0, 9), match='Azerbaija'>
<_sre.SRE_Match object; span=(0, 9), match='Australia'>

pattern = r"^[a-zA-Z_][a-zA-Z0-9_]*$"
print(re.search(pattern, "_this_is_a_valid_variable_name"))
print(re.search(pattern, "this isn't a valid variable"))
print(re.search(pattern, "my_variable1"))
print(re.search(pattern, "2my_variable1"))
<_sre.SRE_Match object; span=(0, 30), match='_this_is_a_valid_variable_name'>
None
<_sre.SRE_Match object; span=(0, 12), match='my_variable1'>
None

# Captura de grupos

result = re.search(r"^(\w*), (\w*)$", "Lovelace, Ada")
print(result)
print(result.groups())
print(result[0])
print(result[1])
print(result[2])
"{} {}".format(result[2], result[1])
<_sre.SRE_Match object; span=(0, 13), match='Lovelace, Ada'>
('Lovelace', 'Ada')
Lovelace, Ada
Lovelace
Ada
Ada Lovelace


def rearrange_name(name):
    result = re.search(r"^(\w*), (\w*)$", name)
    if result is None:
        return name
    return "{} {}".format(result[2], result[1])
rearrange_name("Lovelace, Ada")
Ada Lovelace
rearrange_name("Ritchie, Dennis")
Dennis Ritchie

# Más sobre los calificativos de repetición

# {} Permite establecer la cantidad de caracteres a buscar
print(re.search(r"[a-zA-Z]{5}", "a ghost"))
<_sre.SRE_Match object; span=(2, 7), match='ghost'>
print(re.search(r"[a-zA-Z]{5}", "a scary ghost appeared"))
<_sre.SRE_Match object; span=(2, 7), match='scary'>
print(re.findall(r"[a-zA-Z]{5}", "a scary ghost appeared"))
['scary', 'ghost', 'appea']
re.findall(r"\b[a-zA-Z]{5}\b", "A scary ghost appeared")
['scary', 'ghost']
# se puede establecer un minimo y un maximo
print(re.findall(r"\w{5,10}", "I really like strawberries"))
['really', 'strawberri']
print(re.findall(r"\w{5,}", "I really like strawberries"))
['really', 'strawberries']
print(re.search(r"s\w{,20}", "I really like strawberries"))
<_sre.SRE_Match object; span=(14, 26), match='strawberries'>

```

---

**Dividir y sustituir:**

- **`re.split`:** Es una función del módulo re de Python que permite dividir una cadena de texto en una lista de subcadenas, utilizando una expresión regular como delimitador.

A diferencia del método estándar `.split()` de los strings, que solo permite usar separadores fijos (como una coma o un espacio), `re.split()` ofrece la flexibilidad de definir múltiples patrones, conjuntos de caracteres o secuencias complejas para realizar el corte, permitiendo incluso conservar el delimitador dentro de la lista resultante si este se encierra entre paréntesis de captura.

**Sintaxis:**

- `re.split(pattern, string, maxsplit=0, flags=0)`
  - **pattern:** La expresión regular que define dónde se realizarán los cortes.

  - **string:** El texto que quieres dividir.

  - **maxsplit: (opcional)** El número máximo de divisiones. Si es 1, la lista tendrá 2 elementos. El valor por defecto (0) hace todas las divisiones posibles.

  - **flags: (opcional)** Modificadores como re.IGNORECASE.

- **`re.sub`:** Es la función de búsqueda y reemplazo del módulo re en Python. Su nombre proviene de "substitute" (sustituir).

Permite buscar todas las coincidencias de una expresión regular dentro de una cadena y reemplazarlas por un nuevo texto o por el resultado de una función. Es significativamente más potente que el método `.replace()` de los strings básicos, ya que permite realizar sustituciones basadas en patrones dinámicos, referencias a grupos capturados o transformaciones lógicas complejas sobre cada coincidencia encontrada.

**Sintaxis:**

- `re.sub(pattern, repl, string, count=0, flags=0)`

- **pattern:** La expresión regular que define qué quieres "atrapar".

- **repl:** El reemplazo. Aquí es donde ocurre la magia:
  - Puede ser un texto simple.

  - Puede incluir backreferences (\1, \g<name>) para reinsertar grupos capturados.

  - Puede ser una función (callback) que reciba el objeto match y devuelva un string.

- **string:** La cadena de texto original que quieres procesar.

- **count (opcional):** Número máximo de sustituciones. Si es 0, reemplaza todas las que encuentre.

- **flags (opcional):** Modificadores como re.IGNORECASE.

```PYTHON
import re
re.split(r"[.?!]", "One sentence. Another one? And the last one!")
['One sentence', ' Another one', ' And the last one', '']
re.split(r"([.?!])", "One sentence. Another one? And the last one!")
['One sentence', '.', ' Another one', '?', ' And the last one', '!', '']
re.sub(r"[\w.%+-]+@[\w.-]+", "[REDACTED]", "Received an email for go_nuts95@my.example.com")
'Received an email for [REDACTED]'
re.sub(r"^([\w .-]*), ([\w .-]*)$", r"\2 \1", "Lovelace, Ada")
'Ada Lovelace'
```

---

### RegEx Avanzado: Codicia vs. Pereza (Greedy vs. Lazy)

El comportamiento por defecto de los cuantificadores (`*` y `+`) es **Greedy** (codicioso); intentan capturar la mayor cantidad de texto posible.

- **Greedy (`.*`):** Busca desde la primera coincidencia hasta la **última** posible.
  - _Ejemplo:_ `re.search(r"A.*a", "Azerbaijan")` -> `Azerbaija`
- **Lazy (`.*?`):** Busca desde la primera coincidencia hasta la **primera** que cierre el patrón.
  - _Ejemplo:_ `re.search(r"A.*?a", "Azerbaijan")` -> `Azerba`

#### Uso de Anclas para Validación

- `^`: Fuerza a que el patrón coincida desde el **inicio** de la cadena.
- `$`: Fuerza a que el patrón coincida hasta el **final** de la cadena.
- **Uso conjunto (`^...$`):** Se utiliza para validar que una cadena completa (como un ID o un país) cumpla el formato exacto, sin caracteres extra a los lados.

> [!NOTE]
> El símbolo `?` tiene doble función: solo después de un cuantificador (`*?` o `+?`) activa el modo Lazy. Si está solo tras un carácter (`a?`), significa que ese carácter es opcional.

- `r”\d{3}-\d{3}-\d{4}”` esta línea de código coincide con números de teléfono de EE.UU. en el formato 111-222-3333.

- `r”^-?\d*(\.\d+)?$”` esta línea de código coincide con cualquier número positivo o negativo, con o sin decimales.

-`r”^/(.+)/([^/]+)/$”` Esta línea de código se utiliza a menudo para extraer partes específicas de URL o rutas de archivos, como los nombres de directorios o nombres de archivos.

### Adelanto Pro: Grupos de Captura vs. No Captura

En ejercicios complejos de reordenamiento de nombres, es común necesitar paréntesis para agrupar opciones (como iniciales o segundos nombres).

- **Grupo de Captura `( )`**: Python guarda el contenido. Útil para el resultado final (Nombre, Apellido).
- **Grupo de No Captura `(?: )`**: Python usa la lógica para encontrar el patrón, pero **NO** le asigna un número de grupo ni lo guarda por separado.

#### Ejemplo de uso real:

`r"^([\w.-]+), ([\w.-]+(?: [\w.-]+)*)$"`

1. El primer `()` captura el Apellido (`result[1]`).
2. El segundo `()` captura el Nombre completo (`result[2]`).
3. El `(?: )` interno permite que el nombre tenga múltiples espacios y palabras sin crear un `result[3]` innecesario.

> [!TIP]
> Si tu función de reordenar nombres te devuelve números de grupo extraños o "None" en medio de un nombre, probablemente necesites convertir un paréntesis normal en uno de no captura con `?:`.
