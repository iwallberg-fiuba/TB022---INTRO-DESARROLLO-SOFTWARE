````markdown
# Instructivo - Git Basico

## 1. Configuracion inicial

```bash
git config --global user.name "Tu Nombre"   # define tu nombre para los commits (global en tu máquina)
git config --global user.email "tu.email@dominio.com"   # define tu email asociado a los commits
git config --list   # muestra toda la configuración actual de git
````

## 2. Crear o clonar un repositorio

### Crear uno nuevo

```bash
git init   # inicializa un repositorio vacío en la carpeta actual (crea .git)
```

### Clonar uno remoto

```bash
git clone git@github.com:usuario/repositorio.git   # descarga el repo remoto y crea una copia local
```

## 3. Ver estado

```bash
git status   # muestra el estado actual del repo
```

Usalo para ver:

* archivos sin rastrear (untracked),
* archivos modificados (modified),
* archivos en staging (listos para commit).

Staging area: es una zona intermedia donde seleccionás qué cambios querés incluir en el próximo commit.

Cuando hacés `git add`, los cambios pasan del working directory a la staging area.
Todavía no están guardados en el historial ni subidos a GitHub.

Recién cuando hacés `git commit`, esos cambios se guardan en tu repositorio local.
Y solo con `git push` llegan a GitHub.

Sirve para tener control fino sobre qué cambios entran en cada commit. Te permite:
- separar cambios distintos en commits diferentes,
- evitar incluir archivos o cambios que no están listos,
- revisar exactamente qué vas a guardar antes de hacer commit,
- mantener un historial más claro y organizado.

## 4. Agregar cambios

### Un archivo

```bash
git add archivo.txt   # mueve ese archivo al staging area
```

### Todo lo modificado

```bash
git add .   # agrega todos los cambios actuales al staging
```

## 5. Crear commit

```bash
git commit -m "Mensaje descriptivo"   # guarda un snapshot de los cambios en el historial (solo lo que está en staging)
```

## 6. Ver historial

```bash
git log   # muestra historial completo de commits
git log --graph --oneline   # versión resumida y visual del historial
```

## 7. Sincronizar con remoto

### Traer cambios

```bash
git pull   # trae cambios del remoto y los mezcla con tu rama actual
```

### Subir cambios

```bash
git push   # sube tus commits locales al repositorio remoto
```

## 8. Trabajar con ramas

### Crear y listar

```bash
git branch   # lista las ramas existentes
git branch mi-rama   # crea una nueva rama (no cambia a ella)
```

### Cambiar de rama

```bash
git checkout mi-rama   # cambia tu contexto de trabajo a esa rama
```

### Fusionar

```bash
git merge mi-rama   # trae los cambios de esa rama a la rama actual
```

## 9. Guardar trabajo temporalmente

git stash no es lo mismo que la staging area: es un mecanismo para guardar temporalmente cambios sin hacer commit y limpiar el working directory. Cuando ejecutás git stash, Git guarda tanto los cambios del working directory como los que estaban en staging, y deja tu proyecto limpio para que puedas cambiar de rama o trabajar en otra cosa. Luego podés ver esos cambios con git stash list y recuperarlos con git stash apply (sin borrarlos) o git stash pop (recuperándolos y eliminándolos del stash).

```bash
git stash   # guarda cambios sin commit y limpia el working directory
git stash list   # lista los stashes guardados
git stash apply   # reaplica el stash (lo mantiene en la lista)
git stash pop   # reaplica y elimina el stash
```

## 10. Restaurar cambios

### Sacar del staging

```bash
git restore --staged archivo.txt   # saca el archivo del staging (no pierde cambios)
```

### Volver a ultimo commit

```bash
git restore archivo.txt   # descarta cambios y vuelve al último commit
```

### Traer version de un commit puntual

```bash
git restore --source=<commit-id> archivo.txt   # trae la versión de ese archivo en un commit específico
```

## 11. Staging Area (concepto clave)

La staging area (o index) es una zona intermedia donde preparás qué cambios van a entrar en el próximo commit.

Flujo de estados:

```text
Working Directory → Staging Area → Repository
```

* Working Directory: donde editás archivos
* Staging Area: donde seleccionás qué cambios guardar
* Repository: historial de commits

Ejemplo:

```bash
# modificás un archivo
git status

# lo agregás a staging
git add archivo.txt

