
> **Idea:** Git se entiende mejor cuando lo pensas como una forma de construir historial con sentido, y GitHub como la capa social y remota que organiza colaboracion.

## Keywords a saber

`repositorio`, `commit`, `staging`, `branch`, `merge`, `conflictos`, `pull request`, `origin`, `clone`, `push`, `pull`, `.gitignore`, `remote`

> **Para estudiar:** si un termino te marea, ubicalo primero en `local`, `historial`, `rama` o `remoto`.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `repositorio` | Carpeta versionada donde Git guarda archivos e historial del proyecto. | No es solo una carpeta con codigo: tambien contiene memoria del proyecto, sus ramas y su evolucion. |
| `commit` | Instantanea con mensaje que registra un conjunto de cambios. | Conviene pensarlo como una unidad de significado, no como "guardar por guardar". |
| `staging` | Area intermedia donde elegis que cambios entran al proximo commit. | Es lo que hace a Git mas preciso que "guardar todo": te deja construir commits prolijos. |
| `branch` | Rama de trabajo paralela dentro del mismo repositorio. | Permite experimentar o desarrollar una parte sin ensuciar directamente la linea principal. |
| `merge` | Integracion de cambios de una rama dentro de otra. | El merge existe porque varias lineas de trabajo pueden convivir y despues reunirse. |
| `conflictos` | Choques entre cambios incompatibles que Git no puede unir solo. | No significan que Git "fallo", sino que encontro una decision que necesita criterio humano. |
| `pull request` | Pedido de revision e integracion de cambios en GitHub. | Es mas que un boton para unir ramas: funciona como espacio de discusion, control y revision. |
| `origin` | Nombre remoto por defecto del repositorio principal del que partiste. | No es una palabra magica; es simplemente una etiqueta convencional para un remoto. |
| `clone` | Copia local de un repositorio remoto. | Clonar no es bajar un zip: conserva historial, ramas y toda la estructura Git. |
| `push` | Envio de commits locales hacia un remoto. | Hace visible tu trabajo fuera de tu maquina. Hasta ese momento, tus commits siguen siendo locales. |
| `pull` | Descarga e integracion de cambios desde un remoto. | No solo baja informacion: normalmente tambien intenta integrarla a tu rama actual. |
| `.gitignore` | Archivo que lista que archivos no deben versionarse. | Sirve para separar codigo valioso de ruido tecnico como temporales, compilados o secretos locales. |
| `remote` | Conexion nombrada hacia otro repositorio, local o remoto. | Es la forma en que Git sabe con que otros repositorios puede intercambiar informacion. |

## Tabla comparativa rapida

| Concepto | Vive principalmente en | Funcion |
| --- | --- | --- |
| `Git` | tu maquina y el repo local | versionar cambios |
| `GitHub` | plataforma remota | compartir, revisar e integrar cambios |
| `pull request` | GitHub | coordinar revision antes del merge |

## Mapa mental rapido

La secuencia conceptual mas importante del tema es esta:

```text
trabajo en archivos
-> selecciono cambios con staging
-> los guardo en commits
-> los organizo en ramas
-> y los comparto o integro usando remotos y GitHub
```

Si esa cadena se entiende, Git deja de parecer una coleccion arbitraria de comandos.

## Lo que mas se suele confundir

- `Git` no es lo mismo que `GitHub`: uno es la herramienta de versionado y el otro es una plataforma que la usa.
- `commit` no es lo mismo que `push`: el commit guarda cambios en tu historial local, mientras que push los publica en un remoto.
- `branch` y `pull request` tampoco son equivalentes: la rama es una linea de trabajo y el PR es una instancia de revision e integracion en GitHub.

## Como leer este apunte

Este archivo conserva los temas del material largo original, pero los reordena para que se entiendan mejor al estudiar por primera vez.

La idea clave es separar:

- Git: herramienta de control de versiones;
- GitHub: plataforma que aloja repositorios Git y agrega colaboracion.

## 1. Idea general

Git permite registrar cambios en los archivos de un proyecto a lo largo del tiempo.

Eso resuelve varios problemas:

- saber que cambio;
- saber cuando cambio;
- saber quien cambio;
- volver a una version anterior si algo sale mal;
- trabajar en paralelo sin pisarse tanto.

GitHub usa Git, pero no es Git. GitHub agrega:

- repositorios remotos;
- colaboracion entre personas;
- pull requests;
- issues;
- integraciones y automatizacion.

## 2. Repositorio

Un repositorio es el lugar donde Git guarda:

- los archivos del proyecto;
- el historial de cambios;
- las referencias a ramas y commits.

### Repositorio local

Es el que esta en tu propia computadora.

Ahi podes:

- editar;
- hacer commits;
- crear ramas;
- revisar historial.

### Repositorio remoto

Es la copia alojada en un servidor o plataforma, por ejemplo GitHub.

Sirve para:

- compartir trabajo;
- subir cambios;
- bajar cambios de otras personas;
- tener una copia central del proyecto.

## 3. Versiones y commits

En Git, una version importante del proyecto suele quedar registrada como un commit.

Un commit es una instantanea del estado de los archivos en un momento dado.

Cada commit guarda:

- que cambios quedaron incluidos;
- un mensaje descriptivo;
- un identificador unico llamado hash.

### Por que importa el mensaje del commit

Un buen mensaje no solo dice "cambie cosas". Deberia dejar claro:

