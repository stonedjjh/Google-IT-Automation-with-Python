# Ejemplar: Manejo de archivosEstado: Traducido automáticamente del Inglés

Introducción
En este laboratorio, imagina que eres un especialista en informática de una empresa mediana. El Departamento de Recursos Humanos de tu empresa quería que averiguaras cuántas personas había en cada departamento. Necesitaba escribir un script en Python que leyera un archivo CSV que contuviera una lista de los empleados de la organización, contara cuántas personas hay en cada departamento y, a continuación, generara un informe con esta información. La salida de este script era un archivo de texto plano.

Este ejemplo es un recorrido de la actividad anterior de Qwiklab, incluyendo instrucciones detalladas y soluciones. Puede utilizar este ejemplo si no pudo completar el laboratorio y/o necesita una guía adicional para realizar las tareas del laboratorio. También puede consultar este ejemplo para preparar el cuestionario de este módulo.

Requisitos previos
Hemos creado la lista de empleados para usted. Navegue al directoriodata utilizando el siguiente comando:

1
cd data
Para encontrar los datos, liste los archivos usando el siguiente comando:

1
ls
Ahora puede ver un archivo llamadoempleados.csv, donde encontrará los datos. También puedes ver un directorio llamado scripts. En este directorio escribiremos el script de Python.

Para ver el contenido del archivo, introduzca el siguiente comando:

1
cat employees.csv
Empecemos escribiendo el script. Escribirás este script de Python en el directorio scripts. Ve al directorio scripts utilizando el siguiente comando:

1
cd ~/scripts
Crea un archivo llamadogenerate_report.py usando el siguiente comando:

1
nano generate_report.py
Escribirás tu script de Python en este archivogenerate_report.py. Este script comienza con una línea que contiene la combinación de caracteres #!, que comúnmente se denomina hash bang o shebang, y continúa con la ruta al intérprete. Si el núcleo encuentra que los dos primeros bytes son #! entonces utiliza el resto de la línea como intérprete y pasa el fichero como argumento. Usaremos el siguiente shebang en este script:

1
#!/usr/bin/env python3
Convertir datos de empleados a diccionario
El objetivo del script es leer el Archivo CSV y generar un informe con el número total de personas de cada departamento. Para conseguirlo, dividiremos el script en tres funciones.

Empecemos por la primera función:read_employees(). Esta función recibe un Archivo CSV como parámetro y devuelve una lista de diccionarios de dicho archivo. Para ello, utilizaremos el módulo CSV.

El módulo CSV utiliza clases para leer y escribir datos tabulares en formato CSV. La librería CSV nos permite tanto leer como escribir en archivos CSV.

Ahora, importa el módulo CSV.

1
import csv
Define la funciónleer_empleados. Esta función toma file_location (ruta a empleados.csv) como parámetro.

1
def read_employees(csv_file_location):
Abre el Archivo CSV llamando aopen y luego acsv.DictReader.

DictReader crea un objeto que funciona como un lector normal (un objeto que recorre las líneas del Archivo CSV dado), pero que también asigna la información que lee a un diccionario cuyas claves vienen dadas por el parámetro opcionalfieldnames. Si omitimos el parámetrofieldnames, los valores de la primera fila del Archivo CSV se utilizarán como claves. Por lo tanto, en este caso, la primera línea del Archivo CSV contiene las claves y, por lo tanto, no es necesario pasarfieldnames como parámetro.

También necesitamos pasar un dialecto como parámetro a esta función. No existe un estándar bien definido para los archivos de valores separados por comas, por lo que el analizador debe ser flexible. Flexibilidad aquí significa que hay muchos parámetros para controlar cómo csv analiza o escribe los datos. En lugar de pasar cada uno de estos parámetros al lector y al escritor por separado, los agrupamos convenientemente en un objeto dialect.

Las clases de dialecto se pueden registrar por nombre, de modo que quienes llamen al módulo CSV no necesiten conocer de antemano la configuración de los parámetros. Ahora registraremos un dialectoempDialect.

1
csv.register_dialect('empDialect', skipinitialspace=True, strict=True)
El objetivo principal de este dialecto es eliminar los espacios iniciales al analizar el Archivo CSV.

La función será similar a:

1
employee_file = csv.DictReader(open(csv_file_location), dialect = 'empDialect')
Ahora necesita iterar sobre el Archivo CSV que abrió, es decir, archivo_empleado. Al iterar sobre un Archivo CSV, cada iteración del bucle produce un diccionario FROM de cadenas (clave) a cadenas (valor).

Añada los diccionarios a una lista vacía inicializadaemployee_list a medida que itera sobre el Archivo CSV.

123
employee_list = []
for data in employee_file:
employee_list.append(dict(data))
Ahora devuelve esta lista.

1
return employee_list
Para probar la función, llámala y guárdala en una variable llamadaemployee_list. Pasa la ruta a empleados.csv como parámetro de la función. Imprime la variableemployee_list para comprobar si devuelve una lista de diccionarios.

12
employee_list = read_employees('<file_location>')
print(employee_list)
Sustituya<file_location> por la ruta a empleados.csv (debe parecerse a la ruta/home/student/data/employees.csv).

Guarde el archivo pulsandoCtrl-o,Intro yCtrl-x.

Para que el archivo se ejecute necesita tener permiso de ejecución (x). Actualicemos los permisos de archivo e intentemos ejecutar el archivo. Utilice el siguiente comando para añadir permiso de ejecución al archivo:

1
chmod +x generate_report.py
Ahora prueba la función ejecutando el archivo usando el siguiente comando:

1
./generate_report.py
La lista empleados_list dentro del script debería devolver la lista de diccionarios como se muestra a continuación.

