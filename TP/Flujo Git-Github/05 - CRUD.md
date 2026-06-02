- Desde IDE
- Desde terminal




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

**Para subirla a Github:**

```shell
git push -u origin nombre-de-la-rama
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


