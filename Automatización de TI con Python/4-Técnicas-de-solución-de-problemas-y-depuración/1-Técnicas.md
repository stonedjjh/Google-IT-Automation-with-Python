# Conceptos y Metodologías

## Solución de problemas

Decimos que la solución de problemas es el proceso de identificación, análisis y ​resolución de problemas. ​Podemos usar el término solución de problemas para referirnos a resolver cualquier tipo de problema.

En el contexto de la informática, la solución de problemas se refiere a la identificación y resolución de problemas relacionados con el hardware, software o redes. ​La solución de problemas es una habilidad esencial para los profesionales de TI, ya que les permite diagnosticar y resolver problemas técnicos de manera eficiente.

### Pasos para la Resolución de Problemas

1. **Obtener Información**: Esto significa reunir toda la información ​que necesitamos sobre el estado actual de las cosas, ​cuál es el problema, cuándo ocurre ​y cuáles son las consecuencias

2. **Encontrar la causa raíz del problema:** La clave aquí es ​llegar al fondo de lo que está pasando, ​lo que desencadenó el problema, ​y cómo podemos cambiar eso

3. **Realizar la corrección necesaria:** Dependiendo del problema, ​esto podría incluir una solución inmediata ​para que el sistema vuelva a funcionar ​y, a continuación, una corrección a medio o largo plazo ​para evitar el problema en el futuro

## Depuración

Es el proceso de identificación ​, análisis y eliminación de errores en un sistema. ​A veces usamos la solución de problemas y la depuración de manera intercambiable. ​Pero generalmente, decimos solucionar problemas cuando estamos solucionando ​problemas en el sistema que ejecuta la aplicación, y ​depurando cuando estamos arreglando los errores en el código real de la aplicación.

## Búsqueda binaria

a búsqueda binaria es un proceso iterativo que consiste en dividir en dos el grupo de elementos **ordenados** para encontrar uno en específico. Tiene una notación **O(\log n)**, lo que la hace eficiente para búsquedas en grandes listas de elementos.

## Concurrencia

Dependiendo de las necesidades de recursos de tu aplicación, es posible que puedas utilizar la concurrencia para ayudar a acelerar las cosas que están ralentizando el procesamiento. La concurrencia implica añadir un poco de código extra a tu programación para permitirle ejecutar múltiples cosas en una secuencia, pero con marcos temporales superpuestos. Por ejemplo, puedes tener cientos de hilos o peticiones, pero puedes configurarlos para que se ejecuten uno encima del otro, en lugar de esperar a que uno se complete antes de que empiece el siguiente.

En la programación basada en E/S, en la que hay muchas interfaces con redes u otro hardware, el uso de la concurrencia puede ayudar a descargar contenidos basados en red de forma más rápida y eficiente. En la programación ligada a la CPU, donde el programa está ocupado procesando datos, puede utilizar la concurrencia para repartir los procesos pesados de la CPU entre varios procesadores, esencialmente dividiendo la carga pesada entre los trabajadores.

Ten en cuenta, sin embargo, que añadir concurrencia a tu código significa... eso es: más codificación, y eso introduce un mayor riesgo de introducir errores difíciles de encontrar en tu programa.

Aprende todo sobre la concurrencia, las diferentes formas de multitarea, las maneras de habilitar la concurrencia fuera de `asyncio`, y mucho más en este profundo y [útil](https://realpython.com/python-concurrency)
artículo. Y, para una buena visión general con ejemplos claros de lo que es la concurrencia, lee este [artículo](https://freecontent.manning.com/concurrency-vs-parallelism/#:~:text=Concurrency%20is%20about%20multiple%20tasks,resources%20like%20multi%2Dcore%20processor.).

## Hilos asíncronos

A diferencia de la concurrencia, que implica procesar las cosas en un orden apilado, también podemos utilizar el subproceso (ejecutarvarias cosas al mismo tiempo) para aumentar la eficiencia.

Por ejemplo, puedes configurar tus hilos de la siguiente manera:

```PYTHON
import threading

def thread_function(name):
   print("Thread {} is running".format(name))

if __name__ == "__main__":
# Create two threads
    thread1 = threading.Thread(target=thread_function, args=("Thread-1",))
    thread2 = threading.Thread(target=thread_function, args=("Thread-2",))


# Start the threads
thread1.start()
thread2.start()


# Wait for the threads to finish
thread1.join()
thread2.join()


print("All threads finished")

# salida
# Thread Thread-1 is running
# Thread Thread-2 is running
# All threads finished
```

En este caso, vemos que el programa se inicia, se crean dos hilos, y cada hilo se ejecuta e imprime el nombre del hilo. Luego los hilos terminan y el programa termina.

Usando `asyncio`, podemos incluso organizar esos procesos para que se ejecuten en el orden que elijamos.

Con `asyncio`, podemos utilizar el comando `await` dentro de bucles de eventos para controlar el procesamiento y obtener la máxima eficiencia. Este sistema es particularmente útil para aplicaciones I/O-bound, donde puedes estar esperando una respuesta de la red, y quieres usar ese tiempo para procesar otras tareas o hilos.

Puedes leer todo sobre los diversos trucos para usar `asyncio`, incluyendo la programación, el uso de diferentes hilos y bucles, notificaciones, y más en este [artículo](https://hackernoon.com/threaded-asynchronous-magic-and-how-to-wield-it-bba9ed602c32) informativo.
