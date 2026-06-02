# Serialización

La serialización es el proceso de convertir un objeto en una secuencia de bytes para que pueda ser almacenado o transmitido. En Python, existen varios formatos de serialización, como JSON, XML, YAML, entre otros.

## JSON

[JSON (JavaScript Object Notation)](https://json.org/) es el formato de serialización que más utilizaremos en este curso. Entraremos en detalles más adelante pero, por ahora, vamos a usar el módulo json para convertir nuestra lista de diccionarios en formato JSON.

```python
import json

with open('people.json', 'w') as people_json:
    json.dump(people, people_json, indent=2)
```

Este código utiliza la función `json.dump()` para serializar el objeto `people` en un archivo JSON. El contenido del archivo será algo parecido a esto:

```json
[
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },
  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  }
]
```

## YAML

[YAML (Yet Another Markup Language)](https://yaml.org/) tiene mucho en común con JSON. Ambos son formatos que pueden ser fácilmente entendidos por un humano cuando mira el contenido. En este ejemplo, estamos utilizando el método `yaml.safe_dump()` para serializar nuestro objeto en YAML:

```python
import yaml

with open('people.yaml', 'w') as people_yaml:
    yaml.safe_dump(people, people_yaml)
```

Ese código generará un archivo people.yaml con el siguiente aspecto:

```yaml
- department: IT Infrastructure
  name: Sabrina Green
  phone:
    cell: 802-867-5310
    office: 802-867-5309
  role: Systems Administrator
  username: sgreen
- department: IT Infrastructure
  name: Eli Jones
  phone:
    office: 684-348-1127
  role: IT Specialist
  username: ejones
```

Aunque no es exactamente igual que el ejemplo JSON anterior, ambos formatos enumeran los nombres de los campos como parte del formato, de forma que tanto los programas que analizan los datos como los humanos que los consultan puedan entenderlos. La principal diferencia es cómo se utilizan estos formatos. JSON se utiliza con frecuencia para transmitir datos entre Servicios web, mientras que YAML es el más utilizado para almacenar valores de configuración.

Estos son sólo un par de los formatos de serialización de datos más comunes. Hemos dejado fuera otros bastante comunes como [Python pickle](https://docs.python.org/3/library/pickle.html), [Protocol Buffers](https://developers.google.com/protocol-buffers), o el [eXtensible Markup Language (XML)](https://www.w3.org/XML/). Cada uno de ellos es útil en un contexto específico, aunque no es el foco de este curso. Puedes leer más sobre ellos siguiendo esos enlaces.
