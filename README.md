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