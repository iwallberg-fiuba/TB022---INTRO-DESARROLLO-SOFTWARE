
<br><br>

### Table of Contents

<br>

Bases
- [Conceptos Claves](#conceptos-claves)
- [Ejemplo Línea Temporal](#1-revisión-de-línea-temporal)
- [Git vs Github](#git-vs-github)
- [Ventajas de uso](#ventajas-de-uso)

<br>

Convenciones
- [Sobre Commits](#sobre-commits)
- [Sobre Branches](#sobre-branches)
- [Revisión Línea Temporal](#2-revisión-de-línea-temporal)
- [Errores Comunes](#errores-comunes)

<br>

Comandos
- [Lista](#lista)
- [Relación con Estados y Áreas](#relación-con-estados-y-áreas)
- [Cómo Deshacer Cambios](#cómo-deshacer-cambios)

<br>

Flujos de trabajo
- [Branches](#branches)
- [Merge Conflicts](#merge-conflicts)

<br>

[Extras](#extras)
- [Rebase vs Merge](#rebase-vs-merge)
- [Tags y Releases](#tags-y-releases)


<br>

---

<br>

## Bases

<br>

### Conceptos Claves

- Git: sistema de control de versiones que guarda snapshots/versiones del proyecto y permite rastrear, recuperar y organizar cambios a lo largo del tiempo.
- GitHub: plataforma que almacena repositorios remotos y facilita compartir código, colaborar, revisar cambios y sincronizar proyectos mediante Git.
- Repositorio: carpeta/proyecto gestionado por Git. Contiene archivos, historial de cambios, ramas y configuración de versionado. El historial y metadatos de Git se guardan dentro de la carpeta oculta `.git`.
- Repositorio remoto (`origin`): copia del repositorio alojada en otro lugar (GitHub, GitLab, servidor, etc.) usada para compartir y sincronizar cambios entre personas o dispositivos.
- `origin`: alias/nombre que Git asigna por defecto al repositorio remoto principal al hacer `git clone`. Permite referenciarlo más fácilmente en comandos como `git push origin main`.
- Branches/ramas: líneas de trabajo independientes que permiten desarrollar funcionalidades, corregir errores o experimentar en paralelo sin afectar directamente otras ramas.
- Línea temporal/historial: secuencia cronológica de commits y cambios realizados en el proyecto. Permite ver evolución, recuperar versiones anteriores y rastrear quién hizo cada cambio.
- Merge: proceso de combinar los cambios e historial de una rama dentro de otra para unificar líneas de trabajo.
- Merge conflicts: ocurren cuando Git no puede decidir automáticamente cómo combinar cambios incompatibles realizados sobre la misma parte de uno o más archivos. Ejemplo: dos personas modifican la misma línea de código de formas distintas.


<br><br>

### 1° Revisión de Línea Temporal

donde se siguieron las Convenciones sobre Branches (después de leer las Convenciones se entiende mejor)

<br>

<img width="800" height="400" alt="git-version-control" src="https://github.com/user-attachments/assets/aa6b93ca-356a-4b5d-8fa4-a2effc1d0ba0" />


<br><br><br>

### Git vs Github

| Git | GitHub |
| --- | --- |
| Sistema de control de versiones | Plataforma web |
| Funciona localmente | Hosting remoto |
| Maneja commits/ramas | Maneja PRs/releases |
| Usa `.git` | Usa remotos (`origin`) |
| No requiere internet | Generalmente sí |

<br><br><br>


### Ventajas de uso
de git y github.

| Acrónimo               | Qué representa                                                                 |
| ---------------------- | ------------------------------------------------------------------------------ |
| **H** = Historial      | Ver cambios pasados y recuperar versiones anteriores. “Historia” del proyecto. |
| **E** = Equipo         | Varias personas pueden trabajar juntas sobre el mismo proyecto.                |
| **R** = Ramas          | Permite probar cambios sin afectar `main`. Cada rama es un camino separado.    |
| **O** = Organización   | Los commits, Issues y Projects ayudan a mantener el proyecto ordenado.         |
| **S** = Sincronización | Compartir y respaldar cambios entre dispositivos/personas mediante GitHub.     |

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br>


---

<br>

## Convenciones
- Todas estas se vuelven realmente fundamentales en el trabajo en grupo.
- Algunas son por las buenas prácticas y otras por convenciones de la clase.

<br><br><br>

### Sobre Commits
- Deben ser atómicos, es decir, un commit = un único cambio lógico.
- El mensaje del commit debe ser descriptivo y representar claramente qué se modificó. Evitar mensajes genéricos como `update` o `mejora`.
- Es común usar prefijos para categorizar commits:
  - `feat`: agrega una funcionalidad. ej: `feat: login agregado`
  - `fix`: corrige errores/bugs. ej: `fix: validación corregida`
  - `docs`: cambios en documentación. ej: `docs: README actualizado`
  - `refactor`: reorganiza código sin cambiar comportamiento. ej: `refactor: lógica de autenticación simplificada`
  - `style`: cambios de formato/estilo
  - `test`: cambios relacionados con tests

<br><br><br>

### Sobre Branches
- Usar Merge en vez de Rebase.
- Usar checkout en vez de switch (por costumbre no porque sea mejor).
- No se trabaja directamente en main, cada uno trabaja en su propia rama y al final del desarrollo de cierta rama se hace merge con main.
- Hacer `pull` antes de empezar a trabajar.
- Hacer `pull` frecuentemente.
- Mantener ramas cortas.
- Evitar que muchas personas trabajen sobre el mismo archivo.
- Mergear cambios frecuentemente.
- usar los siguientes nombres:

<br><br>

| Tipos       | Qué significa                | Ejemplos del nombre completo de la rama |
| ---------- | ----------------------------- | -------------------- |
| `feature/` | Nueva funcionalidad           | `feature/login`      |
| `fix/`     | Corrección de errores         | `fix/navbar`         |
| `hotfix/`  | Arreglo urgente en producción | `hotfix/crash`       |
| `docs/`    | Cambios de documentación      | `docs/readme-update` |


<br><br><br>

### 2° Revisión de Línea Temporal

* donde se siguieron las Convenciones sobre Branches (ahora debería entenderse bastante más)

<img width="800" height="400" alt="git-version-control" src="https://github.com/user-attachments/assets/aa6b93ca-356a-4b5d-8fa4-a2effc1d0ba0" />

<br><br><br>

### Errores Comunes

| Error | Problema |
| --- | --- |
| Trabajar en `main` | Riesgo de romper producción |
| Commits gigantes | Difícil debuggear |
| No hacer pull seguido | Más merge conflicts |
| `git push --force` | Fuerza al remoto (origin) a aceptar tu historial local. Puede sobrescribir historial |
| `git reset --hard` | Mueve el repositorio a otro commit y descarta cambios locales. Puede borrar cambios |
| Commits ambiguos | Historial confuso |

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br>

---

<br>

## Comandos

<br>

### Lista
- Existen muchísimos más pero estos son los más utilizados y que hay que recordar.
- Dato: `git pull = git fetch + git merge`

<br>

<img width="1929" height="1151" alt="git" src="https://github.com/user-attachments/assets/f28c9da0-315c-4bc0-b641-bb7735fbcfec" />

<br><br><br>


### Relación con Estados y Áreas

| Estado del archivo                | Área: dónde está            | Cómo llega                                             |
| --------------------------------- | --------------------------- | ------------------------------------------------------ |
| `untracked`                       | Working Directory           | Archivo creado pero Git todavía no lo conoce.          |
| `staged`                          | Staging Area                | `git add` prepara cambios para el próximo commit.      |
| `tracked`                         | Repositorio local (Git)     | `git commit` guarda la snapshot en tu PC.              |
| `modified`                        | Working Directory           | Archivo tracked que fue modificado después del commit. |
| `pushed` *(no es estado oficial)* | Repositorio remoto (GitHub) | `git push` sube commits al remoto.                     |

<br><br><br>

### Cómo Deshacer Cambios

| Riesgo | Comando | Uso |
| --- | --- | --- |
| Bajo | `git reset archivo.txt` | Sacar archivo del stage |
| Medio | `git checkout -- archivo.txt` | Descartar cambios locales |
| Alto | `git reset --hard HEAD~1` | Volver commit atrás |

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br>

---

<br>

## Flujos de trabajo 

<br>

### Branches

```text
checkout main
↓
pull
↓
checkout -b feature/login
↓
trabajar
↓
add
↓
commit
↓
push
↓
Pull Request
↓
merge
```

<br><br><br>

### Merge Conflicts

| Paso | Acción |
| --- | --- |
| 1 | Ir a la rama que recibirá los cambios: `git checkout main` |
| 2 | Combinar otra rama dentro de la actual: `git merge feature/login` |
| 3 | Git detecta conflictos |
| 4 | `git status` para ver los archivos afectados |
| 5 | Editar los archivos manualmente |
| 6 | `git add archivo` |
| 7 | `git commit` |

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br>

---

<br>

## Extras
- No es necesario saberlo de memoria, con tener una noción en suficiente.

<br><br><br>

### Rebase vs Merge

| Tema | Merge | Rebase |
| --- | --- | --- |
| Qué hace | Une historiales | Reescribe historial |
| Historial | Mantiene bifurcaciones | Más lineal |
| Seguridad | Más seguro | Mucho más peligroso |
| Uso típico | Trabajo grupal | Limpiar historial |

<br>

Cómo se ve Merge:
```text
A---B---C main
     \
      D---E feature
           \
            M
```

<br>

Cómo se ve Rebase:
```text
A---B---C---D'---E'
```

<br><br><br>

### Tags y Releases
- Release: Versión publicada oficialmente. Nota: es de Github y se hace desde Github.
- Tag: Etiqueta fija sobre un commit 

<br>

| Acción | Comando |
| --- | --- |
| Crear tag | `git tag v1.0.0` |
| Ver tags | `git tag` |
| Subir tags | `git push origin --tags` |


<br>

[Volver a Table of Contents](#table-of-contents)

<br><br>






