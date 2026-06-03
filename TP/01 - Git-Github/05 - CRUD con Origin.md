<br><br>

### Table of Contents

<br>

[Trabajo en equipo con Git y Github](#Trabajo-en-equipo-con-Git-y-Github)

<br>

- [Pull Request (PR)](#Pull-Request-PR)
 - [Revisión](#Revisión)
 - [Merge de PR](#Merge-de-PR)
 - [Limpieza Posterior](#Limpieza-Posterior)

<br>

- [Flujo general](#Flujo-general)
- [Flujo para Pull Request](#Flujo-para-Pull-Request)
- [Flujo post Pull Request](#Flujo-post-Pull-Request)


<br><br>

---

<br><br>

## Trabajo en equipo con Git y GitHub

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

<br>

---

<br>

### Flujo general

<br>

```text

```

<br><br>

### Flujo para Pull Request

<br>

```text

```

<br><br>

### Flujo post Pull Request

<br>

```text

```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>
