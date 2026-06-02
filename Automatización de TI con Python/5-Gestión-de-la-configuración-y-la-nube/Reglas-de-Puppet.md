# Reglas de Puppet

## Ejercicio

El objetivo de este ejercicio es que vea cómo es Puppet en acción. Durante este laboratorio, se conectará a dos máquinas virtuales diferentes. La VM llamada **puppet** es el Puppet Master que tiene las reglas de Puppet que necesitará editar. La VM llamada **linux-instance** es una VM cliente que usará para comprobar que su catálogo se ha aplicado correctamente.

Los manifiestos utilizados para el entorno de producción se encuentran en `directory /etc/puppet/code/environments/production/manifests`, que contiene un archivo `site.pp` con las definiciones de nodos que se utilizarán para este despliegue. Además, el directorio modules contiene un montón de módulos que ya están en uso. Extenderás el código de este despliegue para añadirle más funcionalidad.

1. Instalar paquetes

Hay un módulo llamado **packages** en la **instancia de Puppet VM** que se encarga de instalar los paquetes necesarios en las máquinas de la flota. Utilice el comando para visitar el módulo:

`cd /etc/puppet/code/environments/production/modules/packages`

Este módulo ya tiene una entrada de recursos que especifica que **python-requests** está instalado en todas las máquinas. Puede ver el archivo `init.pp` usando el comando **cat** en la **instancia Puppet VM**.

`cat manifests/init.pp`

Salida:

```bash
class packages {
    package { 'python-requests':
        ensure => installed,
    }

}
```

Ahora, añada un recurso adicional en el mismo archivo `init.pp` dentro de `path /etc/puppet/code/environments/production/modules/packages`, asegurando que el paquete **golang** se instala en todas las máquinas que pertenecen a la familia `Debian` de sistemas operativos (que incluye Debian, Ubuntu, LinuxMint, y un montón de otros).

Este recurso será muy similar al anterior **python-requests**. Añade permiso de edición al archivo antes de seguir adelante usando:

`sudo chmod 646 manifests/init.pp`

Para instalar el paquete sólo en sistemas Debian, necesitarás usar el hecho de **la familia OS**, así:

```bash
if $facts[os][family] == "Debian" {
# Resource entry to install golang package
}
```

Ahora, abra el archivo usando el editor nano y añada la entrada de recursos especificando que el paquete golang se instale en todas las máquinas de la familia Debian después de la entrada de recursos anterior.

El fragmento tendría ahora este aspecto:

```
if $facts[os][family] == "Debian" {
     package { 'golang':
       ensure => installed,
     }
  }
```

El archivo **init.pp** completo tendría ahora un aspecto similar al siguiente:

```bash
class packages {
   package { 'python-requests':
       ensure => installed,
   }
   if $facts[os][family] == "Debian" {
     package { 'golang':
       ensure => installed,
     }
  }
}
```

Después de esto, también tendremos que asegurarnos de que el paquete **nodejs** está instalado en las máquinas que pertenecen a la familia RedHat. Consulte el siguiente fragmento para ello.

```bash
if $facts[os][family] == "RedHat" {
  #Resource entry
}
```

Complete el fragmento anterior igual que el anterior.

El archivo **init.pp** completo debería tener ahora este aspecto:

```bash

class packages {
   package { 'python-requests':
       ensure => installed,
   }
   if $facts[os][family] == "Debian" {
     package { 'golang':
       ensure => installed,
     }
  }
   if $facts[os][family] == "RedHat" {
     package { 'nodejs':
       ensure => installed,
     }
  }
}
```

Una vez que haya editado el archivo y añadido los recursos necesarios, querrá comprobar que las reglas funcionan correctamente. Podemos hacerlo conectándonos a otra máquina de la red y verificando que están instalados los paquetes correctos.

Nos conectaremos a **la instancia de Linux** usando su dirección IP externa. Para obtener la dirección IP externa de **linux-instance**, utilice el siguiente comando:

`gcloud compute instances describe linux-instance --zone="Zone" --format='get(networkInterfaces[0].accessConfigs[0].natIP)'`

Este comando muestra la dirección IP externa de **linux-instance**. Copia la dirección IP externa de **linux-instance**, abre otro terminal y conéctate a él. Siga las instrucciones dadas en la sección `Accessing the virtual machine` haciendo click en `Accessing the virtual machine` desde el panel de navegación a la derecha.

