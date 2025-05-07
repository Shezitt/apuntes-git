# Git

## ¿Qué es Git?

## Instalación (Linux)

Para instalar Git en Linux, basta con ejecutar el siguiente comando:

```bash
sudo apt install git
```

## Configuraciones 

Git soporta opciones de configuración. Estas opciones son usados por los comandos de Git para definir ciertos comportamientos. Podemos settera estos ajustes con `git config`.

Estos ajustes están establecidos en tres niveles:

### A nivel de sistema

Estas están ubicadas en el archivo **/etc/gitconfig**. Los ajustes de este archivo son aplicados para todos los usuarios de la computadora. 

Para acceder a estos ajustes, tenemos que usar **git config --system**.

### A nivel de usuario

Estas se ajustan en el archivo **~/.gitconfig**. Estos ajustes serán aplicados para el usuario que corresponda.

Estos ajusten se pueden acceder mediante **git config --global**.

### A nivel de repositorio

Estos se guardan en el archivo **path_repositorio/.git/config**. Estos ajustes se aplican solo para el repositorio actual. Por ejemplo, la URL del repositorio remoto se guarda en este nivel. 

Estos ajustes se acceden mediante **git config --local**.

También podemos especificar un archivo de configuración específico usando la flag **-f** o equivalente **--file**.

Podemos listar las configuraciones actuales con:

```bash
git config --<nivel> --list
```

O también:

```bash
git config --list
```

## Configuraciones iniciales

Como configuraciones iniciales, deberíamos establecer nuestras credenciales:

1. Definir nuestro nombre de usuario:
```bash
git config --global user.name shezitt
```
(Reemplazar "shezitt" por tu nombre)

2. Definir nuestro correo electrónico:
```bash
git config --global user.email shamirteranmustafa@gmail.com
```

También podemos indicar nuestro editor de código preferido, por ejemplo para Visual Studio Code (code):

```bash
git config --global core.editor "code --wait"
```

## Eliminar configuraciones

Usando **git config** podemos eliminar ajustes usando la opción **--unset**:

```bash
git config --global --unset [seccion].[variable]
```

Por ejemplo, para eliminar nuestro nombre de usuario:

```bash
git config --global --unset user.name
```

## Configurar llave SSH

*Pendiente*.

## Crear un repositorio 

Primero crearemos un repositorio local, utilizando **git init**:

1. Creamos un directorio en la ruta que deseemos, esta será para nuestro repositorio:

```bash
~/Documentos/repos/> mkdir Nuevo-Repo
```

2. Entramos en el directorio creado:

```bash
cd Nuevo-Repo
```

3. Ejecutamos **git init**:

```bash
git init
```

## Los commits

En Git, los archivos tienen los siguientes estados:

### Untracked (archivos sin seguimiento)

Un archivo que existe en el directorio que estamos trabajando pero cuyos cambios todavía no han sido monitoreados por Git y no está listado en el archivo gitignore.

![Archivos sin seguimiento](/images/untracked.png)

Básicamente se refiere a archivos nuevos.

### Unstaged 

Archivos cuyos cambios están siendo monitoreados por Git; y el archivo ha cambiado respecto al último commit.

![Archivos unstaged](/images/unstaged.png)

### Staged

Archivos cuyos cambios son monitoreados por Git; el archivo cambió respecto al último commit y ha sido *stageado* al **index**. Estos archivos están listos para ser commiteados.

Un archivo entra en esta área cada vez que usamos `git add`.

Por ejemplo, al ejecutar `git add staged.txt`:

![Archivos staged](/images/staged.png)

### git status

El comando `git status` nos permite conocer los detalles de archivos del repositorio que están en estado *untracked*, *unstaged* o *staged*.

Para ver una versión más brave de la salida de este comando, podemos usar la flag **--short** o **-s**

Las capturas anteriores eran justamente resultado de ejecutar `git status`.

### git diff

El comando `git diff` nos permite ver las diferencias entre dos estados del repositorio.

#### Comparar nuestro directorio de trabajo con el Index

Recordemos que el **Index** se refiere al área de staging.

Para este fin, basta con ejecutar `git diff`.

También podemos ser más específicos:

```bash
git diff -- archivo.txt
```

Este comando comparará el archivo especificado con la versión que existe en el Index (o área de staging). 

#### Comparar nuestro directorio de trabajo con un Commit o una rama

La sintaxis para esto es la siguiente:

```bash
git diff [commit_hash] -- [path_file_or_directory]
```

Para comparar el HEAD (último commit de la rama actual) con el directorio src/ podemos usar:

