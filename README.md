# Uso de Workflows

Los Workflows, o flujos de trabajo, se refiere a qué convención toma un equipo para hacer introducir cambios en el repositorio. Se basa en qué uso le daremos a las ramas.

## Gitflow

Se usan dos ramas principales: **main** y **develop**. 

También tenemos ramas auxiliares: **feature**, **release** y **hotfix**.

### main

* Rama principal.
* Siempre debe contener el código estable listo para la producción.
* Cada vez que se hace un **release** o **deployment**, proviene de esta rama.

### develop

* Aquí es donde se desarrolla el código.
* Es la rama intermedia donde todos los programadores integran su trabajo.
* Antes de integrar el código en producción, se deben hacer las pruebas en esta rama.
* **Es el punto de partida para ramas de features.**

### feature

* Se crean a partir de la rama **develop**.
* Se usa para cada nueva funcionalidad que se quiere implementar.
* Nombre común: `feature/nueva-funcionalidad`
* Cuando la feature está terminada, se hace merge de nuevo con **develop**.

### release

* Se crean a partir de **develop** cuando se quiere preparar **una nueva versión** para producción.
* Se usa para preparar la release: pruebas finales y corrección de errores.
* Una vez que el código está listo para producción, se fusiona tanto en **main** como en **develop** (para que develop se mantenga actualizado).
* Nombre común: `release/v.1.2.0`.

### hotfix

* Se crea a partir de **main** cuando es necesario hacer algún **arreglo urgente** en producción debido a algún bug.
* Después de arreglar el problema, la rama **hotfix** se mergea tanto en **main** como en **develop**.
* Nombre común: `hotfix/arreglo-urgente`

## Forking Workflow

1. Haces fork del repositorio original (upstream) para tener una copia de ese repositorio en tu cuenta de GitHub (origin).
2. Clonas tu fork en tu máquina local.
3. Opcionalmente, puedes configurar un remote adicional hacia el repositorio original: `git remote add upstream url-repo-original`.
4. Creas ramas para trabajar nuevas funcionalidades en tu repositorio local. 
5. Subes los cambios a tu fork: `git push origin feature/nueva-feature`.
6. Creas una **pull request** desde tu fork hasta el repositorio original. 
7. Los desarrolladores del proyecto original revisarán, discutirán, te darán feedback y si todo está bien te aceptarán la pull request, haciendo merge de tus cambios al repositorio original.