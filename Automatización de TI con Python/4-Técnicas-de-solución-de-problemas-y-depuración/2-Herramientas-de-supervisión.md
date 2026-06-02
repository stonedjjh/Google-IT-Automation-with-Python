# Herramientas de supervisión

Dispone de sólidas herramientas para encontrar y diagnosticar los cuellos de botella en el rendimiento de los sistemas informáticos. Esto garantiza una experiencia operativa fluida y refinada. Windows, Linux y macOS ofrecen una amplia gama de metodologías y herramientas para supervisar y ajustar el rendimiento del sistema.

## Procesos de Windows

Windows Process Monitor, también conocido como Sysinternals, es una potente herramienta de supervisión que sirve como gestor avanzado de tareas. Proporciona información en tiempo real sobre diversos aspectos del sistema, como las operaciones del sistema de archivos, los cambios en el registro, los procesos y los subprocesos. La herramienta destaca en el diagnóstico de problemas de acceso a archivos, el análisis de configuraciones del sistema y la comprensión de procesos.

Puede utilizar Process Monitor para localizar errores, detectar cambios no autorizados en el Registro e investigar caídas del sistema, lo que la convierte en una herramienta indispensable para la solución de problemas del sistema. Con propiedades detalladas de los eventos y una amplia gama de opciones de filtrado, puede localizar las causas raíz de forma más eficiente centrándose en procesos específicos.

Cuando se combina con herramientas de registro, generación de informes y supervisión, Process Monitor puede mejorar la eficacia del diagnóstico y la resolución de problemas complejos. También puede ser útil para detectar aplicaciones sospechosas que se ejecutan en segundo plano de forma inadvertida.

Para explorar a fondo las capacidades de Process Monitor, lea más sobre él [aquí](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon)

## Rendimiento de Linux

Para mejorar el rendimiento de su sistema Linux, puede utilizar herramientas especializadas que ofrecen información en tiempo real sobre la CPU, la memoria, la E/S del disco y la actividad de la red para detectar rápidamente los cuellos de botella en el rendimiento. Algunas de estas herramientas son Perf-tools, bcc/BPF y bpftrace.

Para optimizar aún más el sistema, utilice una herramienta de análisis estático para examinar el código y las configuraciones en busca de posibles mejoras. El uso de herramientas de evaluación comparativa también puede ser útil para evaluar el rendimiento de su sistema bajo diferentes cargas de trabajo y revelar áreas que pueden necesitar mejoras.

Personalizar su sistema Linux utilizando utilidades de ajuste es una estrategia poderosa para adaptar la configuración y lograr una configuración más rápida y con mayor capacidad de respuesta. Por ejemplo, el SAR (System Activity Reporter) es especialmente útil para analizar tendencias de rendimiento e identificar problemas recurrentes a lo largo del tiempo.

Puede solucionar problemas de forma eficaz, ajustar el rendimiento y garantizar el funcionamiento fluido y eficiente de su sistema Linux incorporando estas herramientas junto con los datos históricos.