Salida:

1
[{'Full Name': 'Audrey Miller', 'Username': 'audrey', 'Department': 'Development'}, {'Full Name': 'Arden Garcia', 'Username': 'ardeng', 'Department': 'Sales'}, {'Full Name': 'Bailey Thomas', 'Username': 'baileyt', 'Department': 'Human Resources'}, {'Full Name': 'Blake Sousa', 'Username': 'sousa', 'Department': 'IT infrastructure'}, {'Full Name': 'Cameron Nguyen', 'Username': 'nguyen', 'Department': 'Marketing'}, {'Full Name': 'Charlie Grey', 'Username': 'greyc', 'Department': 'Development'}, {'F
Procesar datos de empleados
La segunda funciónprocess_data() debería recibir ahora la lista de diccionarios, es decir, employee_list como parámetro y devolver un diccionario dedepartment:amount.

Abra el archivo generate_report.py para definir la función.

1
nano generate_report.py
1
def process_data(employee_list):
Esta función necesita pasar elemployee_list, recibido de la sección anterior, como parámetro a la función.

Ahora, inicialice una nueva lista llamada lista_departamentos, itere sobre lista_de_empleados, y añada sólo los departamentos en lalista_departamentos.

123
department_list = []
for employee_data in employee_list:
department_list.append(employee_data['Department'])
La lista_departamentos debería tener ahora una lista redundante de todos los nombres de departamentos. Ahora tenemos que eliminar la redundancia y devolver un diccionario. Devolveremos este diccionario en el formatodepartamento:cantidad, donde cantidad es el número de empleados en ese departamento en particular.

1234
department_data = {}
for department_name in set(department_list):
department_data[department_name] = department_list.count(department_name)
return department_data
Esto utiliza el métodoset(), que convierte los elementos iterables en elementos distintos.

Ahora, llame a esta función pasando elemployee_list de la sección anterior. A continuación, guarde el resultado en una variable llamadadictionary. Imprime la variabledictionary.

12
dictionary = process_data(employee_list)
print(dictionary)
Guarde el archivo pulsandoCtrl-o,Enter yCtrl-x.

Ahora prueba la función ejecutando el archivo usando el siguiente comando:

1
./generate_report.py
Esto debería devolver un diccionario en el formatodepartamento: cantidad, como se muestra a continuación.

1
{'Vendor operations': 2, 'Sales': 3, 'Development': 4, 'IT infrastructure': 4, 'User Experience Research': 2, 'Human Resources': 2, 'Marketing': 2}
Generar un informe
A continuación, escribiremos la funciónwrite_report(). Esta función escribe un diccionario dedepartamento: importe en un archivo.

El informe debe tener el formato:

<departamento1>: <importe1>

<departamento2>: <importe2>

Abramos el archivogenerate_report.py para definir la función.

1
nano generate_report.py
1
def write_report(dictionary, report_file):
Esta función requiere quedictionary, de la sección anterior, yreport_file, un archivo de salida para generar el informe, sean pasados como parámetros.

Utilizará la funciónopen() para abrir un archivo y devolver un objeto de archivo correspondiente. Esta función requiere que la Ruta de archivo y el Modo de archivo se pasen como parámetros. El modo de archivo es'r'(lectura) por defecto, por lo que ahora debe pasar explícitamente el modo'w+'(abrir para lectura y escritura, sobrescribiendo un archivo) como parámetro.

Una vez abierto el archivo para escritura, itere a través del diccionario y utilicewrite() en el archivo para almacenar los datos.

1234
with open(report_file, "w+") as f:
for k in sorted(dictionary):
f.write(str(k) + ':' + str(dictionary[k]) + '\n')
f.close()
Ahora llame a la funciónwrite_report()pasando una variabledictionary de la sección anterior y también pasando un report_file. El archivo_informe pasado en esta función debe ser similar a/home/student/data/report.txt.

1
write_report(dictionary, '<report_file>')
Guarde el archivo pulsandoCtrl-o,Enter yCtrl-x.

Ahora vamos a ejecutar el script.

1
./generate_report.py
Este script no genera ninguna salida, pero crea un nuevo archivo llamadoreport.txt dentro del directorio dedatos. Este archivo report.txt debería tener ahora el recuento de personas en cada departamento.

Vaya al directoriodata y liste los archivos. Debería ver un nuevo archivo llamadoreport.txt.

1
cd ~/data
1
ls
Para ver el archivo de informe generado, utilice el siguiente comando:

1
cat report.txt
El archivo de informe debe ser similar a la salida de abajo.

1234567
Development:4
Human Resources:2
IT infrastructure:4
Marketing:2
Sales:3
User Experience Research:2
Vendor operations:2
Código Python:

123456789101112131415161718192021222324252627282930
#!/usr/bin/env python3
import csv

#Convert employee data to dictionary
def read_employees(csv_file_location):
csv.register_dialect('empDialect', skipinitialspace=True, strict=True)
employee_file = csv.DictReader(open(csv_file_location), dialect = 'empDialect')
employee_list = []
for data in employee_file:
employee_list.append(data)

¡Enhorabuena!
Ha escrito con éxito un script Python que realiza dos tareas. En primer lugar, lee un Archivo CSV que contiene una lista de los empleados de la organización. En segundo lugar, genera un informe del número de personas en cada departamento en un archivo de texto sin formato.

Crear informes utilizando Python es una herramienta muy útil en Asistencia de TI. Es probable que realices tareas similares con regularidad a lo largo de tu carrera, así que no dudes en pasar por este laboratorio más de una vez. Recuerda, la práctica hace al maestro.
