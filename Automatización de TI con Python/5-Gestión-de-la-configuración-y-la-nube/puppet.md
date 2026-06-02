# Puppet

Puppet es una herramienta de gestión de configuración y automatización de infraestructura de código abierto. Permite a los administradores de sistemas y equipos DevOps gestionar, configurar y desplegar servidores a gran escala utilizando un enfoque declarativo y el concepto de "infraestructura como código" (IaC) para garantizar la consistencia en entornos físicos, virtuales y en la nube.

**Recursos:**

- [Documentación](https://help.puppet.com/core//current/Content/PuppetCore/puppet_index.htm)

- [Blog](https://puppet.com/blog/deploy-packages-across-your-windows-estate-with-bolt-and-chocolatey/)

- [Puppet Best Practices](https://www.oreilly.com/library/view/puppet-best-practices/9781491922996/ch01.html)

## Características clave de Puppet

- **Enfoque Declarativo**: En lugar de escribir una lista de comandos para ejecutar, se describe el estado deseado del sistema (por ejemplo, "el paquete Nginx debe estar instalado y ejecutándose") en archivos llamados manifiestos.

- **Modelo Agente-Servidor:** Generalmente, Puppet funciona con un agente que se ejecuta en los nodos (servidores) y un nodo central (Puppet Master) que almacena la configuración.

- **Automatización de Tareas:** Automatiza la instalación de software, la gestión de usuarios, las actualizaciones de parches de seguridad y la gestión de configuraciones complejas.

- **Convergencia:** La herramienta ajusta continuamente el sistema para que coincida con el estado definido, asegurando que los servidores no se desvíen de la configuración deseada.

## Componentes

- Una **`clase`** en Puppet es un bloque de código nombrado y reutilizable que agrupa un conjunto de recursos (archivos, paquetes, servicios) para configurar un aspecto específico de un nodo, logrando que alcance un estado deseado. Son fundamentales para organizar la configuración, facilitando la lectura y reutilización de código en infraestructuras.

- En puppet, los **`recursos`** son la unidad básica para ​modelar la configuración que queremos gestionar.

- **`Manifiesto de Puppet`**, es un archivo de configuracion usado para administrar sistemas usando el framework de automatizacion Puppet.

- **`fact`**: son Variable que representa las características de un sistema.

## Ejemplos

```
class sudo {
  package { 'sudo':
    ensure => present,
  }
}
```

> [!NOTE]
> Este bloque de código dice que el paquete 'sudo' debe estar presente en cada computadora donde se aplique la regla. Si esta regla se aplica en 100 ordenadores, el paquete se instalará automáticamente en todos ellos. Se trata de un bloque pequeño y sencillo, pero puede darnos una idea básica de cómo se escriben las reglas en puppet.

```
class ntp {
  package { 'ntp':
    ensure => latest,
  }
  file { '/etc/ntp.conf':
    source => 'puppet:///modules/ntp/ntp.conf'
    replace => true,
  }
  service { 'ntp':
    enable  => true,
    ensure  => running,
  }
}
```

> [!NOTE]
> Este bloque de código incluye una clase con tres recursos, un paquete, un archivo y un servicio. Todos ellos están relacionados con el Protocolo de Tiempo de Red, o NTP, el mecanismo que utilizan nuestros ordenadores para sincronizar los relojes. Este código asegura que el paquete NTP se actualiza siempre a la última versión. Estamos estableciendo el contenido del fichero de configuración usando el atributo source, lo que significa que el agente leerá el contenido requerido desde la ubicación especificada. Y estamos diciendo que queremos que el servicio NTP esté habilitado y funcionando. Al agrupar todos los recursos relacionados con NTP en la misma clase, sólo necesitamos un rápido vistazo para entender cómo está configurado el servicio y cómo se supone que debe funcionar. Esto facilitaría la realización de cambios en el futuro, ya que tenemos todos los recursos relacionados juntos. Tiene sentido utilizar esta técnica siempre que queramos agrupar recursos relacionados.

```
#Manifiesto de Puppet

if $facts['is_virtual'] {
  package { 'smartmontools':
    ensure => purged,

  }
} else {
  package { 'smartmontools':
    ensure => installed,
  }
}
```

> [!NOTE]
> El código que ha proporcionado es una sentencia if . Una sentencia if es una sentencia condicional que ejecuta un bloque de código si se cumple una determinada condición. En este caso, la condición es si el hecho is_virtual es verdadero. El hecho is_virtual es un hecho integrado que Puppet utiliza para determinar si el nodo es una máquina virtual.

> Si el dato is_virtual es verdadero, se ejecutará el código del bloque de sentencia if. Este codigo purgara el paquete smartmontools. El paquete smartmontools es un paquete de software que proporciona herramientas para monitorizar y gestionar discos duros. Purgar el paquete smartmontools en una máquina virtual se hace típicamente para mejorar el rendimiento.

> Si el hecho is_virtual se establece en false, entonces se ejecutará el código en el bloque de sentencia else. Este código instalará el paquete smartmontools.

> En este bloque de código, el valor del hecho is_virtual es verdadero, por lo que se ejecutará el código del bloque de sentencia if. Esto significa que se purgará el paquete smartmontools.

```
file { '/etc/issue':
  mode    => '0644',
  content => "Internal system \l \n",
}
```

> [!NOTE]
> Este recurso asegura que el archivo /etc/issue tiene un conjunto de permisos y una línea específica en él. Cumplir este requisito es una operación idempotente. Si el archivo ya existe y tiene el contenido deseado, entonces Puppet entenderá que no hay que realizar ninguna acción. Si el archivo no existe, entonces Puppet lo creará. Si el contenido o los permisos no coinciden, Puppet los corregirá. No importa cuantas veces el agente aplique la regla, el resultado final es que este archivo tendrá los contenidos y permisos solicitados.

## Instalación

```bash
sudo apt install puppet-master
#puppetserver.service is a disabled or a static unit, not starting it.
#Setting up puppet-master (8.4.0-1) ...
vim tools.pp
# package{'htop':
#  ensure => present,
#}
htop
# Command 'htop' not found, but can be installed with:
# sudo snap install htop  # version 3.5.0, or
# sudo apt  install htop  # version 3.2.2-2
# See 'snap info htop' for additional versions.
sudo puppet apply -v tools.pp
# Notice: Compiled catalog for stonecolombia in environment production in 0.57 seconds
# Info: Using environment 'production'
# Info: Applying configuration version '1776218897'
# Notice: /Stage[main]/Main/Package[htop]/ensure: created
# Info: Creating state file /var/cache/puppet/state/state.yaml
# Notice: Applied catalog in 8.92 seconds
htop
sudo puppet apply -v tools.pp
```

## Nodos

```
node default {
  class { 'sudo': }
  class { 'ntp':
        servers => ['ntp1.example.com', 'ntp2.example.com']
  }
} /
```

> [!NOTE]
> El comando `node default` instala las clases sudo y ntp en todos los nodos por defecto. La clase sudo se instala con sus parámetros por defecto, porque no se especifican parámetros. La clase ntp se instala con un parámetro adicional, indicado por `servers => ['ntp1.example.com', 'ntp2.example.com']`.

```
node webserver.example.com {
  class { 'sudo': }
  class { 'ntp':
        servers => ['ntp1.example.com', 'ntp2.example.com']
  }
  class { 'apache': }
}
```

> [!NOTE]
> El comando `node webserver.example.com` instala las clases sudo, ntp y apache en nodos con el nombre de dominio completamente calificado (FQDN) webserver.ejemplo.com.

**Nota**: Dado que los nodos con este FQDN tienen un conjunto específico de clases que se les aplican, el comando `node default` no les aplicará ninguna clase.

## Configuración Cliente Servidor

```bash
sudo puppet config --section master set autosign true
```

Este comando configura Puppet para firmar automáticamente las solicitudes de certificado de los nodos añadidos.

---

```bash
ssh webserver
sudo apt install puppet
sudo puppet config set server ubuntu.example.com
```

El comando ssh webserver permite hacer ssh en una máquina llamada webserver. El comando sudo apt install puppet instala el agente de Puppet en webserver con el paquete Puppet. Luego, el comando sudo puppet config set server ubuntu.example.com configura Puppet para hablar con el servidor en ubuntu.ejemplo.com.

---

```bash
sudo puppet agent -v --test
```

Este código prueba la conexión entre el agente de Puppet en la máquina y el Puppet master. El comando -v indica que la salida debe ser verbosa, y el comando --test indica que se trata de una ejecución de prueba.

---

```
vim /etc/puppet/code/environments/production/manifests/site.pp

node webserver {
  class { 'apache': }
}

node default {}
```

Visualice y cree el archivo de manifiesto `site.pp` entrando en modo de edición con el comando `vim` . Primero, para instalar Apache en los nodos del servidor web, define el nodo del servidor web con el comando `node webserver`, y luego incluye la clase Apache sin ningún parámetro con `class{‘apache’}`. En segundo lugar, define el nodo por defecto con el código `node default{}`. Todavía no añadiremos ninguna clase.

---

```bash
sudo systemctl enable puppet
```

Este codigo usa el comando `systemctl` para habilitar el servicio puppet con el parametro `enable` para que el agente Puppet se inicie cada vez que la maquina se reinicie.

---

```bash
sudo systemctl start puppet
sudo systemctl status puppet
```

Este código inicia el servicio puppet con el parámetro start , luego comprueba su estado con el parámetro status.

## Modificación y comprobación de manifiestos

```bash
describe 'gksu', :type => :class do
  let (:facts) { { 'is_virtual' => 'false' } }
  it { should contain_package('gksu').with_ensure('latest') }
end
```

> [!NOTE]
> Este código ejecuta una prueba rspec para determinar si el paquete gksu tiene el comportamiento previsto cuando el hecho is_virtual se establece en false. Cuando este es el caso, el paquete gksu debe tener el parámetro ensure establecido en latest: ensure('latest').