Ahora ejecute manualmente el cliente Puppet en el terminal de su instancia VM de **linux-instance**:

`sudo puppet agent -v --test`

Este comando deberia ejecutarse con exito y el catalogo deberia ser aplicado.

Salida:

```
2023-10-17 10:38:21.161341 WARN  puppetlabs.facter - locale environment variables were bad; continuing with LANG=C LC_ALL=C
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Retrieving locales
Info: Caching catalog for linux-instance.us-central1-a.c.qwiklabs-gcp-03-73433a2333b1.internal
Info: Applying configuration version '1697539102'
Notice: /Stage[main]/Packages/Package[golang]/ensure: created
Notice: /Stage[main]/Machine_info/File[/tmp/machine_info.txt]/content:
--- /tmp/machine_info.txt	2023-10-17 10:33:25.188341331 +0000
+++ /tmp/puppet-file20231017-2844-1f6npxn	2023-10-17 10:39:01.789374002 +0000
@@ -1,6 +1,6 @@
 Machine Information
 -------------------
 Disks: {"sda"=>{"model"=>"PersistentDisk", "size"=>"10.00 GiB", "size_bytes"=>10737418240, "vendor"=>"Google"}}
-Memory: {"system"=>{"available"=>"3.63 GiB", "available_bytes"=>3901550592, "capacity"=>"5.71%", "total"=>"3.85 GiB", "total_bytes"=>4137762816, "used"=>"225.27 MiB", "used_bytes"=>236212224}}
+Memory: {"system"=>{"available"=>"3.63 GiB", "available_bytes"=>3897368576, "capacity"=>"5.81%", "total"=>"3.85 GiB", "total_bytes"=>4137762816, "used"=>"229.26 MiB", "used_bytes"=>240394240}}
 Processors: {"count"=>2, "isa"=>"unknown", "models"=>["Intel(R) Xeon(R) CPU @ 2.20GHz", "Intel(R) Xeon(R) CPU @ 2.20GHz"], "physicalcount"=>1}
 }

Info: Computing checksum on file /tmp/machine_info.txt
Info: /Stage[main]/Machine_info/File[/tmp/machine_info.txt]: Filebucketed /tmp/machine_info.txt to puppet with sum d30f80b5fe7b675290df24547d8ec410
Notice: /Stage[main]/Machine_info/File[/tmp/machine_info.txt]/content: content changed '{md5}d30f80b5fe7b675290df24547d8ec410' to '{md5}ea6a5de087b843d62eb6a4afe74b61a9'
Notice: Applied catalog in 38.40 seconds

```

Ahora verifique si el paquete **golang** fue instalado en esta instancia. Siendo esta una maquina de la familia Debian deberia tener golang instalado. Utilice el siguiente comando para verificarlo:

`apt policy golang`

Salida:

```bash
golang:
  Installed: 2:1.11~1
  Candidate: 2:1.11~1
  Version table:
     2:1.15~1~bpo10+1 100
        100 http://deb.debian.org/debian buster-backports/main amd64 Packages
 *** 2:1.11~1 500
        500 http://deb.debian.org/debian buster/main amd64 Packages
        100 /var/lib/dpkg/status
```

Con esto, ha visto como puede utilizar los hechos y recursos de paquetes de Puppet para instalar paquetes específicos en máquinas dentro de su flota.

### Obtener información de la máquina

Ahora es el momento de navegar hasta el módulo **machine_info** en nuestro entorno Puppet. En la **terminal de Puppet VM**, navegue hasta el módulo usando el siguiente comando:

`cd /etc/puppet/code/environments/production/modules/machine_info`

El módulo **machine_info** recopila información de la máquina usando los hechos de **Puppet** y luego la almacena en un archivo. Actualmente, el módulo siempre almacena esta información en `/tmp/machine_info`.

Vamos a comprobarlo:

`cat manifests/init.pp`

Salida:

```bash
class machine_info {
  file { '/tmp/machine_info.txt':
    content => template('machine_info/info.erb'),
  }
}
```

Puede ver la ruta en el archivo de arriba. Esta ruta no funciona para máquinas Windows. Por lo tanto, es necesario adaptar esta regla para Windows.

Añada permiso de edición al archivo usando el siguiente comando antes de adaptar la regla.

`sudo chmod 646 manifests/init.pp`