```bash
git diff HEAD -- src/
```

Para comparar nuestro directorio de trabajo con la rama **master**:

```bash
git diff master
```

#### Comparar el Index con un Commit

Para comparar los archivos en el Index (área de staging) con un commit específico, se puede usar la opción **--staged** o **--cached** junto al comando `git diff`. Para esto necesitamos especificar el hash del commit, o bien tomará el HEAD por defecto:

```bash
git diff --cached [commit_hash]
```

O especificando un archivo o directorio:

```bash
git diff --cached [commit_hash] -- [path_file_or_directory]
```

Por ejemplo:

```bash
git diff --cached HEAD -- /src/main.py
```

Este último compara la versión del archivo **main.py** en el Index con el de la versión en el HEAD de la rama actual.

#### Comparar Commits y ramas

Para comparar los dos últimos commits de dos ramas, usamos la siguiente sintaxis:

```bash
git diff [commit_hash or branch_name] [commit_hash or branch_name]
```

Similar a los anteriores casos, podemos especificar un archivo o directorio a comparar:

```bash
git diff [commit_hash or branch_name] [commit_hash or branch_name] -- [path_file_or_directory]
```

### git add

Ya sabemos que un archivo puede existir en tres formas, estas son: *untracked*, *unstaged* y *staged*. 

El comando `git add` nos sirve para agregar archivos al **Index** desde nuestro directorio de trabajo:

```bash
git add [options] [path_to_files]
```

### git commit

Este comando permite crear un nuevo commit, guardando los cambios de los archivos que estaban en el Index. Este comando debe ir acompañado de un mensaje que describe el cambio asociado a esta nueva *snapshot* del repositorio.

Su sintaxis es:

```bash
git commit [options]
```

Incluyendo el mensaje asociado al commit:

```bash
git commit -m [texto]
```

### git rm

Sirve para eliminar archivos y directorios de la zona de preparación (Index / staging area) y también del directorio de trabajo.

```bash
git rm [path_to_file]
```

También tenemos la opción de eliminar un archivo solo del Index pero no de nuestro directorio de trabajo:

```bash
git rm --cached archivo.txt
```

### git mv

Este comando nos permite mover o renombrar un archivo de forma fácil ya que, internamente, combina las operaciones de eliminación y adición en un solo paso.

```bash
git mv [source] [destination]
```

### git log

Nos permite listar el historial de cambios de una rama o de todo el repositorio. 

Tiene distintas opciones, algunas son:
* `git log` para ver el historial de la rama actual.
* `git log <rama>` para ver el historial de una rama específica.
* `git log --all` muestra el historial de todas las ramas.
* `git log -n 5` muestra los últimos 5 commits.
* `git log --graph --oneline` muestra el historial con gráfico de ramas y en una línea.


### Amending Commits

Supongamos que hiciste cambios y utilizaste `git commit`, y ahora te arrepientes del mensaje del commit o incluso de los archivos que commiteaste. Ahora veremos cómo podemos "editar" commits.

#### Amend el commit más reciente

Podemos editar o rehacer el último commit con la siguiente opción:

```bash
git commit --amend
```

#### Amend varios commits

El comando **git rebase** nos proporciona las opciones **reword** y **edit** para editar commits.

La opción **reword** nos permite editar un mensaje. Mientras que la opción **edit** nos permite no solo editar un mensaje, sino también el contenido de un commit.

Cuando ejecutas:

```bash
git rebase -i HEAD~4
```

Le dices a Git: "quiero ver los últimos 4 commits y decidir qué hacer con cada uno". Aparece algo como:

```bash
pick 123abc Primer commit
pick 456def Segundo commit
pick 789ghi Tercer commit
pick abc123 Cuarto commit
```

La palabra `pick` la podemos cambiar por varias acciones:

* `pick`: dejar el commit tal cual.
* `reword`: cambiar el mensaje del commit.
* `edit`:  detenerse en ese commit para cambiar su contenido o mensaje.
* `squash`: fusionarlo con el anterior.
* `fixup`: fusionarlo sin conservar su mensaje.

Durante el rebase, puedes usar el siguiente comando para continuar:

```bash
git rebase --continue
```

## Obtener el código

En un sistema de control de versiones distribuido, el código base reside en un punto central del cual los contribuidores pueden recuperar el código, hacer cambios locales y publicar los cambios en el host central.

Algunos términos para describir el vínculo entre el código que se modifica localmente y el código hosteado en GitHub son los siguientes:

### Upstream

