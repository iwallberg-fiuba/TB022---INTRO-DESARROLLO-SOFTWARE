<br><br>

### Table of Contents

<br>

[Colaborar usando Git y Github](#Colaborar-usando-Git-y-Github)

<br>

- [Flujo Crear Rama](#Flujo-Crear-Rama)
- [Flujo General](#Flujo-general)
- [Flujo para Pull Request](#Flujo-para-Pull-Request)
- [Flujo post PR Exitoso](#Flujo-post-PR-Exitoso)
- [Flujo post PR Exitoso](#Flujo-post-PR-Problema)

<br>

- [Explicado](#Explicado)
- [Pull Request (PR)](#Pull-Request-PR)
 - [Revisión](#Revisión)
 - [Merge de PR](#Merge-de-PR)
 - [Limpieza Posterior](#Limpieza-Posterior)

<br>

[Extra](#Extra)
- [Merge Conflicts](#Merge-Conflicts)
- [Issues](#Issues)

<br><br>

---

<br><br>

## Colaborar usando Git y GitHub

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

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

### Flujo Crear Rama

<br>

Cuando la rama en la que tenes que trabajar no existe todavía:

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

<br><br>

### Flujo General

<br>

Cuando la rama en la que tenes que trabajar ya existe:

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

<br><br>

### Flujo para Pull Request

<br>

Cuando consideras lista la rama:

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
Elegir base y compare branch
↓
Completar datos
↓
Seleccionar "Create Pull Request"
↓
Esperar la revisión de los demás junto con la Merge del PR
```

<br><br>

### Flujo post PR Exitoso

<br>

Siempre hacerlo después de un Pull Request que termina siendo aprobado (y por ende se transforma en Merge del PR).

<br>

```text
Estás esperando que termine la revisión del Merge del PR
↓
Si aprobada, Github hace el Merge del PR y avisa "Pull Request merged successfully"
↓
Seleccionar "Delete branch"
↓
Volver al repo local
↓
git switch main
↓
git pull
↓
git branch -d feature/login
↓
git status
```


<br><br>

### Flujo post PR Problema

<br>


```txt
Pull Request
↓
GitHub intenta hacer el merge
↓
¿Hay conflictos?
├─ No → Merge Pull Request
└─ Sí
    ↓
    GitHub bloquea el merge
    ↓
    git pull
    ↓
    Resolver conflictos manualmente
    ↓
    git add .
    ↓
    git commit
    ↓
    git push
    ↓
    GitHub verifica nuevamente
    ↓
    Se habilita Merge Pull Request
```


<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

---

<br>

## Explicado

<br><br>

### Pull Request (PR)

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

<br><br>

<br>

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

<br><br>

<br>

### Merge de PR

<br>

7. Una vez revisado el Pull Request por los demás integrantes, se selecciona:

<br>

```text
Merge Pull Request
```

<br>

GitHub combinará ambas ramas.

<br>

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

<br>

Ahora los cambios ya forman parte de `main` en GitHub.

<br>
<br>
<br>

### Limpieza posterior

<br>

8. Después del merge GitHub suele mostrar:

<br>

```text
Pull Request merged successfully
↓
Delete branch
```

<br>

Esto elimina la rama en GitHub y hay que hacerlo.

<br><br>

9. Actualizar la copia local de main

<br>

```shell
git switch main
git pull
```

<br><br>

10. Eliminar la rama local porque ya no es necesaria (su contenido ya fue incorporado a `main`).

<br>

```shell
git branch -d feature/login
```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

---

<br>

## Extra

<br><br>

### Merge Conflicts

<br>

| Paso | Acción                                                                           |
| ---- | -------------------------------------------------------------------------------- |
| 1    | Se crea un Pull Request                                                          |
| 2    | GitHub intenta combinar la rama origen con la rama destino                       |
| 3    | GitHub verifica si existen conflictos                                            |
| 4    | GitHub detecta que ambas ramas modificaron líneas incompatibles                  |
| 5    | GitHub informa que no es posible realizar el merge hasta resolver los conflictos |
| 6    | Se actualiza la rama local con los cambios más recientes de la rama destino      |
| 7    | Se ejecuta `git status` para identificar los archivos con conflictos             |
| 8    | Se editan manualmente los archivos y se resuelven los conflictos                 |
| 9    | Se ejecuta `git add .`                                                           |
| 10   | Se ejecuta `git commit -m "resolver conflictos"`                                 |
| 11   | Se ejecuta `git push`                                                            |
| 12   | GitHub vuelve a verificar el Pull Request                                        |
| 13   | Si ya no existen conflictos, GitHub habilita la opción de realizar el merge      |
| 14   | Se realiza manualmente el merge mediante el botón Merge Pull Request             |

<br><br><br>

### Issues

<br>

Algún miembro puede completar un "formulario" que describe:

<br>

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

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>
