# Deshacer commits

Git proporciona varias formas de revertir cambios.

## git revert

Revierte los cambios introducidos por el commit especificado. 

```bash
git revert [commit_hash]
```

## git reset

Este comando mueve el puntero **HEAD** a otro commit.

Dependiendo del modo que escojamos (`--soft`, `--mixed`, `--hard`), afecta también a tu staging area y tu directorio de trabajo.

### git reset --soft [commit_hash]

Resetea el HEAD al commit especificado, pero no altera tu directorio de trabajo ni tu area de staging, permanecen tal cual como estaban.

### git reset --hard [commit_hash]

Resetea el HEAD al commit especificado. Tu área de staging y directorio de trabajo se descartan. 

### git reset --mixed [commit_hash]

Resetea el HEAD al commit especificado. Tu área de staging se pierde, pero tu directorio de trabajo se mantiene.