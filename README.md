# Trucos en Git

## Git Hooks

Git hooks son scripts que se ejecutan automáticamente en ciertas fases de un repositorio Git, como antes de un commit, después de un push, etc.

Los hooks se encuentran en el directorio `/.git/hooks` de tu repositorio. Git trae algunos scripts de ejemplo en ese directorio con extensión `.sample`.

### Tipos de hooks

* `pre-commit`: Se ejecuta antes de un `git commit`. Puedes usarlo para ejecutar pruebas, análisis estático, o formatear el código antes de hacer el commit.

* `commit-msg`: Se ejecuta después de un commit, pero antes de que Git registre el mensaje. Es útil para asegurar que los mensajes de commit sigan un formato específico.

* `pre-push`: Se ejecuta antes de un `git push`. Puedes usarlo para hacer pruebas antes de subir tu código al repositorio remoto.

## Git Aliases

Los aliases son una forma de crear comandos personalizados para hacer más fácil el uso de Git. Puedes definir tus propios comandos o abreviar comandos largos para usarlos más rápido.

```bash
git config --global alias.<nombre-alias> <comando-de-git>
```

Por ejemplo, se puede configurar un alias para un comando largo como `git log`:

```bash
git config --global alias.lg "log --oneline --graph --all --decorate"
```

## git cherry-pick

Permite aplicar un commit específico de una rama a otra, sin necesidad de hacer un merge completo.

Es útil cuando quieres traer solo uno (o varios) cambios puntuales de otra rama, sin arrastrar todo el historial.

Sintaxis:

```bash
git cherry-pick <hash_del_commit>
```

Por ejemplo, digamos que en la rama `feature-x` hiciste un commit con hash `a1b2c3d` que necesitas en `main`.

Desde `main`:

```bash
git cherry-pick a1b2c3d
```

## git bisect

Es una herramienta para encontrar rápidamente qué commit introdujo un bug usando búsqueda binaria.

### Cómo funciona

* Le dices a Git cuál fue el último commit bueno y cuál es el malo (donde ya está el error).
* Git va probando commits intermedios (por mitad) y te pregunta si ese commit está bien o mal.
* Así, reduce las pruebas de forma eficiente hasta encontrar el commit problemático.

### Comandos básicos

```bash
git bisect start
git bisect bad          # Marca el commit actual como defectuoso
git bisect good <hash>  # Marca un commit anterior como correcto
```

Luego, Git te posicionará en commits intermedios. Ahí tú pruebas manualmente el código y le dices: `git bisect good` o `git bisect bad`.

Cuando lo encuentre, te indicará cuál fue el primer commit que introdujo el bug. Para terminar usas `git bisect reset`, para volver al estado original. 

