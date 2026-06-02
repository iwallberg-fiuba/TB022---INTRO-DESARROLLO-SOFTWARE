- Desde IDE
- Desde terminal




### Crear Repositorio

1. Estar en la carpeta donde se desea crear el repositorio.
2. Click derecho en la carpeta y seleccionar **"Abrir en Terminal"** o abrir en Git Bash (el nombre puede variar según el sistema operativo).
3. Ejecutar:

```shell
git init
```

Esto crea un repositorio Git local (aparece una carpeta oculta `.git`).

4. Verificar el estado del repositorio:

```shell
git status
```

5. Agregar los archivos al área de staging:

```shell
git add .
```

6. Crear el primer commit:

```shell
git commit -m "Primer commit"
```

## Crear ramas
Nota: Uso switch porque me resulta más práctico.

- La rama principal suele llamarse `main`.
- No se debe trabajar directamente sobre ella.

1. Ver las ramas existentes:

```shell
git branch
```

2. Cada integrante debería tener su propia rama. Para crearla:
Nota: al crearla ya quedas parado en esa nueva rama.

```shell
git switch -c nombre-de-la-rama
```


Nota: ejemplos de nombres de ramas

```shell
git switch -c feature/login
git switch -c feature/navbar
git switch -c fix/dockerfile
git switch -c docs/readme
```

- Si se desea cambiar de rama:

```shell
git switch nombre-rama-destino
```


