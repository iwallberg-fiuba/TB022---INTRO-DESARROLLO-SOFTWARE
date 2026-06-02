
Pending.






El cómo hacer las cosas sigue siendo igual, pero, al final, se debe hacer git push. Además, aparece el git pull y git status previos a modificar cualquier archivo, y funciones como el Pull Request (PR). Además, trabajar correctamente con ramas y hacer commits con mensajes atómicos pasa a ser muchísimo más importante. 
Cada integrante debe tener y trabajar en su propia rama.

---


# Trabajo en equipo con Git y GitHub

Cuando se trabaja en equipo, el flujo básico de Git sigue siendo prácticamente el mismo:

```text
modificar
↓
add
↓
commit
```

Sin embargo, aparecen nuevos conceptos y prácticas importantes:

* Cada integrante trabaja en su propia rama.
* Los cambios se suben a GitHub mediante `git push`.
* Es importante mantener la rama actualizada con `git pull`.
* Los commits deben ser claros y atómicos.
* Los cambios se incorporan mediante Pull Requests (PR).
* El código suele pasar por una etapa de revisión antes de integrarse a la rama principal.

---

## Flujo de trabajo diario

Estás en VS Code con el proyecto abierto.

### 1. Verificar en qué rama estás

```shell
git status
```

### 2. Cambiar a tu rama si es necesario

```shell
git switch nombre-rama
```

### 3. Traer los cambios más recientes

```shell
git pull
```

### 4. Verificar el estado actualizado

```shell
git status
```

### 5. Realizar los cambios deseados

Modificar, crear o eliminar archivos.

### 6. Agregar los cambios al área de staging

```shell
git add .
```

### 7. Crear un commit

```shell
git commit -m "mensaje"
```

Ejemplos:

```shell
git commit -m "feat: agrega login"
git commit -m "fix: corrige validacion de email"
git commit -m "docs: actualiza README"
```

### 8. Subir los cambios a GitHub

```shell
git push
```

Hasta este punto el flujo sigue siendo Git tradicional, con la diferencia de que ahora los cambios también quedan disponibles en GitHub.

---

## ¿Cuándo crear un Pull Request?

Cuando la funcionalidad, corrección o tarea quedó terminada y está lista para incorporarse a otra rama (generalmente `main`).

En ese momento se crea un Pull Request.

---

## Pull Request (PR)

Un Pull Request es una solicitud para incorporar los cambios de una rama dentro de otra.

Normalmente:

```text
feature/login
↓
main
```

El Pull Request ocurre en GitHub.

### 1. Ir al repositorio en GitHub

### 2. Seleccionar

```text
Pull Requests
↓
New Pull Request
```

### 3. Elegir las ramas

```text
Base branch:
rama destino
(generalmente main)

Compare branch:
rama que contiene tus cambios
```

Ejemplo:

```text
Base: main
Compare: feature/login
```

### 4. Revisar los cambios

GitHub mostrará:

* Archivos modificados.
* Líneas agregadas.
* Líneas eliminadas.
* Commits incluidos.

### 5. Crear el Pull Request

Agregar:

* Título.
* Descripción (opcional).
* Comentarios adicionales.

Luego confirmar:

```text
Create Pull Request
```

---

## Revisión

Antes de mezclar las ramas, otros integrantes pueden revisar el código.

Pueden:

* Leer el código.
* Comentar líneas específicas.
* Sugerir cambios.
* Aprobar el Pull Request.
* Solicitar modificaciones.

```text
GitHub
↓
Pull Request
↓
Revisión
↓
Aprobación
↓
Merge Pull Request
```

---

## Merge de PR

Una vez aprobado el Pull Request:

### 6. Hacer Merge

```text
Merge Pull Request
```

GitHub combinará ambas ramas.

```text
main
 │
 ├── feature/login
 │       ↓
 │      Pull Request
 │       ↓
 │      Revisión
 │       ↓
 └──── Merge
```

Ahora los cambios ya forman parte de `main` en GitHub.

---

## Limpieza posterior

### 7. Eliminar la rama remota

Después del merge GitHub suele mostrar:

```text
Pull Request merged successfully
↓
Delete branch
```

Esto elimina la rama en GitHub.

### 8. Actualizar la copia local

```shell
git switch main
git pull
```

Ahora la rama local contiene los cambios recién incorporados.

### 9. Eliminar la rama local

```shell
git branch -d feature/login
```

La rama ya no es necesaria porque su contenido fue incorporado a `main`.

---

## Resumen

```text
git switch mi-rama
↓
git pull
↓
modificar archivos
↓
git add .
↓
git commit
↓
git push
↓
crear Pull Request
↓
revisión
↓
merge
↓
git switch main
↓
git pull
↓
git branch -d mi-rama
```

La principal diferencia entre trabajar solo y trabajar en equipo no son los comandos de Git, sino el uso de ramas, Pull Requests, revisiones de código y merges controlados.







---

Estás en VS Code con el proyecto abierto.

1. Verificar en qué rama estás:

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