Ahora usaremos `$facts[kernel]` fact para comprobar si el núcleo es "windows". Si es así, establece una variable **$info_path** a `"C:\Windows\Temp\Machine_Info.txt"`, de lo contrario establécela a `"/tmp/machine_info.txt"`. Para ello, abra el archivo con el editor nano y añada la siguiente regla después de la ruta por defecto dentro de la clasemachine_info.

```bash
  if $facts[kernel] == "windows" {
    $info_path = "C:\Windows\Temp\Machine_Info.txt"
  } else {
      $info_path = "/tmp/machine_info.txt"
  }
```

El archivo debería tener ahora un aspecto similar al siguiente

```bash
class machine_info {
  file { '/tmp/machine_info.txt':
    content => template('machine_info/info.erb'),
  }
  if $facts[kernel] == "windows" {
    $info_path = "C:\Windows\Temp\Machine_Info.txt"
  } else {
       $info_path = "/tmp/machine_info.txt"
  }
}
```

Por defecto, los recursos de archivo se almacenan en la ruta definida en el nombre del recurso (la cadena de la primera línea) dentro de la clase. También podemos establecer diferentes rutas, estableciendo el atributo path.

Ahora renombraremos el recurso a "machine_info" y utilizaremos la variable en el atributo path. La variable

variable que estamos utilizando para almacenar la ruta en la regla anterior es **$info_path**.

Elimina la siguiente parte del archivo **manifests/init.pp**.

```bash
  file { '/tmp/machine_info.txt':
    content => template('machine_info/info.erb'),
  }
```

Y añade el siguiente recurso después de la regla dentro de la definición de la clase:

````
  file { 'machine_info':
    path => $info_path,
    content => template('machine_info/info.erb'),
  }

El archivo manifests/init.pp completo debería tener ahora este aspecto:

```bash
class machine_info {
  if $facts[kernel] == "windows" {
       $info_path = "C:\Windows\Temp\Machine_Info.txt"
   } else {
       $info_path = "/tmp/machine_info.txt"
   }
 file { 'machine_info':
       path => $info_path,
       content => template('machine_info/info.erb'),
   }
````

### Plantillas Puppet

Las plantillas son documentos que combinan código, datos y texto literal para producir un resultado final. El objetivo de una plantilla es manejar un texto complicado con entradas simples.

En Puppet, usualmente usará plantillas para manejar el contenido de los archivos de configuración (a través del atributo content del tipo de recurso file).

Las plantillas se escriben en un lenguaje de plantillas, especializado en generar texto a partir de datos. Puppet soporta dos lenguajes de plantillas:

- **Embedded Puppet (EPP)** utiliza expresiones de Puppet en etiquetas especiales. Es fácil de leer para cualquier usuario de Puppet, pero sólo funciona con las versiones más recientes de Puppet. (≥ 4.0, o últimas versiones 3.x con el futuro parser habilitado)

- **Embedded Ruby (ERB)** utiliza código Ruby en las etiquetas. Necesitas saber un poco de Ruby para leerlo, pero funciona con todas las versiones de Puppet.

Ahora, eche un vistazo al archivo de plantilla usando el siguiente comando.

`cat templates/info.erb`

Las plantillas de Puppet generalmente usan datos tomados de las variables de Puppet. Las plantillas son archivos que son pre-procesados, algunos valores son reemplazados por variables. En este caso, el archivo actualmente incluye los valores de tres hechos. Vamos a añadir un nuevo hecho en este archivo ahora.

Agregue permisos de edición al archivo usando `templates/info.erb` usando el siguiente comando:

`sudo chmod 646 templates/info.erb`

Ahora abra el archivo usando el editor nano y agregue el siguiente hecho justo después del último hecho dentro del archivo:

`Network Interfaces: <%= @interfaces %>`

La plantilla debería tener ahora este aspecto:

```bash
Machine Information

------------------

Disks: <%= @disks %>
Memory: <%= @memory %>
Processors: <%= @processors %>
Network Interfaces: <%= @interfaces %>
}
```

Para comprobar si esto funcionó correctamente, vuelva a la terminal VM **de la instancia de Linux** y ejecute manualmente el cliente en esa máquina utilizando el siguiente comando:

`sudo puppet agent -v --test`

Este comando debería ejecutarse correctamente y el catálogo debería aplicarse.

Ahora verifique que el archivo **machine_info** tiene la información requerida usando:

`cat /tmp/machine_info.txt`

Salida:

```bash
Machine Information

