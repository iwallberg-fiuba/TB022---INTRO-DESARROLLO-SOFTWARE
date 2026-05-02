# Instructivo - Git Basico

## Objetivo

Cubrir el flujo minimo para empezar a usar Git con un repositorio local y remoto.

## 1. Configuracion inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@dominio.com"
git config --list
```

## 2. Crear o clonar un repositorio

### Crear uno nuevo

```bash
git init
```

### Clonar uno remoto

```bash
git clone git@github.com:usuario/repositorio.git
```

## 3. Ver estado

```bash
git status
```

Usalo para ver:

- archivos sin rastrear,
- archivos modificados,
- archivos en staging.

## 4. Agregar cambios

### Un archivo

```bash
git add archivo.txt
```

### Todo lo modificado

```bash
git add .
```

## 5. Crear commit

```bash
git commit -m "Mensaje descriptivo"
```

## 6. Ver historial

```bash
git log
git log --graph --oneline
```

## 7. Sincronizar con remoto

### Traer cambios

```bash
git pull
```

### Subir cambios

```bash
git push
```

## 8. Trabajar con ramas

### Crear y listar

```bash
git branch
git branch mi-rama
```

### Cambiar de rama

```bash
git checkout mi-rama
```

### Fusionar

```bash
git merge mi-rama
```

## 9. Guardar trabajo temporalmente

```bash
git stash
git stash list
git stash apply
git stash pop
```

## 10. Restaurar cambios

### Sacar del staging

```bash
git restore --staged archivo.txt
```

### Volver a ultimo commit

```bash
git restore archivo.txt
```

### Traer version de un commit puntual

```bash
git restore --source=<commit-id> archivo.txt
```

## 11. Si aparece un merge conflict

1. Corre `git status`.
2. Abre el archivo en conflicto.
3. Decide que contenido final queda.
4. Guarda el archivo.
5. Haz `git add`.
6. Cierra la fusion con commit.
