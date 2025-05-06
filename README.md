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