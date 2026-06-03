
### Table of Contents




---

## Trabajo en equipo con Git y GitHub

Cuando se trabaja en equipo, el flujo de Git sigue siendo prácticamente el mismo:

```text
modificar
↓
add
↓
commit
```

Sin embargo, aparecen nuevos conceptos y ciertas prácticas se vuelven más importantes:

* Origin: nombre del repositorio remoto que apunta al local
* git status
* Mantener la rama actualizada con `git pull`.
* Trabajar en ramas y no en main.
* Que los nombres de las ramas sean los sugeridos por las buenas prácticas.
* Cada integrante debe trabajar en su propia rama.
* La relevancia de los mensajes (que sean como los propuestos por las buenas prácticas) del commit aumenta.
* Después de cada commit, hay que subir los cambios a GitHub mediante `git push`.
* Las ramas se mergean mediante Pull Requests (PR).

---

## Pull Request (PR)

Qué es?
Es una solicitud para incorporar los cambios de una rama dentro de otra.

Cuándo se hace?
Cuando se cree que una rama está lista para unirse a (generalmente) main, se crea una Pull Request (PR).


Cómo se hace?

1. Ir al repositorio en GitHub

2. Seleccionar

```text
Pull Requests
↓
New Pull Request
```

3. Elegir cuál va a ser la base branch (rama destino, generalmente main) y la compare branch (rama a unir).

Ejemplo:
```text
Base: main
Compare: feature/login
```

4. Revisar los cambios

GitHub mostrará:

* Archivos modificados.
* Líneas agregadas.
* Líneas eliminadas.
* Commits incluidos.

5. Agregar datos pedidos como título, descripción, comentarios y confirmar con:

```text
Create Pull Request
```

## Revisión

6. Antes de mezclar las ramas, otros integrantes pueden revisar el código.

Pueden:

* Leer el código.
* Comentar líneas específicas.
* Sugerir cambios.
* Aprobar el Pull Request.
* Solicitar modificaciones.

---

## Merge de PR

7. Una vez revisado el Pull Request por los demás integrantes, se selecciona:

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

8. Después del merge GitHub suele mostrar:

```text
Pull Request merged successfully
↓
Delete branch
```

Esto elimina la rama en GitHub y hay que hacerlo.

9. Actualizar la copia local de main

```shell
git switch main
git pull
```

10. Eliminar la rama local porque ya no es necesaria (su contenido ya fue incorporado a `main`).

```shell
git branch -d feature/login
```

---

## Flujo normal

```text

```

## Flujo cuando se desea crear Pull Request

```text

```

## Flujo post Pull Request

```text

```
