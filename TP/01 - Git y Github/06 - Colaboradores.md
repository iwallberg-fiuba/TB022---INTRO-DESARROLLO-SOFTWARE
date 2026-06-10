
<br><br>

### Table of Contents

<br>

Flujos
- [Crear Rama](#Crear-Rama)
- [General](#General)
- [Crear Pull Request](#Crear-Pull-Request)
- [Post Pull Request](#Post-Pull-Request)

<br>

---

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

<br><br><br><br>

---

<br>

### Entender




