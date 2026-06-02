# Version control Systems (VCS)

Son sistemas que permiten versionar archivos permitiendo volver a estados anteriores de ser necesario y facilitando la colaboración en la elaboración del mismo.

Un sistema de control de versiones nos permite hacer un seguimiento de cuándo y quién hizo qué cambios en nuestros archivos. Puede tratarse de código, configuración, imágenes o cualquier otra cosa que necesitemos controlar.

## Ventajas

- Permite volver a versiones anteriores del mismo archivo
- Permite comparar versiones anteriores con la actual para ver los cambios realizados
- Permite trabajar en colaboración con otras personas sin sobrescribir el trabajo de los demás
- Permite tener un historial de cambios realizado en el archivo
- Permite trabajar en ramas para desarrollar nuevas funcionalidades sin afectar la rama principal
- Permite fusionar ramas para integrar nuevas funcionalidades a la rama principal
- Permite resolver conflictos cuando dos personas editan el mismo archivo al mismo tiempo

## `diff`

`diff` muestra todas las diferencias entre cualquier tipo de archivo. Al resaltar lo que ha cambiado, nos ayuda a entender los cambios y ver cómo se han modificado los archivos.

`<` cuando tenemos un menor que indica que la linea fue eliminada del 1 archivo a comparar

`>` cuando tenemos un mayor que indica que la linea fue añadida al 1 archivo a comparar

`-u` muestra los cambios en formato unificado

## patch

`patch` es una herramienta que se utiliza para aplicar cambios a archivos existentes. Se utiliza comúnmente para aplicar parches a código fuente, pero también se puede utilizar para aplicar cambios a cualquier tipo de archivo.

```bash
# Visualizar el contenido del primer archivo (el original corto)
~$ cat hello_world.txt
Hello World

# Visualizar el contenido del segundo archivo (la versión modificada/larga)
~$ cat hello_world_long.txt
"Hello World
It's a wonderful day!"

# Comparar archivos y mostrar las diferencias en formato unificado (-u)
# El símbolo '-' indica lo que se quitaría y '+' lo que se añade
~$ diff -u hello_world.txt hello_world_long.txt
--- hello_world.txt     2019-12-16 19:24:12.556102821 +0900
+++ hello_world_long.txt        2019-12-16 19:24:38.944207773 +0900
@@ -1 +1,3 @@
 Hello World
+
+"It's a wonderful day!"

# Crear un archivo de parche (.diff) redirigiendo la salida del comando anterior
~$ diff -u hello_world.txt hello_world_long.txt > hello_world.diff

# Aplicar el parche al archivo original para actualizarlo automáticamente
~$ patch hello_world.txt < hello_world.diff
patching file hello_world.txt

# Verificar que el archivo original ahora tiene los cambios aplicados
~$ cat hello_world.txt
Hello World
It's a wonderful day!
```

## git

Git es un sistema de control de versiones distribuido que permite a los desarrolladores colaborar en proyectos de software. Fue creado por Linus Torvalds en 2005 para gestionar el desarrollo del kernel de Linux.

Git es un sistema de control de versiones distribuido, lo que significa que cada desarrollador tiene una copia completa del repositorio en su máquina local. Esto permite trabajar sin conexión y facilita la colaboración entre desarrolladores.

### áreas principales (o estados)

En Git, el flujo de trabajo se divide en tres áreas principales (o estados) por las que pasan tus archivos antes de guardarse definitivamente en el historial. Entender esto es clave para no borrar nada por accidente.

1. **Directorio de trabajo (Working Directory):**

Es el estado en el que se encuentran tus archivos actualmente. Son los archivos físicos que ves y editas en tu editor de código (como VS Code).

- **Estado:** Aquí los archivos están "Modified" (modificados) pero Git aún no ha tomado una "foto" oficial de ellos.

2. **Área de preparación (Staging Area / Index):**

Es una zona intermedia, como un muelle de carga. Aquí es donde colocas los archivos que quieres incluir en tu próximo guardado (commit).

- **Comando:** Se usa git add para mover archivos aquí.

- **Estado:** Los archivos están "Staged" (preparados).

3. **Directorio de Git (Repository / .git directory):**

Es donde Git guarda permanentemente las capturas de tu proyecto en una base de datos. Es el historial real.

- **Comando:** Se usa git commit para mover los archivos del área de preparación al repositorio.

- **Estado:** Los archivos están "Committed" (confirmados).

**Resumen del flujo:**

