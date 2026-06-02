

## Trabajar con ramas y colaboradores

Estás en VS Code con el proyecto abierto.

1. Verificar en qué rama estás:

```shell
git branch
```

o:

```shell
git status
```

2. Cambiar a tu rama si es necesario:

```shell
git switch nombre-rama-destino
```

3. Traer los cambios más recientes del repositorio remoto:

```shell
git pull
```

4. Verificar el estado actualizado del repositorio:

```shell
git status
```

5. Realizar los cambios deseados en el código.

6. Agregar los cambios al área de staging:

```shell
git add .
```

7. Crear un commit:

```shell
git commit -m "mensaje"
```

Ejemplos de mensaje de commit:

```shell
git commit -m "Agrego pantalla de login"
git commit -m "Corrijo error en Dockerfile"
git commit -m "Actualizo README"
```

8. Subir los cambios a GitHub:

```shell
git push
```

Una vez hechos estos pasos: 
¿Qué pasa si el feature que quería agregar ya está completamente listo y no se volverá a editar? -> ahí aparecen las Pull Requests (PR).

---

## Pull Request (PR)

Un Pull Request es una solicitud para que los cambios de una rama se incorporen a otra (generalmente a `main`).
El **Pull Request ocurre en GitHub**, mientras que **add, commit, push, pull, switch y merge local** son comandos de Git.

1. Ir a GitHub.

2. Seleccionar:

```text
Pull Requests
↓
New Pull Request
```

3. Elegir:

Base branch: rama destino (generalmente main)
Compare branch: rama a incorporar a la rama destino (la tuya)

4. Revisar los cambios que muestra GitHub.

5. Confirmar "Crear el Pull Request".

Ahora se debe esperar a que el Pull Request (PR) pase la etapa de Revisión para después hacer el Merge.


## Revisión

6. Los integrantes del equipo pueden:

* Leer el código.
* Comentar líneas específicas.
* Sugerir cambios.
* Aprobar o rechazar el Pull Request.

```text
GitHub
↓
Pull Request 
↓
Revisión de todos los colaboradores
↓
Botón Merge Pull Request
```

La línea de tiempo de ramas sería algo como:

```text
main
 │
 ├── feature/login
 │       ↓
 │      Pull Request
 │       ↓
 |      Revisión
 |       ↓
 └──── merge PR 
```

## Merge de PR

7. Cuando el Pull Request fue revisado, se toca el botón `Merge Pull Request`.
GitHub combinará las ramas y main quedará actualizada en github, pero no localmente.

8. Ahora se debe apretar:

```txt
Pull Request merged successfully
↓
Delete branch
```

9. Actualizar la copia local:

```shell
git switch main
git pull
```

10. Eliminar la rama completada (la local):

```shell
git branch -d feature/login
```
