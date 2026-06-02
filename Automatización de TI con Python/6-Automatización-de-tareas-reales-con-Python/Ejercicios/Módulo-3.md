# Planteamiento del problema del proyecto

Ha llegado el momento de ejercitar tus músculos de programador y practicar la resolución de un problema de la vida real con los conocimientos adquiridos

En el siguiente laboratorio, tendrás que procesar información relacionada con las ventas que tu empresa generó el mes pasado, y convertirla en un informe PDF con un buen formato que luego enviarás por correo electrónico para que tu jefe pueda consultarlo. La máquina del laboratorio tiene configurado el correo electrónico para que puedas consultar los mensajes resultantes a través de una bonita interfaz de webmail que ya está en funcionamiento.

El sistema con el que trabajarás ya incluye algunos scripts que harán parte del trabajo por ti. Tendrás que unir estas piezas para obtener el resultado que deseas, basando tu código en el que ya está ahí.

ASÍ COMO hemos dicho antes, resolver estos problemas puede llevar algún tiempo, ¡y no pasa nada! Resolver problemas complejos es la mejor manera de dominar realmente tus habilidades de codificación. Antes de empezar el laboratorio, asegúrate de que entiendes lo que tienes que hacer y de que sabes cómo quieres resolverlo. Nadie te va a meter prisa, así que tómate todo el tiempo que necesites, repasa los conceptos que no estén del todo claros y ponte manos a la obra.

Buena suerte, ¡tú puedes!

## Evaluación de Qwiklabs: Genere automáticamente un PDF y envíelo por correo electrónico

**Introducción:**

Trabajas en una empresa que vende coches de segunda mano. La dirección quiere obtener un resumen de las cantidades de vehículos que se han vendido al final de cada mes. La empresa ya dispone de un servicio web que sirve los datos de ventas al final de cada mes, pero la dirección quiere que se envíe un correo electrónico con un PDF adjunto para que los datos sean más fácilmente legibles.

### Lo que hay que hacer

- Escribir un script que resuma y procese los datos de ventas en diferentes categorías

- Generar un PDF utilizando Python

- Enviar automáticamente un PDF por correo electrónico

Por favor, tenga en cuenta que hay una prueba calificada que sigue a este laboratorio. Debe completar el laboratorio antes de realizar el cuestionario. El cuestionario evaluará su comprensión de los conceptos y procedimientos clave tratados en el laboratorio.

Esto es lo que puedes hacer para prepararte:

- Preste mucha atención a las instrucciones y explicaciones que se dan durante la sesión de laboratorio.

- Participa activamente en las actividades del laboratorio y toma notas.

- Repasa tus apuntes antes de realizar la prueba.

**Consejo profesional:**

- Puedes consultar tus apuntes de laboratorio durante el examen.

Tendrás 90 minutos para completar este laboratorio.

## Repuesta Planteada

35.232.95.62