Para obtener información en tiempo real sobre el rendimiento de su sistema Linux, lea más [aquí](https://www.brendangregg.com/linuxperf.html)

## El método USE

El método USE es esencial para optimizar el rendimiento del sistema y solucionar problemas de los servidores. Ayuda a identificar cuellos de botella en los recursos y problemas de rendimiento mediante el análisis de Utilización, Saturación y Errores. Los recursos como CPU, memoria, almacenamiento e interfaces de red pueden medirse en función del tiempo de ocupación, la capacidad de carga de trabajo adicional y los errores.

Para detectar problemas y relaciones, el método USE sugiere crear una lista de recursos y un diagrama de bloques funcionales. Esto ayuda a evitar la sobrecarga de datos y proporciona una visualización clara de los componentes del sistema y sus interacciones.

Este método es adaptable a entornos de computación en la nube para evaluar cómo afectan al rendimiento los controles de los recursos de software. Esta metodología proporciona un enfoque sencillo y eficaz para optimizar el rendimiento del sistema.

Para obtener información más detallada, incluidas listas de comprobación específicas para distintos sistemas operativos y orientaciones, siga leyendo [aquí](https://brendangregg.com/usemethod.html)

## monitor de actividad de macOS

El Monitor de actividad de macOS le permite supervisar y gestionar el rendimiento del sistema fácilmente. Puedes optimizar el rendimiento del Mac con la información que ofrece el Monitor de actividad sobre la actividad de los procesos, el uso de recursos y el consumo de energía. El Monitor de Actividad identifica las aplicaciones o procesos que no responden, supervisa el uso de energía, realiza un seguimiento del impacto energético global y muestra el estado del sistema en tiempo real. Le permite solucionar problemas y optimizar la duración de la batería, garantizando un funcionamiento fluido y con capacidad de respuesta.

Para obtener instrucciones detalladas e información sobre cómo utilizar esta utilidad,[consulta](https://support.apple.com/guide/activity-monitor/welcome/mac) la Guía del usuario del Monitor de actividad de Apple [aquí](https://support.apple.com/guide/activity-monitor/welcome/mac).

## Monitor de rendimiento de Windows

El Monitor de Rendimiento es una herramienta versátil y personalizable que analiza el rendimiento de su sistema. Al identificar y resolver problemas de hardware, aplicaciones mal diseñadas, uso excesivo de recursos o malware, garantiza un funcionamiento eficiente y sin problemas. Disponer de datos en tiempo real sobre la memoria, la red, los discos y los procesadores le permite supervisar los componentes clave y resolver rápidamente los problemas. Puede configurar contadores, establecer recopiladores de datos y analizar informes para optimizar su sistema.

Para obtener más información sobre cómo mantener un rendimiento óptimo del sistema, lea más [aquí](https://www.windowscentral.com/how-use-performance-monitor-windows-10)

## Supervisión de recursos de Windows

Para obtener información en tiempo real sobre el uso de los recursos de su ordenador en Windows, utilice la herramienta Monitor de recursos (resmon.exe). Ayuda a identificar las causas de las ralentizaciones, como problemas de hardware, aplicaciones mal diseñadas y malware. Accede a ella buscando "resmon" o "Resource Monitor" Navega entre las secciones Memoria, Disco y Red para un análisis más profundo. Ten cuidado con los procesos de la CPU para evitar la inestabilidad del sistema.

El Monitor de Recursos le ayuda a entender el uso de recursos de su sistema. Para saber más sobre el Monitor de Recursos, lea más [aquí](https://www.digitalcitizen.life/how-use-resource-monitor-windows-7/)

## Explorador de procesos de Windows

El software Process Explorer v17.05 se utiliza principalmente para la monitorización de archivos y el análisis de procesos en ordenadores Windows. Proporciona información detallada sobre los procesos activos, handles y DLLs. Los procesos y sus cuentas se muestran en la ventana superior, mientras que los manejadores y DLL se muestran en la ventana inferior. Además de solucionar problemas de DLL, también ayuda a detectar fugas y problemas, proporcionando información valiosa sobre el funcionamiento del sistema.

Process Explorer soluciona problemas y gestiona DLL de forma eficaz. Para saber más sobre Process Explorer v17.05, lea más [aquí](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)

## Caché

Aunque la caché no es una herramienta de monitorización, es importante no pasarla por alto, ya que la informática depende en gran medida de las cachés, que mejoran la velocidad de acceso a los datos y el rendimiento general del sistema. Almacenan datos a los que se accede con frecuencia para recuperarlos rápidamente, por lo que son esenciales para CPU, SSD, HDD, navegadores y servidores web. Las cachés son más pequeñas y rápidas que la memoria, y actúan como almacenamiento intermedio para optimizar la eficiencia.

## Autoagrupación en Linux

En Linux, la autoagrupación optimiza el rendimiento del escritorio durante las cargas de trabajo intensivas de CPU agrupando los procesos y garantizando una distribución equitativa de los ciclos de CPU. El autoagrupamiento indica al componente planificador de procesos de Linux que actúe basándose en el "nivel agradable" configurado de un grupo en lugar de en los procesos individuales. Sin embargo, la autoagrupación puede interferir con los procesos tradicionales. Cuando está activado, el valor "nice" afecta principalmente a la prioridad dentro del grupo, reduciendo la efectividad de los comandos "nice" y "renice". Incluso los programas que establecen sus propios niveles "nice" pueden seguir recibiendo una parte "justa" del tiempo de CPU.

## Comprobación del uso de memoria

Las fugas de memoria pueden ser un gran problema a la hora de programar, ya que ralentizan el procesamiento de la aplicación y pueden provocar fallos. Cuando puedes evaluar la programación para encontrar problemas, puedes entonces racionalizar tu código y/o procesos para liberar código limpiamente.

Aunque Python gestiona automáticamente la memoria como parte de su lenguaje, existen otras herramientas que puedes utilizar para buscar fugas de memoria y asegurarte de que la tuya funciona de la forma más eficiente posible.

Si estás buscando una sección de tu código que sospechas que puede estar ralentizando tu aplicación, hay paquetes, como [memory-profiler](https://pypi.python.org/pypi/memory_profiler), que evaluarán una única función o código, línea por línea, para mostrar el uso detallado de memoria. También puedes usarlo para evaluar el uso de memoria de tu aplicación a lo largo del tiempo, ayudando a identificar la memoria que no se está liberando tan regularmente como debería.

Si necesitas ver la aplicación en su conjunto, prueba [guppy](https://zhuyifei1999.github.io/guppy3/), una biblioteca para ver y evaluar el uso de memoria por diferentes tipos de objetos.

Para más información sobre el perfilador de memoria y otras herramientas, lee [este artículo.](https://www.pluralsight.com/blog/tutorials/how-to-profile-memory-usage-in-python)

## Comprobación de problemas de red

Si no eres administrador o ingeniero de redes, todos esos acrónimos y sus configuraciones pueden ser un misterio: IP, SASE, IMAP, MAC, SSH, DHCP... Si eres un programador que se enfrenta a problemas de conexión de red, puede ser abrumador resolverlos.

Por suerte, dispones de algunas herramientas integradas que te ayudarán a identificar el origen del problema.

Lo primero que hay que intentar es hacer ping al servidor para ver si se trata de un problema del servidor o de un problema real de la red. Enviando un simple comando `telnet` al servidor y al puerto que estás tratando de alcanzar puedes saber si el servidor está teniendo un problema de tiempo de espera (o está completamente caído), o si podría haber un problema para acceder a él por alguna otra razón.

Si no obtienes respuesta del servidor, puedes suponer que hay algún problema con él o con la red. Aquí es donde entran en juego tus dotes detectivescas. En primer lugar, tendrás que comprobar si se trata de algo en tu extremo o en el extremo receptor.

Comprueba tu puerta de enlace predeterminada utilizando el comando `ipconfig /all` (en Windows) o `ifconfig -a` (en Linux). Esto te mostrará las direcciones IP y las conexiones DHCP. Si no puedes ver el DHCP, entonces necesitas renovar su arrendamiento (la conexión de red entre tú y la dirección IP) o, en algunos casos, el servidor DHCP está caído, lo cual es un problema mayor para los expertos en redes.

Si puedes ver el DHCP, pero la conexión sigue sin funcionar, puedes probar varios dispositivos para localizar el problema. En Linux, puedes utilizar el comando `#arp -n` para ver una lista de direcciones MAC de los dispositivos de la red. Las direcciones MAC son como identificadores de ordenadores individuales en lugar de una red (la dirección IP). Cuando usas `#arp -n`, entonces, puedes ser capaz de ver si a un dispositivo le falta una dirección MAC, lo que te indicaría que está caído.

Para más ejemplos y detalles, consulta este [artículo](https://www.linuxjournal.com/content/troubleshooting-network-problems).

## rsync

rsync(remote sync) es una utilidad para transferir y sincronizar archivos de forma eficiente entre un ordenador y un disco duro externo y entre ordenadores conectados en red, comparando el tiempo de modificación y el tamaño de los archivos. Una de las características importantes dersync es que funciona con elalgoritmo de transferencia delta, lo que significa que sólo sincronizará o copiará los cambios del origen al destino en lugar de copiar todo el archivo. Esto, en última instancia, reduce la cantidad de datos enviados a través de la red.

A continuación se enumeran algunas de las opciones más utilizadas en el comandorsync:

| Opciones | Usos                                                      |
| :------- | :-------------------------------------------------------- |
| -v       | Salida detallada                                          |
| -q       | Suprimir la salida de mensajes                            |
| -a       | Archivar ficheros y directorios durante la sincronización |
| -r       | Sincronizar ficheros y directorios recursivamente         |
| -b       | Tomar la copia de seguridad durante la sincronización     |
| -z       | Comprimir datos de archivos durante la transferencia      |

Ejemplo:

1. Copiar o sincronizar archivos localmente:
   `rsync -zvh [Source-Files-Dir] [Destination]`

2. Copiar o sincronizar directorio localmente:
   `rsync -zavh [Source-Files-Dir] [Destination]`

3. Copia archivos y directorios recursivamente de forma local:
   `rsync -zrvh [Source-Files-Dir] [Destination]`

Para saber más sobre el comando básicorsync, consulta
[este enlace](https://www.linuxtechi.com/rsync-command-examples-linux/)

```PYTHON
#!/usr/bin/env python3

import os
import multiprocessing
import subprocess

def run_sync(directory):
    # Definimos las rutas de origen y destino
    src = os.path.join("/home/student/data/prod", directory)
    dest = "/home/student/data/prod_backup"

    # Usamos subprocess para llamar a rsync
    # -a: modo archivo, -v: visual, -z: compresión
    subprocess.call(["rsync", "-arq", src, dest])

if __name__ == "__main__":
    # 1. Identificar la ruta de origen
    path = "/home/student/data/prod"

    # 2. Obtener la lista de directorios a sincronizar
    # os.listdir nos da los nombres de las carpetas dentro de /data/prod
    dirs = [d for d in os.listdir(path)]

    # 3. Crear el Pool de procesos
    # multiprocessing.cpu_count() detecta cuántos núcleos tienes
    p = multiprocessing.Pool(multiprocessing.cpu_count())

    # 4. Mapear la función run_sync a la lista de directorios
    p.map(run_sync, dirs)

    # 5. Cerrar el pool
    p.close()
    p.join()
```
