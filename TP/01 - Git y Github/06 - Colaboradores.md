
<br><br>

### Table of Contents

<br>

- [Flujo Crear Rama](#Flujo-Crear-Rama)
- [Flujo General](#Flujo-general)
- [Flujo para Pull Request](#Flujo-para-Pull-Request)
- [Flujo post PR Exitoso](#Flujo-post-PR-Exitoso)
- [Flujo post PR Problema](#Flujo-post-PR-Problema)

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