```PYTHON
#!/usr/bin/env python3

import json
import locale
import sys
import os
import reports
import emails

def load_data(filename):
  """Loads the contents of filename as a JSON objects."""
  with open(filename) as json_file:
    data = json.load(json_file)
  return data

def format_car(car):
  """Given a car dictionary, returns a nicely formatted name."""
  return "{} {} ({})".format(
      car["car_make"], car["car_model"], car["car_year"])

def process_data(data):
  """Analyzes the data, looking for maximums.

  Returns a list of lines that summarize the information.
  """
  max_revenue = {"revenue": 0}
  max_sales = {"total_sales": 0}
  years_dict = {}

  for item in data:
    # Calcular el ingreso (revenue = price * total_sales)
    # Es necesario limpiar el símbolo '$' y convertir a float
    item_price = float(item["price"].strip("$"))
    item_revenue = item["total_sales"] * item_price
    if item_revenue > max_revenue["revenue"]:
      item["revenue"] = item_revenue
      max_revenue = item

    # TODO: calcular el modelo de coche con más ventas
    if item["total_sales"] > max_sales["total_sales"]:
      max_sales = item

    # TODO: calcular el año más popular (frecuencia de ventas por año)
    year = item["car"]["car_year"]
    years_dict[year] = years_dict.get(year, 0) + item["total_sales"]

  # Encontrar el año con más ventas acumuladas
  popular_year = max(years_dict, key=years_dict.get)
  popular_year_sales = years_dict[popular_year]

  summary = [
    "The {} generated the most revenue: ${}".format(
        format_car(max_revenue["car"]), max_revenue["revenue"]),
    "The {} had the most sales: {}".format(
        format_car(max_sales["car"]), max_sales["total_sales"]),
    "The most popular year was {} with {} sales.".format(
        popular_year, popular_year_sales),
  ]

  return summary

def cars_dict_to_table(car_data):
  """Turns the data in car_data into a list of lists."""
  table_data = [["ID", "Car", "Price", "Total Sales"]]
  for item in car_data:
    table_data.append([item["id"], format_car(item["car"]), item["price"], item["total_sales"]])
  return table_data

def main(argv):
  """Process the JSON data and generate a full report out of it."""
  data = load_data("car_sales.json")
  summary = process_data(data)

  # TODO: generar el reporte PDF en /tmp/cars.pdf
  # Nota: usamos <br/> para saltos de línea en el PDF
  table_data = cars_dict_to_table(data)
  reports.generate("/tmp/cars.pdf", "Sales summary for last month", "<br/>".join(summary), table_data)

  # TODO: enviar el correo electrónico con el PDF adjunto
  sender = "automation@example.com"
  receiver = "student@example.com"
  subject = "Sales summary for last month"
  # Nota: usamos \n para saltos de línea en el cuerpo del correo
  body = "\n".join(summary)

  message = emails.generate(sender, receiver, subject, body, "/tmp/cars.pdf")
  emails.send(message)

if __name__ == "__main__":
  main(sys.argv)

```

---

## Solución dada en el curso

```PYTHON
#!/usr/bin/env python3

import collections
import json
import locale
import mimetypes
import os.path
import reports
import sys
import emails


def load_data(filename):
  """Loads the contents of filename as a JSON file."""
  with open(filename) as json_file:
    data = json.load(json_file)
  return data


def format_car(car):
  """Given a car dictionary, returns a nicely formatted name."""
  return "{} {} ({})".format(
      car["car_make"], car["car_model"], car["car_year"])


def process_data(data):
  """Analyzes the data, looking for maximums.

  Returns a list of lines that summarize the information.
  """
  max_sales = {"total_sales": 0}
  max_revenue = {"revenue": 0}
  car_year_sales = collections.defaultdict(int)
  for item in data:
    # We need to convert "$1234.56" into 1234.56
    item_price = locale.atof(item["price"].strip("$"))
    item_revenue = item["total_sales"] * item_price
    if item_revenue > max_revenue["revenue"]:
      item["revenue"] = item_revenue
      max_revenue = item

    if item["total_sales"] > max_sales["total_sales"]:
      max_sales = item
    car_year_sales[item["car"]["car_year"]] += item["total_sales"]

  max_car_sales_year = (0,0)
  for year, sales in car_year_sales.items():
    if sales > max_car_sales_year[1]:
      max_car_sales_year = (year,sales)

  summary = []
  summary.append("The {} generated the most revenue: ${}".format(
      format_car(max_revenue["car"]), max_revenue["revenue"]))
  summary.append("The {} had the most sales: {}".format(
      format_car(max_sales["car"]), max_sales["total_sales"]))
  summary.append("The most popular year was {} with {} sales.".format(
      max_car_sales_year[0], max_car_sales_year[1]))

  return summary


def cars_dict_to_table(car_data):
  """Turns the data in car_data into a list of lists."""
  table_data = [["ID", "Car", "Price", "Total Sales"]]
  # sorted_car_data = sorted(a, key=lambda k: k['total_sales'])
  for item in car_data:
    table_data.append([item["id"], format_car(item["car"]), item["price"], item["total_sales"]])
  return table_data


def main(argv):
  data = load_data("car_sales.json")
  summary = process_data(data)

  # Generate a paragraph that contains the necessary summary
  paragraph = "<br/>".join(summary)
  # Generate a table that contains the list of cars
  table_data = cars_dict_to_table(data)
  # Generate the PDF report
  title = "Sales summary for last month"
  attachment = "/tmp/cars.pdf"
  reports.generate(attachment, title, paragraph, table_data)

  # Send the email
  sender = "<sender>@example.com"
  receiver = "<user>@example.com"
  body = "\n".join(summary)
  message = emails.generate(sender, receiver, title, body, attachment)
  emails.send(message)


if __name__ == "__main__":
  main(sys.argv)
```
