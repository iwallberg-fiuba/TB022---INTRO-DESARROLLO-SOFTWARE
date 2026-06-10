
<br><br>

### Table of Contents

<br>

[Flujos](#Flujos)
- [Crear Rama](#Crear-Rama)
- [General](#General)
- [Crear Pull Request](#Crear-Pull-Request)
- [Post Pull Request](#Post-Pull-Request)

<br>

[Templates](#Templates)
- [Commit Mensajes](#Commit-Mensajes)
- [Nombres Ramas](#Nombres-Ramas)
- [Issues y Etiquetas](#Issues-y-Etiquetas)

<br>

[Aprendizaje](#Aprendizaje)
- [Trabajo en Grupo](#Trabajo-en-Grupo)
- [Pull Requests](#Pull-Requests)
    - [Revisión](#Revisión)
- [Issues](#Issues)

<br>

---

<br><br>

## Flujos

<br><br>

### Crear Rama

<br>

Cuando la rama en la que se debe trabajar no existe todavía:

<br>

```text
Abrir la IDE con el repositorio
↓
git status
↓
git switch main
↓
git pull
↓
git switch -c feature/login
↓
Modificar archivos
↓
git status
↓
git add .
↓
git commit -m "mensaje"
↓
git push -u origin feature/login
↓
Crear Pull Request
```

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br><br>

### General

<br>

Cuando la rama en la que se debe trabajar ya existe:

<br>

```text
Abrir la IDE con el repositorio
↓
git status
↓
git switch feature/login
↓
git pull
↓
Modificar archivos
↓
git status
↓
git add .
↓
git commit -m "mensaje"
↓
git push
```

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br><br>

### Crear Pull Request

<br>

Cuando se considera lista la rama:

<br>

```text
Venís de un push
↓
Si la branch está lista para mergear:
git switch main
↓
Github Repositorio
↓
Seleccionar "Pull Requests"
↓
Seleccionar "New Pull Request"
↓
Elegir "base" y "compare branch"
↓
Completar datos
↓
Seleccionar "Create Pull Request"
↓
Esperar la revisión de los demás para lograr la Merge del PR
```

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br><br>

### Post Pull Request

<br>

```txt

Se crea un Pull Request
↓
GitHub intenta hacer el merge
↓
¿Hay conflictos?
├─ Sí (Merge Conflict)
│   ↓
│   GitHub bloquea el merge
│   ↓
│   git pull
│   ↓
│   Resolver conflictos manualmente
│   ↓
│   git add .
│   ↓
│   git commit
│   ↓
│   git push
│   ↓
│   GitHub verifica nuevamente
│   ↓
│   ¿Hay conflictos?
│   ├─ Sí → repetir proceso
│   └─ No
│
└─ No
    ↓
    GH habilita el botón Merge Pull Request
    ↓
    GH muestra "Pull Request merged successfully"
    ↓
    GH muestra botón "Delete branch"
    ↓
    Apretarlo
    ↓
    Volver al repositorio local
    (queda actualizarlo y borrar la rama local de la rama que fue mergeada)
    ↓
    git switch main
    ↓
    git pull
    ↓
    git branch -d nombre-rama-mergeada
    ↓
    git status
```

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br>

---

<br>

## Templates

<br><br>

### Commit Mensajes

<br>



<br><br><br><br>

### Nombres Ramas

<br>



<br><br><br><br>

### Issues y Etiquetas

<br>

Campos que tiene:

<br>

| Campo       | Para qué sirve             |
| ----------- | -------------------------- |
| Título      | Resumen corto              |
| Descripción | Explicación detallada      |
| Etiquetas   | Categorías                 |
| Assignees   | Personas responsables      |
| Comments    | Discusión                  |
| Milestone   | Versión o entrega asociada |

<br><br>

Etiquetas:

<br>

| Etiqueta           | Significado              |
| ------------------ | ------------------------ |
| `bug`              | Error                    |
| `feature`          | Nueva funcionalidad      |
| `enhancement`      | Mejora                   |
| `documentation`    | Documentación            |
| `help wanted`      | Se necesita ayuda        |
| `good first issue` | Ideal para principiantes |

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br>

---

<br>

## Aprendizaje

<br><br>

### Trabajo en Grupo

<br>

Cuando se trabaja en equipo, el flujo de Git sigue siendo prácticamente el mismo:

```text
modificar
↓
add
↓
commit
```

<br>

Sin embargo, aparecen nuevos conceptos y ciertas prácticas se vuelven más importantes:

<br>

* Origin: nombre del repositorio remoto que apunta al local
* git status
* Mantener la rama actualizada con `git pull`.
* Trabajar en ramas y no en main.
* Que los nombres de las ramas sean los sugeridos por las buenas prácticas.
* Cada integrante debe trabajar en su propia rama.
* La relevancia de los mensajes (que sean como los propuestos por las buenas prácticas) del commit aumenta.
* Después de cada commit, hay que subir los cambios a GitHub mediante `git push`.
* Las ramas se mergean mediante Pull Requests (PR).

<br><br><br><br>

### Pull Requests

<br>

Qué es? <br>
Es una solicitud para incorporar los cambios de una rama dentro de otra.

<br>

Cuándo se hace? <br>
Cuando se cree que una rama está lista para unirse a (generalmente) main, se crea una Pull Request (PR).

<br>
<br>

Cómo se hace?

1. Ir al repositorio en GitHub

2. Seleccionar

<br>

```text
Pull Requests
↓
New Pull Request
```

<br><br>

3. Elegir cuál va a ser la base branch (rama destino, generalmente main) y la compare branch (rama a unir).

<br>

Ejemplo:
```text
Base: main
Compare: feature/login
```

<br><br>

4. Revisar los cambios. GitHub mostrará:

<br>

* Archivos modificados.
* Líneas agregadas.
* Líneas eliminadas.
* Commits incluidos.

<br><br>

5. Agregar datos pedidos como título, descripción, comentarios y confirmar con:

<br>

```text
Create Pull Request
```

<br><br><br><br>

### Revisión

<br>

6. Antes de mezclar las ramas, otros integrantes pueden revisar el código.

<br>

Pueden:

* Leer el código.
* Comentar líneas específicas.
* Sugerir cambios.
* Aprobar el Pull Request.
* Solicitar modificaciones.

<br><br><br><br>

### Issues

<br>

Algún miembro puede completar un "formulario" que describe:
* Bugs (errores).
* Nuevas funcionalidades.
* Tareas pendientes.
* Mejoras.
* Preguntas o discusiones.

<br>

- Existen para registrar, organizar y discutir trabajos o tareas pendientes dentro de un repositorio.
- Un Pull Request puede vincularse a un Issue mediante expresiones como `Fixes #12`, `Closes #12` o `Resolves #12` en la descripción del PR o en un commit.
- Cuando el Pull Request se mergea en la rama destino, el Issue #12 se cierra automáticamente.

<br>

```txt
Problema o idea
↓
Se crea un Issue
↓
Se discute
↓
Alguien trabaja en él
↓
Se hace un Pull Request
↓
Se mergea
↓
Se cierra el Issue
```

<br><br><br>

#### Qué suele tener un Issue

<br>

| Campo       | Para qué sirve             |
| ----------- | -------------------------- |
| Título      | Resumen corto              |
| Descripción | Explicación detallada      |
| Etiquetas   | Categorías                 |
| Assignees   | Personas responsables      |
| Comments    | Discusión                  |
| Milestone   | Versión o entrega asociada |

<br><br><br>

#### Etiquetas comunes

<br>

| Etiqueta           | Significado              |
| ------------------ | ------------------------ |
| `bug`              | Error                    |
| `feature`          | Nueva funcionalidad      |
| `enhancement`      | Mejora                   |
| `documentation`    | Documentación            |
| `help wanted`      | Se necesita ayuda        |
| `good first issue` | Ideal para principiantes |

<br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br><br>