# lo guardás en el historial
git commit -m "cambio"
```

Importante:

* Solo lo que está en staging se guarda en el commit
* Podés tener cambios hechos pero no incluidos si no hiciste git add

## 12. Si aparece un merge conflict

## Contexto

Tenés dos ramas:

* main (principal)
* feature (tu rama de trabajo)

Objetivo: traer cambios de main a feature.

## Flujo correcto

### 1. Pararte en tu rama

```bash
git checkout feature   # te movés a la rama feature
```

Estás en: feature

### 2. Traer cambios de main

```bash
git pull origin main   # trae cambios de main desde el remoto (origin) y los mergea en feature
```

Seguís en: feature
Trae cambios de origin/main y los mezcla en feature. Pueden aparecer conflictos.

### 3. Resolver conflictos

En los archivos:

```text
<<<<<<< HEAD   # inicio de tu versión (feature)
codigo de feature
=======
codigo de main   # versión que viene de main
>>>>>>> main   # fin del conflicto
```

Elegís qué queda y eliminás las marcas.

### 4. Marcar como resuelto

```bash
git add .   # indicás que resolviste los conflictos
```

Seguís en: feature

### 5. Finalizar el merge

```bash
git commit -m "conflictos arreglados"   # crea el commit que cierra el merge
```

Seguís en: feature

### 6. Subir cambios

```bash
git push   # sube tu rama feature al remoto
```

Seguís en: feature

## Error común

```bash
git pull origin main
git checkout feature
git merge main
```

Problemas:

* orden incorrecto
* checkout debería ir primero
* pull ya hace merge

## Alternativa explícita

```bash
git checkout feature   # te posicionás en tu rama de trabajo
git fetch origin   # trae cambios del remoto pero NO los mezcla
git merge origin/main   # mezcla manualmente lo que trajiste con fetch
```

* `git checkout feature`: cambia la rama activa.
* `git fetch origin`: descarga cambios del remoto sin afectar tu código.
* `git merge origin/main`: integra esos cambios a tu rama actual.

## Resumen

* Siempre trabajás en feature
* Traés cambios de main
* Resolves conflictos si aparecen
* git add + git commit cierran el merge
* git push sube los cambios

---
Apunte de @milagrosarganin
# 👾 GitHub

## 🌿 Ramas
- Desde una rama se puede intercambiar cosas sin necesidad de pasar por el `main`.

### 💻 Comandos
- `git branch`: Veo la rama en la que estoy (con un `*`) y las que tengo.
- `git checkout <nombre_rama>`: Me muevo a la rama que quiero.
- `git checkout -b <nombre_rama>`: Me crea la rama si no está y me mueve a esa.
- `git merge <nombre_rama>`: Me traigo los cambios de la rama que pongo a la que estoy trabajando.
- `git pull`: Me traigo los cambios de la rama donde estoy trabajando.

#### 💡 Aclaración: 
> Si pongo `git pull` me traigo los cambios que hay en GitHub a mi local de la rama en la que estoy trabajando, pero si pongo `git merge <nombre_rama>` me traigo los cambios que hay en GitHub de esa rama que puse después de `merge`, a la rama que estoy trabajando en mi local.

### 🚀 Subir una rama
> Si no hice un `push` de la rama que creé, cuando la voy a pushear (después de agregar cambios) me va a saltar error, y me dice cómo la tengo que pushear. Lo hago y después subo los cambios.

---

## 🔄 Pull request (PR)

### ❓ ¿Qué son?
> Es una solicitud para integrar con un **MERGE** todos los cambios en una rama. El equipo puede ver los cambios que voy a mergear antes de hacerlo, funciona como un feedback del equipo.

### 🛠️ ¿Cómo se hacen?
> Debemos entrar al repositorio y donde nos aparecen los cambios recientes nos dice *"Compare & pull request"*. Entramos allí, comparamos las ramas y nos aparece la comparación. Ponemos un título y escribimos lo que creemos necesario. En la parte de *reviewers* selecciono quién/es quiero que vea/n lo que quiero mergear y ellos deciden si lo aprueban o no.

### ⚠️ ¿Qué pasa si no todos aprueban el PR?
> En ese caso, se activa la funcionalidad de pedir cambios y queda en rojo porque alguien lo rechazó. Entonces quien hizo el PR debe corregir el error. Siempre que un PR cumpla con la cantidad necesaria de *approves* (aprobaciones) para mergear, se podrá hacerlo.

#### 📝 Nota:
> Todos debemos trabajar de esta forma, con PR para evitar errores :)

---

## 🔀 Formas de usar ramas

### 1️⃣ Rama única:
- El método **menos recomendado**.

### 2️⃣ main, feature:
- **feature:** Cada vez que hacés una funcionalidad, hacés una rama nueva.

### 3️⃣ main, develop, feature *(más utilizada por desarrolladores)*:
- **main:** Cosas finalizadas.
- **develop:** Se ponen todos los próximos cambios que irán al `main`.
- **feature:** Lo ideal es que cada uno se haga su feature y luego eso se envíe a `develop`. Si está bien, se envía a `main` (que es donde se está desarrollando el juego o lo que fuese).

### 4️⃣ Gitflow *(main, develop, release, hotfix, feature)*:
- **release:** Se freeza (congela), no como `develop` que está en continuo cambio.
- **hotfix:** Una rama para cambios rápidos. Luego del cambio se vuelve a mergear con `main`.
- *(`main`, `develop` y `feature` son iguales que en el ítem anterior).*

#### 📝 Nota:
> Se hace mucho **hincapié** en esto en el TP final.

---

## 🍴 Fork 
> Es hacer una copia exacta de un repositorio en nuestra cuenta o computadora.

---

## 🔀 Merge
> Cuando una persona toca un archivo y no hacemos un `pull`, pero querés hacer un `merge` a tu rama, Git te dice que hay un **conflicto** y te hace elegir entre lo que estaba cambiado en GitHub y lo que vos querés poner. Podés elegir entre esas opciones u otra cosa distinta, pero tenés que decidir algo para resolver ese conflicto. Lo corregís, volvés a añadir los cambios y pusheás a GitHub. **Siempre se hace en equipo.**

---

## 💻 Más comandos

- `git restore <archivo.txt>`: Restaura el archivo a la versión del último commit.
- `git restore --staged <archivo.txt>`: Remueve el archivo del área de staging, pero mantiene los cambios locales.
- `git restore --source=<commit-id> <archivo.txt>`: Restaura el archivo a la versión del commit especificado sin modificar a los demás.