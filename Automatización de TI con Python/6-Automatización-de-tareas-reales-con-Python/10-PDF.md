# Introducción a la generación de PDF

Dependiendo de lo que haga tu automatización, puede que quieras generar un informe en PDF al final, que te permita decidir exactamente cómo quieres que sea tu información.

Hay algunas herramientas en Python que te permiten generar PDFs con el contenido que quieras. Aquí, aprenderemos sobre una de ellas:[ReportLab](https://www.reportlab.com/opensource/). ReportLab tiene un **montón** de características diferentes para la creación de documentos PDF. Cubriremos sólo lo básico aquí, y le daremos indicaciones para obtener más información al final.

Para nuestros ejemplos, utilizaremos principalmente las clases y métodos de alto nivel de la parte **Diseño de página y tipografía mediante scripts (PLATYPUS)** del módulo ReportLab.

Supongamos que tengo una gran colección de fruta y quiero crear un informe en PDF con todos los tipos de fruta que tengo Puedo representar fácilmente los diferentes tipos de fruta y cuánto tengo de cada uno con un diccionario Python. Podría ser algo como esto:

```PYTHON
fruit = {
  "elderberries": 1,
  "figs": 1,
  "apples": 2,
  "durians": 3,
  "bananas": 5,
  "cherries": 8,
  "grapes": 13
}
```

Ahora vamos a convertir esta información en un informe del que podamos presumir Vamos a utilizar la clase **SimpleDocTemplate** para construir nuestro PDF.

```PYTHON
>>> from reportlab.platypus import SimpleDocTemplate
>>> report = SimpleDocTemplate("/tmp/report.pdf")
```

El objeto **informe** que acabamos de crear generará un PDF con el nombre **/tmp/informe.pdf**. Ahora vamos a añadirle algo de contenido Crearemos un título, algo de texto en párrafos y algunos gráficos e imágenes. Para ello, vamos a utilizar lo que reportlab llama **Flowables**. Flowables son algo así como trozos de un documento que reportlab puede organizar para hacer un informe completo. Vamos a importar algunas clases Flowable.

`>>> from reportlab.platypus import Paragraph, Spacer, Table, Image`

Cada uno de estos elementos(**Párrafo**, **Espaciador**, **Tabla** e **Imagen**) son clases que construyen elementos individuales en el documento final. Tenemos que decirle a reportlab qué **estilo** queremos que tenga cada parte del documento, así que vamos a importar algunas cosas más del módulo para describir el estilo.

```PYTHON
>>> from reportlab.lib.styles import getSampleStyleSheet
>>> styles = getSampleStyleSheet()
```

Puedes hacer un estilo propio, pero usaremos el predeterminado proporcionado por el módulo para estos ejemplos. El objeto **styles** contiene ahora un estilo "sample" por defecto. Es como un diccionario de diferentes configuraciones de estilo. Si alguna vez has escrito HTML, las opciones de estilo te resultarán familiares. Por ejemplo **h1** representa el estilo para el primer nivel de encabezados. Bien, ¡por fin estamos listos para darle un título a este informe!

`>>> report_title = Paragraph("A Complete Inventory of My Fruit", styles["h1"])`

Veamos qué aspecto tendrá. Ahora podemos construir el PDF utilizando el método **build()** de nuestro informe. Toma una lista de elementos Flowable, y genera un PDF con ellos.

`>>> report.build([report_title])`

Bien, ahora echemos un vistazo al PDF:

No es mucho, ¡pero es un comienzo!

A continuación, veremos un interesante Flowable para nuestros informes: Tablas.

## Añadir tablas a nuestros PDF

Hasta ahora, hemos generado un archivo PDF muy sencillo, que sólo incluye un título.

Vamos a animarlo añadiendo una **tabla**. Para crear un objeto Tabla, necesitamos que nuestros datos estén en una **lista de listas**, a veces llamada **matriz bidimensional**. Tenemos nuestro inventario de frutas en un diccionario. ¿Cómo podemos convertir un diccionario en una lista de listas?

```PYTHON
>>> table_data = []
>>> for k, v in fruit.items():
...   table_data.append([k, v])
...
>>> print(table_data)
[['elderberries', 1], ['figs', 1], ['apples', 2], ['durians', 3], ['bananas', 5], ['cherries', 8], ['grapes', 13]]
```

Genial, ya tenemos la lista de listas. Ahora podemos añadirla a nuestro informe y volver a generar el archivo PDF llamando al método build.

```PYTHON
>>> report_table = Table(data=table_data)
>>> report.build([report_title, report_table])
```

Y este es el aspecto que tiene ahora el informe generado:

Vale, ¡ha funcionado! Aunque no es muy fácil de leer. Tal vez deberíamos añadir algo de estilo a **report_table**. Para nuestro ejemplo, añadiremos un borde alrededor de todas las celdas de nuestra tabla, y moveremos la tabla a la izquierda. Las definiciones de **TableStyle** pueden ser bastante complicadas, así que siéntete libre de echar un vistazo a la documentación para tener una idea más completa de lo que es posible.

```PYTHON
>>> from reportlab.lib import colors
>>> table_style = [('GRID', (0,0), (-1,-1), 1, colors.black)]
>>> report_table = Table(data=table_data, style=table_style, hAlign="LEFT")
>>> report.build([report_title, report_table])
```

¡Mucho mejor! A continuación, vamos a ver cómo hacer esto más colorido mediante la adición de gráficos a nuestros informes.

## Añadir gráficos a nuestros PDF

Hasta ahora, hemos generado un informe con un título y una tabla de datos. Ahora vamos a añadir algo más gráfico. ¿Qué podría ser mejor que una tarta de frutas (gráfico)? Vamos a necesitar utilizar la clase **Drawing** Flowable para crear un Gráfico **circular**.

```PYTHON
from reportlab.graphics.shapes import Drawing
from reportlab.graphics.charts.piecharts import Pie
report_pie = Pie(width=3*inch, height=3*inch)
```

Para agregar datos a nuestro Gráfico **circular**, necesitamos dos listas separadas: Una para los datos y otra para las etiquetas. Una vez más, vamos a tener que transformar nuestro diccionario de frutas en una forma diferente. Para darle un toque adicional, vamos a ordenar las frutas por orden alfabético:

```PYTHON
report_pie.data = []
report_pie.labels = []
for fruit_name in sorted(fruit):
    report_pie.data.append(fruit[fruit_name])
    report_pie.labels.append(fruit_name)

print(report_pie.data)
# output: [2, 5, 8, 3, 1, 1, 13]
print(report_pie.labels)
# output: ['apples', 'bananas', 'cherries', 'durians', 'elderberries', 'figs', 'grapes']
```

El objeto **Tarta** no es Flowable, pero puede ser colocado dentro de un **Dibujo** Flowable.

```PYTHON
report_chart = Drawing()
report_chart.add(report_pie)
```

Ahora, añadiremos el nuevo Dibujo al informe, y veremos qué aspecto tiene.

`report.build([report_title, report_table, report_chart])`

Muy bien, y con esto, has visto algunos ejemplos de lo que podemos hacer con la librería ReportLab. Hay un montón de cosas más que se pueden hacer y que no cubriremos aquí. Usted querrá referirse a la [ReportLab Guía del Usuario](https://www.reportlab.com/docs/reportlab-userguide.pdf) para más detalles sobre las características que hemos visto, y para ver qué más se puede crear con ella.

Por cierto, ¡la Guía del usuario de ReportLab es un PDF que se genera con reportlab! Genial, ¿verdad?
