# Problemas Freceuntes

Aqui se nombraran los problemas más frecuente en el desarrollo de software

## Fuga de memoria (Memory Leak)

Una fuga de memoria ocurre cuando un programa consume memoria pero no la libera adecuadamente, lo que puede llevar a un agotamiento de la memoria disponible y causar que el programa se vuelva lento o incluso se bloquee.

### Herramientas para verificar la Memoría(Memory Profiler)

- **Valgrind**: Es la herramienta específica recomendada para perfilar programas escritos en C y C++

- **Perfiladores para Python**: Para este lenguaje existen diversas herramientas que permiten desde analizar el uso de memoria de una sola función hasta monitorear el consumo total de memoria a lo largo del tiempo

- **Garbage Collector (Recolector de basura)**: En lenguajes como Python, Java o Go, este es un componente interno encargado de liberar automáticamente la memoria que ya no está en uso. Sin embargo, si el código mantiene referencias innecesarias a variables, el recolector no podrá liberar esa memoria, provocando efectos similares a una fuga

## Rendimiento de la red

- La latencia es el retraso entre el envío y la recepción de un byte de datos, el cual se ve afectado por la distancia física y la cantidad de dispositivos intermedios.

- El ancho de banda es la capacidad de datos que pueden enviarse o recibirse por segundo

> [!NOTE]
> La importancia de cada factor depende del tipo de contenido. Para archivos pequeños o navegación web ligera, la latencia inicial tiene un impacto porcentual mayor en el tiempo total de descarga. En cambio, para archivos grandes (como 10 MB o más), la latencia es menos significativa frente al ancho de banda

### Gestión del tráfico y congestión

Dado que todas las conexiones comparten el mismo ancho de banda, una conexión muy pesada puede causar "atascos de tráfico", aumentando drásticamente la latencia de las demás. Para Solucionar esto, se pueden utilizar herramientas como iftop para monitorear procesos o aplicar shaping de tráfico (traffic shaping), que consiste en priorizar ciertos paquetes de datos para que los procesos ligeros sigan funcionando mientras los pesados usan el resto del recurso.

> [!IMPORTANT]
> Límites de conexión: Existe un límite físico en la cantidad de conexiones que una computadora puede establecer. Errores en el software pueden causar que se abran demasiadas o que no se cierren las antiguas, impidiendo que nuevos usuarios se conecten a un servidor
