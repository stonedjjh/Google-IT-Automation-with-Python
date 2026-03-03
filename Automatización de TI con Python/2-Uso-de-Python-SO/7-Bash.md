# Bash y Linux

## Comandos básicos de Linux

- **`mv`** se utiliza para mover uno o más archivos a un directorio diferente, renombrar un archivo, o ambas cosas a la vez.

> [!NOTE]
> Linux distingue entre mayúsculas y minúsculas, por lo que mv también puede utilizarse para cambiar las mayúsculas de un nombre de archivo.

`mv myfile.txt dir1/` Este comando mueve un archivo al directorio.

`mv file1.txt file2.txt file3.txt dir1/` Este comando mueve múltiples archivos.

- **`cp`** se utiliza para copiar uno o más archivos. Algunos ejemplos son:

`cp file1.txt file2.txt`

`cp file1.txt file2.txt file3.txt dir1/`

- **`chmod`/`chown`/`chgrp`** se utiliza para hacer que un archivo sea legible para todos en el sistema antes de moverlo a un directorio público. Un ejemplo común es:

`chmod +r file.html && mv file.html /var/www/html/index.html`

- **`cut`** es un comando que extrae campos de un archivo de datos. Dos ejemplos son:

`cut -f1 -d”,” addressbook.csv` Este comando extrae el primer campo de un archivo .csv.

`cut -c1-3,5-7,9-12 phones.txt` Este comando extrae sólo los dígitos de una lista de números de teléfono.

-**`sort`** es un comando que ordena el contenido de un archivo. Algunos ejemplos son:

`sort names.txt` Este comando ordena las entradas alfabéticamente.

`sort -r names.txt` Este comando ordena las entradas en orden alfabético inverso, empezando por la letra z.

`sort -n numbers.txt` Este comando trata las entradas como números y luego las ordena numéricamente.

- Algunos ejemplos que incluyen la combinación de varios comandos son:

`ls -l | cut -w -f5,9 | sort -rn | head -10` Este comando muestra los 10 archivos más grandes del directorio actual.

`cut -f1-2 -d”,” addressbook.csv | sort` Este comando extrae los nombres y apellidos de un archivo .csv y los ordena.

- **`id`** es un comando que imprime información sobre el usuario actual. Este comando es útil si recibe un error de permisos denegados y cree que se le debería conceder acceso a un archivo.

```Bash
$ id

uid=3000(tradel) gid=3000(tradel) groups=3000(tradel),0(root),100(users),545(builtin_users),999(docker)
```

- **`free`** es un comando que imprime información sobre la memoria en el sistema actual.

`free -h` Este comando imprime en unidades legibles por humanos en lugar de bytes.

- **`basename`:** se utiliza para eliminar los directorios y sufijos de una ruta de archivo, devolviendo únicamente el nombre final del archivo o la última carpeta de la ruta.

**Funciones principales:**

1. Limpiar la ruta: Si le das una ruta completa como /home/usuario/documentos/archivo.txt, te devolverá solo archivo.txt.

2. Eliminar extensiones: Si le indicas el sufijo (la extensión), puede quitarlo automáticamente. Por ejemplo, al ejecutar basename /ruta/foto.jpg .jpg, el resultado será solo foto.

**Ejemplo de uso:**

- Comando simple:
  `basename /var/log/syslog -> Resultado: syslog`

- Con eliminación de sufijo:
  `basename /home/daniel/script.py .py -> Resultado: script`

## Redirecciones, tuberías y señales

**Gestión de flujos:**

Estos son los redireccionadores que podemos utilizar para tomar el control de los flujos de nuestros programas

- comando `>` archivo: redirige la salida estándar, sobrescribe el archivo

- comando `>>` archivo: redirige la salida estándar, anexa al archivo

- comando `<` archivo: redirige la entrada estándar desde archivo

- comando `2>` archivo: redirige el error estándar a archivo

- comando1 `|` comando2: conecta la salida del comando1 a la entrada del comando2

**Operando con procesos:**

Estos son algunos comandos que es útil conocer en Linux cuando se interactúa con procesos. No todos están explicados en los vídeos, así que siéntase libre de investigarlos por su cuenta.

- **`ps`:** lista los procesos que se están ejecutando en el terminal actual para el usuario actual

- **`ps ax`:** lista todos los procesos que se están ejecutando actualmente para todos los usuarios

- **`ps e`:** muestra el entorno de los procesos listados

- **`kill PID`:** envía la señal SIGTERM al proceso identificado por PID

- **`fg`:** hace que un trabajo que estaba detenido o en segundo plano vuelva al primer plano

- **`bg`:** hace que un trabajo que estaba detenido pase a segundo plano

- **`jobs`:** enumera los trabajos actualmente en ejecución o parados

- **`top`:** muestra los procesos que actualmente utilizan más tiempo de CPU (pulse "q" para salir)

## Condicionales y Ciclos

En bash podemos condicionar la ejecución de instrucciones usando la palabra reservada `if`

```Bash
if [ condición ]; then
    # instrucciones a ejecutar si la condición es verdadera
else
    # instrucciones a ejecutar si la condición es falsa
fi
```

También se dispone de ciclos como el `while`

```Bash
#!bin/bash
while [ condición ]; do
    # instrucciones a ejecutar mientras la condición sea verdadera
done

# otro ejemplo

n=1
while [ $n -le 5]; do
    echo "Numero: $n"
    ((n+1))
done
```

Y el `for`

```Bash
#!bin/bash
for variable in lista; do
    # instrucciones a ejecutar para cada elemento de la lista
done

# otro ejemplo
for i in {1..5}; do
    echo "Numero: $i"
done

for frutas in pera naranja manzana; do
    echo "Fruta: $frutas"
done
```
