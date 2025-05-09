# Obtener el código

En un sistema de control de versiones distribuido, el código base reside en un punto central del cual los contribuidores pueden recuperar el código, hacer cambios locales y publicar los cambios en el host central.

Algunos términos para describir el vínculo entre el código que se modifica localmente y el código hosteado en GitHub son los siguientes:

## Upstream

Este se refiere al repositorio en el hosting. De este repositorio es del cual los contribuidores pueden clonar el repositorio para sus entornos locales, hacer cambios y luego publicarlos.

Cuando se hace *forking*, hacemos fork de este repositorio. 

## Downstream

Se refiere a un repositorio que se encuentra en tu entorno local. El repositorio *downstream* es el resultado de clonar un repositorio *upstream*. Es tu copia local de un repositorio upstream.

## Remote

Un remote es simplemente una referencia a un repositorio que está alojado en otro lugar, normalmente en un servidor remoto como GitHub, GitLab, Bitbucket o incluso otro servidor privado.

Cuando clonas o creas una copia de un repositorio remoto, Git guarda una referencia para poder conectarse a ese repositorio más tarde, y le asigna un nombre.

## Origin

*origin* es el nombre por defecto que Git le pone al *remote* del repositorio desde el que clonaste.

Ejemplo:

```bash
git clone https://github.com/miusuario/mi-proyecto.git
```

Cuando clonas, Git automáticamente crea un remote llamado `origin` referenciando a esa URL.

## Diferencia entre Origin y Upstream

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

## git remote

Un remote es simplemente una conexión a un repositorio alojado en otro lugar, normalmente en servicios como GitHub, GitLab o Bitbucket.
Te permite sincronizar cambios entre tu repositorio local y ese repositorio remoto.

### Ver remotes configurados

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

### Agregar un nuevo remote

```bash
git remote add <nombre> <url>
```

Ejemplo:

```bash
git remote add origin git@github.com:Shezitt/apuntes-git.git
``` 

### Eliminar un remote

```bash
git remote remove <nombre>
```

### Cambiar la URL de un remote

```bash
git remote set-url <nombre> <nueva-url>
```

# Fetch, push y pull

Estos comandos nos permiten sincronizar nuestro repositorio local con el repositorio remoto (o varios).

## git fetch

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

## git push

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

## git pull

Este comando descarga **e integra** los cambios del repositorio remoto al repositorio local. 

Este comando ejecuta una combinación del comando **git fetch** y **git merge**. 

```bash
git pull [nombre_remoto] [nombre_rama]
```