- que cambiaste;
- y, cuando hace falta, por que.

Ejemplos mejores:

```text
Agrega validacion de email en formulario
Corrige calculo de promedio en reporte mensual
```

Ejemplos peores:

```text
arreglos
cosas
update
```

## 4. Estados de un archivo en Git

Una de las ideas mas importantes del tema es que Git no trata a todos los archivos igual todo el tiempo.

### Untracked

Git todavia no sigue ese archivo.

### Tracked

Git ya conoce ese archivo porque entro antes al historial.

Un archivo tracked puede estar:

- `unmodified`: sin cambios desde el ultimo commit;
- `modified`: cambiado, pero no preparado para el proximo commit;
- `staged`: preparado para entrar en el proximo commit.

### Flujo mental

```text
creo o modifico archivo
-> git add
-> staged
-> git commit
-> queda guardado en el historial
```

## 5. Area de staging

La staging area es una zona intermedia entre "modifique algo" y "lo confirme en el historial".

Sirve para elegir exactamente que cambios van a entrar en el proximo commit.

Eso importa porque:

- no siempre queres commitear todo junto;
- a veces hay cambios de distinta naturaleza mezclados;
- separar bien los commits hace mas legible el historial.

## 6. Ramas

Una rama es una linea alternativa de trabajo dentro del mismo repositorio.

Permite:

- desarrollar una funcionalidad aparte;
- probar una idea;
- corregir un bug;
- sin tocar directamente la rama principal.

### Idea practica

En vez de trabajar siempre sobre `main`, se crea una rama para una tarea puntual.

Cuando esa tarea esta lista, se fusiona de nuevo.

## 7. Merge y conflictos

### Merge

`merge` es la operacion de fusionar cambios de una rama en otra.

### Merge conflict

Aparece cuando Git no puede decidir solo como combinar cambios incompatibles.

Eso suele pasar cuando:

- dos ramas tocaron la misma parte de un archivo;
- una rama borro algo que la otra modifico;
- o las versiones ya no encajan automaticamente.

Resolver un conflicto implica:

1. abrir el archivo;
2. decidir que version conservar o como combinarlas;
3. guardar el resultado;
4. hacer `git add`;
5. terminar la fusion con un commit.

## 8. GitHub, PRs e issues

### GitHub

Es una plataforma para alojar repositorios Git y trabajar colaborativamente.

### Issue

Es una unidad para registrar:

- bugs;
- tareas;
- mejoras;
- ideas o pedidos de funcionalidad.

### Pull Request

Un pull request es una solicitud para fusionar una rama en otra en el repositorio remoto.

No es solo "subir codigo". Tambien funciona como espacio para:

- revisar cambios;
- discutir decisiones;
- detectar errores;
- aprobar o pedir correcciones.

## 9. .gitignore

`.gitignore` define patrones de archivos o carpetas que Git debe ignorar.

Es util para no versionar:

- archivos temporales;
- compilados;
- caches;
- secretos;
- dependencias generadas;
- configuraciones locales.

Ejemplo:

```gitignore
node_modules/
.env
__pycache__/
dist/
```

## 10. Flujo de trabajo tipico

Un flujo minimo muy comun se ve asi:

```bash
git status
git add .
git commit -m "Mensaje claro"
git push origin nombre-rama
```

Lectura:

1. miras que cambio;
2. preparas lo que queres commitear;
3. creas el commit;
4. lo subis al remoto.

## 11. Comandos importantes

### Configuracion inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@dominio.com"
git config --list
```

### Crear o clonar repositorio

```bash
git init
git clone <url>
```

### Ver estado e historial

```bash
git status
git log
git log --oneline
git diff
git diff --staged
```

### Agregar y confirmar cambios

```bash
git add <archivo>
git add .
git commit -m "Mensaje"
git commit --amend
```

### Ramas

```bash
git branch
git branch nombre-rama
git checkout nombre-rama
git checkout -b nombre-rama
git merge nombre-rama
```

### Remotos

```bash
git remote add origin <url>
git push origin nombre-rama
git pull origin nombre-rama
```

### Restaurar o deshacer

```bash
git restore <archivo>
git restore --staged <archivo>
git reset <archivo>
git stash
git stash pop
```

## 12. Que conviene entender de verdad

Mas importante que memorizar todos los comandos es entender estas relaciones:

- working tree: donde editas archivos;
- staging area: donde preparas cambios;
- commit: donde quedan guardados;
- rama: linea de trabajo;
- remoto: copia compartida;
- PR: revision y fusion en GitHub.

## 13. Errores conceptuales comunes

### "Git y GitHub son lo mismo"

No. Git es la herramienta. GitHub es una plataforma que usa Git.

### "Commit y push son lo mismo"

No. `commit` guarda en tu repo local. `push` sube al remoto.

### "Si hago add ya esta guardado"

No. `add` solo prepara cambios para el commit.

### "Trabajar siempre en main esta bien"

Para cosas chicas puede pasar, pero en trabajo colaborativo suele ser mejor usar ramas.

## 14. Resumen final

Si tuvieras que quedarte con una idea por bloque:

- Git registra historia de cambios;
- un repo puede ser local o remoto;
- un commit guarda una instantanea;
- la staging area decide que entra al commit;
- las ramas permiten trabajar en paralelo;
- GitHub agrega colaboracion;
- los PRs sirven para revisar y fusionar;
- `.gitignore` evita versionar basura o secretos.


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