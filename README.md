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

### Unstaged 

Archivos cuyos cambios están siendo monitoreados por Git; y el archivo ha cambiado respecto al último commit.

![Archivos unstaged](/images/unstaged.png)