------------------

Disks: {"sda"=>{"model"=>"PersistentDisk", "size"=>"10.00 GiB", "size_bytes"=>10737418240, "vendor"=>"Google"}}
Memory: {"system"=>{"available"=>"3.59 GiB", "available_bytes"=>3853631488, "capacity"=>"6.87%", "total"=>"3.85 GiB", "total_bytes"=>4137762816, "used"=>"270.97 MiB", "used_bytes"=>284131328}}
Processors: {"count"=>2, "isa"=>"unknown", "models"=>["Intel(R) Xeon(R) CPU @ 2.20GHz", "Intel(R) Xeon(R) CPU @ 2.20GHz"], "physicalcount"=>1}
Network Inte
Y con esto, ya has visto cómo puedes obtener información de la máquina y almacenarla según el sistema operativo.
```

### Reiniciar la máquina

Para el último ejercicio, vamos a crear un nuevo módulo llamado **reboot**, que comprueba si un nodo ha estado en línea durante más de30 días. Si es así, entonces reinicia el equipo.

Para ello, empezaremos por crear el directorio del módulo.

Vuelva al terminal de **puppet VM** y ejecute el siguiente comando:

`sudo mkdir -p /etc/puppet/code/environments/production/modules/reboot/manifests`

Vaya al directorio `manifests/`.

`cd /etc/puppet/code/environments/production/modules/reboot/manifests`

Cree un archivo **init.pp** para el módulo de reinicio en el directorio `manifests/`.

`sudo touch init.pp`

Abre `init.pp` con el editor nano usando sudo.

`sudo nano init.pp`

En este archivo, empezarás creando una clase llamada `reboot`.

La forma de reiniciar un ordenador depende del OS que esté ejecutando. Por lo tanto, establecerás una variable que tenga uno de los siguientes comandos de reinicio, basado en el hecho del kernel:

- **shutdown /r** en windows

- **shutdown -r now** en Darwin (macOS)

- **reboot** en Linux.

Por lo tanto, añadir el siguiente fragmento en el archivo **init.pp**:

```bash
class reboot {
    if $facts[kernel] == "windows" {
        $cmd = "shutdown /r"
    } elsif $facts[kernel] == "Darwin" {
        $cmd = "shutdown -r now"
    } else {
        $cmd = "reboot"
    }
}
```

Con esta variable definida, ahora definiremos un recurso exec que llame al comando, pero sólo cuando el hecho **uptime_days** sea mayor de 30 días.

Añade el siguiente snippet después del anterior dentro de la definición de la clase en el fichero **reboot/manifests/init.pp**:

```bash
if $facts[uptime_days] > 30 {
    exec { 'reboot':
        command => $cmd,
    }
}
```

El **reboot/manifests/init.pp** completo debería tener ahora este aspecto:

```bash
class reboot {
    if $facts[kernel] == "windows" {
        $cmd = "shutdown /r"
    } elsif $facts[kernel] == "Darwin" {
        $cmd = "shutdown -r now"
    } else {
        $cmd = "reboot"
    }
    if $facts[uptime_days] > 30 {
    exec { 'reboot':
     command => $cmd,
         }
    }
}
```

Por último, para que este módulo se ejecute, asegúrese de incluirlo en el archivo `site.pp`.

Para ello, edita `/etc/puppet/code/environments/production/manifests/site.pp` utilizando el siguiente comando:

`sudo nano /etc/puppet/code/environments/production/manifests/site.pp`

Añade una línea extra que incluya el módulo reboot.

El archivo `/etc/puppet/code/environments/production/manifests/site.pp` debería tener ahora este aspecto:

```bash
node default {
    class { 'packages': }
    class { 'machine_info': }
    class { 'reboot': }
}
```

Ejecuta el cliente en la terminal VM **de la instancia de Linux**:

`sudo puppet agent -v --test`

Salida:

```bash
Info: Using configured environment 'production'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Caching catalog for linux-instance.us-central1-a.c.qwiklabs-gcp-03-73433a2333b1.internal
Info: Applying configuration version '1697540321'
Notice: Applied catalog in 0.10 seconds
```

Y con eso, ¡has añadido un módulo completamente nuevo a tu despliegue!
