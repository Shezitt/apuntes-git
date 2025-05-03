# Git

## ¿Qué es Git?

## Instalación (Linux)

Para instalar Git en Linux, basta con ejecutar el siguiente comando:

```bash
sudo apt install git
```

## Configuraciones iniciales

Una vez instalado Git, en el caso de Linux, tenemos que configurar algunos puntos importantes: nuestro nombre, correo y nuestro editor de texto preferido.

Para ver la configuración actual (a nivel `global`) podemos usar el siguiente comando:

```bash
git config --global --list
```

En realidad, hay diferentes jerarquías de configuración, de ahí una de ellas es `global`. Las jerarquías, en orden de más general a más específico, son las siguientes:

1. `system`
2. `global`
3. `local`

Por ejemplo, esta es mi configuración global actualmente (resultado de ejecutar el anterior comando):

```bash
core.editor=code --wait
user.name=Shezitt
user.email=shamirteranmustafa@gmail.com
init.defaultbranch=main
```

Los más fundamentales son los primeros tres. El último lo configuré para asegurarme que la rama principal sea `main`, respetando la convención actual.

Para establecer alguna configuración, se sigue la siguiente sintaxis, por ejemplo para configurar el user.email a nivel `global`:

```bash
git config --global user.email "shamirteranmustafa@gmail.com"
```