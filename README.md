# Ramas y merging

## Las ramas en Git

Una rama es un puntero que apunta a un commit específico. Por defecto, todo proyecto tiene una rama llamada **main** o **master**, según la versión. Pero para trabajar ordenadamente, es muy común crear ramas nuevas para features, correcciones o pruebas. Pero esto depende del **workflow** que tomemos. 

### Crear una rama

```bash
git branch nombre-rama
```

### Cambiarse a una rama existente

```bash
git checkout nombre-rama
```

También 

```bash
git switch nombre-rama
```

O crearla y cambiarse directamente:

```bash
git checkout -b nombre-rama
```

También 

```bash
git switch -c nombre-rama
```

### Listar ramas

```bash
git branch
```

Para ver también ramas remotas:

```bash
git branch -a
```

### Renombrar una rama

Si estás en la rama que quieres renombrar:

```bash
git branch -m nuevo-nombre
```

Si no:

```bash
git branch -m nombre-viejo nuevo-nombre
```

Ejemplo:

```bash
git branch -m feature/login feature/signin
```

### Eliminar una rama

#### Localmente

```bash
git branch -d nombre-rama
```

Puedes usar `-d` si la rama ya fue fusionada. Y `-D` si quieres forzar la eliminación aunque no haya sido fusionada.

#### Remotamente

```bash
git push origin --delete nombre-rama
```

### Merging 

Un **merge** combina los cambios de una rama en otra. Normalmente se hace para traer cambios de una rama secundaria a **main** o **develop**.

Primero te posicionas en la rama donde quieres realizar los cambios:

```bash
git checkout main
```

Luego:

```bash
git merge nombre-rama-a-unir
```

Ejemplo: 

```bash
git merge feature/login
```

#### Listar el historial de ramas y merges

```bash
git log --oneline --graph --all
```

### git stash

Es un comando que guarda temporalmente los cambios no guardados (sin commitear) tanto de tu área de trabajo como de tu stating area, para que puedas volver a un estado limpio del repositorio sin perder tus cambios. 

Los guarda en una "pila temporal" llamada *stash stack*.

Se suele usar cuando estás trabajando en algo pero de repente quieres:

* Cambiar de rama.
* Hacer un pull.
* Solucionar un hotfix urgente.
* Revisar algo sin perder tus cambios en lo que estás trabajando.

```bash
git stash
git checkout main
```

Esto hará que tus cambios se guarden en el stash, dejando tu área de trabajo limpia. Y luego cambias a la rama main.

También puedes guardarlos con una descripción:

```bash
git stash save "trabajo en login"
```

#### Ver lista de stashes guardados

```bash
git stash list
```

#### Recuperar cambios

Para recuperar el stash más reciente:

```bash
git stash apply
```

O para aplicar uno específico:

```bash
git stash apply stash@{numero}
```

Para aplicar **y eliminarlo de la pila**:

```bash
git stash pop
```

Para eliminar un stash:

```bash
git stash drop stash@{numero}
```

Para eliminar todos los stash:

```bash
git stash clear
```

#### Guardar también archivos sin trackear

Para incluir archivos no trackeados (archivos nuevos):

```bash
git stash -u
```

## Pull Request

Una Pull Request (PR) es una solicitud que se hace para informar a otros desarrolladores de que se ha realizado una serie de cambios en una rama y se desea que estos cambios se integren en otra rama, generalmente en la rama main o develop.

El término Pull Request se usa principalmente en GitHub y Bitbucket. En GitLab se llama Merge Request, pero el concepto es el mismo.

1. Supongamos que tienes tu rama `feature/nueva-funcion`

2. Haces tus cambios y tus commits en esa rama.

3. Haces push a tu remoto.

4. Se crea la **Pull Request** desde GitHub.

    * Eliges:
        * Rama de origen: `feature/nueva-funcion`
        * Rama de destino: `main` (por ejemplo).

5. Los revisores analizan el código: pueden comentar, sugerir cambios o aprobarlo.

6. Se pueden hacer cambios adicionales en la misma rama y se actualiza automáticamente en la misma PR.

7. Si se aprueba, **se hace el merge** de la PR a la rama destino.

8. Opcionalmente, puedes borrar tu rama feature luego del merge.

### Usos

* Revisar código antes de integrarlo al repositorio principal.
* Colaborar y discutir cambios con otros desarrolladores.
* Mantener un flujo de trabajo ordenado y seguro en proyectos colaborativos.
* Hacer control de calidad antes de incorporar nuevas funciones, correcciones o mejoras.