Este se refiere al repositorio en el hosting. De este repositorio es del cual los contribuidores pueden clonar el repositorio para sus entornos locales, hacer cambios y luego publicarlos.

Cuando se hace *forking*, hacemos fork de este repositorio. 

### Downstream

Se refiere a un repositorio que se encuentra en tu entorno local. El repositorio *downstream* es el resultado de clonar un repositorio *upstream*. Es tu copia local de un repositorio upstream.

### Remote

Un remote es simplemente una referencia a un repositorio que está alojado en otro lugar, normalmente en un servidor remoto como GitHub, GitLab, Bitbucket o incluso otro servidor privado.

Cuando clonas o creas una copia de un repositorio remoto, Git guarda una referencia para poder conectarse a ese repositorio más tarde, y le asigna un nombre.

### Origin

*origin* es el nombre por defecto que Git le pone al *remote* del repositorio desde el que clonaste.

Ejemplo:

```bash
git clone https://github.com/miusuario/mi-proyecto.git
```

Cuando clonas, Git automáticamente crea un remote llamado `origin` referenciando a esa URL.

### Diferencia entre Origin y Upstream

`origin` es el **nombre por defecto** que Git le pone al remote del repositorio desde el que clonaste.

`upstream` es **otro remote adicional que tú puedes configurar** y que generalmente se usa para referenciar el **repositorio original del que se hizo un fork**.

El escenario de acción más común de ambos sería:

* Haces un fork de un proyecto.
* Clonas tu fork (que queda como `origin`).
* Pero quieres hacer una referencia al repositorio original para traer sus cambios.

Entonces le agregas un remote llamado `upstream`.

```bash
git remote add upstream https://github.com/original/proyecto.git
```

| Nombre   | Definición                                                                                     | Cuándo se usa                                    |
|----------|------------------------------------------------------------------------------------------------|--------------------------------------------------|
| origin   | El remote por defecto que apunta al repositorio  desde el que clonaste                         | Para hacer push o pull con tu copia              |
| upstream | Un remote adicional que tú defines,  generalmente apuntando al repositorio original de un fork | Para hacer fetch o pull de los cambios oficiales |

### git remote

Un remote es simplemente una conexión a un repositorio alojado en otro lugar, normalmente en servicios como GitHub, GitLab o Bitbucket.
Te permite sincronizar cambios entre tu repositorio local y ese repositorio remoto.

#### Ver remotes configurados

```bash
git remote -v
```

Te muestra los remotes que tiene tu repositorio local y sus URL.

Por ejemplo puede salir algo así:

```bash
origin  https://github.com/miusuario/mi-repo.git (fetch)
origin  https://github.com/miusuario/mi-repo.git (push)
```

O si usamos llaves SSH:

```bash
origin  git@github.com:Shezitt/apuntes-git.git (fetch)
origin  git@github.com:Shezitt/apuntes-git.git (push)
```

#### Agregar un nuevo remote

```bash
git remote add <nombre> <url>
```

Ejemplo:

```bash
git remote add origin git@github.com:Shezitt/apuntes-git.git
``` 

#### Eliminar un remote

```bash
git remote remove <nombre>
```

#### Cambiar la URL de un remote

```bash
git remote set-url <nombre> <nueva-url>
```

## Fetch, push y pull

Estos comandos nos permiten sincronizar nuestro repositorio local con el repositorio remoto (o varios).

### git fetch

```bash
git fetch [nombre_remoto]
```

Esto descarga los cambios del remoto, pero no los aplica a tu rama actual.

Quedan en `nombre_remoto/rama` y tú decides cuándo revisarlos o hacer hacer merge. 

Por ejemplo, supongamos que hay nuevos cambios en la rama `main` en el remoto `origin`:

* `git fetch origin`
* Y luego podemos ver los cambios con:

```bash
git log origin/main
```

Pero tu rama actual no cambia.

### git push

Este comando actualiza la rama remota con nuestros commits locales.

Puedes hacer push de los commits de la rama actual a la rama remota con el comando:

```bash
git push [nombre_remoto]
```

Para especificar una rama:

```bash
git push [nombre_remoto] [nombre_rama]
``` 

Por ejemplo, para subir los cambios de la rama **main** al remoto **origin**:

```bash
git push origin main
```

### git pull

Este comando descarga **e integra** los cambios del repositorio remoto al repositorio local. 

Este comando ejecuta una combinación del comando **git fetch** y **git merge**. 

```bash
git pull [nombre_remoto] [nombre_rama]
```

## Deshacer commits

Git proporciona varias formas de revertir cambios.