1. Modificas un archivo en tu **Directorio de trabajo**.
2. Preparas el archivo con `git add` para llevarlo al **Staging Area**.
3. Confirmas los cambios con `git commit` para guardarlos en el Repositorio.

### git config

Permite establer el usuario que interactuara con git

- **`user.email`:**

- **`user.name`:**

### git init

Permite crear un nuevo repositorio de git en el directorio actual

### git add

Permite agregar archivos al área de preparación (staging area) para su posterior confirmación (commit)

### git status

Permite verificar el estado actual del repositorio, mostrando los archivos modificados, los archivos en el área de preparación y los archivos sin seguimiento.

### git commit

Permite confirmar los cambios realizados en el área de preparación, creando un nuevo commit con un mensaje descriptivo.

- **`-m`:** permite establecer el mensaje del commit

- **`-a`:** permite realizar un commit sin antes hacer un add al archivo

> [!IMPORTANT]
> Si no se agrega la bandera `-m` se abrira el editor de texto predeterminado para agregar el comentario si este no se agrega un comentario se cancela el commit

**Recomendaciones:**

Un mensaje de commit debe iniciar con una breve descripción del cambio (hasta 50 caracteres), seguida de una línea en blanco y, a continuación, uno o varios párrafos con más detalles del cambio (si es necesario). Cada línea del párrafo o párrafos detallados debe tener menos de 72 caracteres.

```bash
Se corrigió el problema de conexión a la BD

Según lo reportado en el ticket 53, había un problema al reconectarse a
la base de datos. Al revisar el código, se detectó la causa y el
problema fue resuelto. Ante cualquier inconveniente, puede abrir otro
ticket en los issues de la BD.
```

### git log

muestra el historial detallado de confirmaciones (commits) de un repositorio, ordenado cronológicamente desde el más reciente. Proporciona el hash del commit, autor, fecha y mensaje.

- **`-p`** Muestra los cambios (patch) introducidos en cada commit.

- **`-1`** Limita el número de confirmaciones (commits) que se muestran en el historial a 1. Este número es variable puedes colocar la cantidad que quieras.

### git checkout

se utiliza para cambiar de rama. Por ejemplo, puede que quieras hacer un pull desde tu rama principal. En este caso, usarías el comando `git checkout main`. Esto cambiará a tu rama principal, permitiéndote hacer pull. Luego podrías cambiar a otra rama usando el comando `git checkout <branch>`.

- **`-b`** permite crear una rama y cambiarse a ella

tambien sirve para volver al estad o anterior es decir al ultimo commit

```bash
git checkout HEAD
```

### git commit --amend

se utiliza para realizar cambios en tu confirmación más reciente a posteriori, lo que puede ser útil para tomar notas o añadir archivos a tu confirmación más reciente. Ten en cuenta que este comando `git --amend` reescribe y reemplaza tu confirmación anterior, así que es mejor no usar este comando en una confirmación publicada.

### git revert

hace un nuevo commit que efectivamente revierte un commit anterior. A diferencia del comando git reset que reescribe tu historial de confirmaciones, el comando `git revert` crea una nueva confirmación que deshace los cambios en una confirmación específica. Por lo tanto, una orden `revert` es generalmente más segura que una orden `reset`.

```bash
git revert HEAD
```

### git reset

permite deshacer cambios en tu historial de confirmaciones. A diferencia del comando `git revert`, el comando `git reset` reescribe tu historial de confirmaciones, lo que puede ser peligroso si ya has publicado tus cambios. El comando `git reset` tiene tres modos principales: `--soft`, `--mixed` y `--hard`.

### git show

muestra información detallada sobre un commit específico, incluyendo el mensaje del commit, el autor, la fecha y los cambios realizados en los archivos.

```bash
git show <commit>
```

### git branch

permite gestionar las ramas en un repositorio de Git. Las ramas son una forma de trabajar en diferentes versiones de un proyecto sin afectar la rama principal (main o master). Con `git branch`, puedes crear, listar y eliminar ramas.

```bash
# Listar todas las ramas en el repositorio
git branch
# Crear una nueva rama llamada "feature-branch"
git branch feature-branch
# Cambiar a la rama "feature-branch"
git checkout feature-branch
# Eliminar la rama "feature-branch"
git branch -d feature-
```

### git merge

permite fusionar una rama con otra. Por ejemplo, si has estado trabajando en una rama de características y quieres fusionarla con la rama principal, puedes usar `git merge` para integrar los cambios.

```bash
# Cambiar a la rama principal
git checkout main
# Fusionar la rama "feature-branch" con la rama principal
git merge feature-branch
```
