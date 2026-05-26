


Definiciones bases

<img width="800" height="400" alt="git-version-control" src="https://github.com/user-attachments/assets/aa6b93ca-356a-4b5d-8fa4-a2effc1d0ba0" />


## Conceptos

- [ ] Git vs GitHub
- [ ] Repositorio local vs remoto
- [ ] Branches
- [ ] Commit atómico
- [ ] HEAD
- [ ] Merge vs Rebase
- [ ] Pull Request
- [ ] Tags y releases

## Comandos

- [ ] `git init`
- [ ] `git clone`
- [ ] `git status`
- [ ] `git add`
- [ ] `git commit`
- [ ] `git push`
- [ ] `git fetch`
- [ ] `git pull`
- [ ] `git merge`
- [ ] `git checkout`
- [ ] `git log`
- [ ] `git diff`
- [ ] `git reset`

## Flujos

- [ ] Crear rama
- [ ] Resolver merge conflict
- [ ] Hacer hotfix
- [ ] Crear tag/release
- [ ] Flujo grupal con ramas


---


# Git

## Orden recomendado para estudiar

```text
modelo mental
↓
estados de Git
↓
comandos esenciales
↓
ramas y remoto
↓
merge conflicts
↓
rebase vs merge
```

---

# 1. Modelo mental

```text
Git guarda snapshots del proyecto.
GitHub almacena una copia remota.
Las ramas permiten trabajar en paralelo.
```

---

# 2. Estados y áreas de Git

```text
untracked
↓ git add
staged
↓ git commit
tracked
↓ modificar
modified
```

```text
Working Directory
↓ add
Staging Area
↓ commit
Repositorio local (Git)
↓ push
Repositorio remoto (GitHub)
```

| Estado / área | Qué significa |
| --- | --- |
| `untracked` | Git todavía no sigue el archivo |
| `staged` | Archivo preparado para commit |
| `tracked` | Archivo ya versionado |
| `modified` | Archivo modificado después de un commit |
| Working Directory | Archivos modificados |
| Staging Area | Cambios preparados |
| Repo local | Historial local |
| Repo remoto | Copia subida a GitHub |

---

# 3. Git vs GitHub

| Git | GitHub |
| --- | --- |
| Sistema de control de versiones | Plataforma web |
| Funciona localmente | Hosting remoto |
| Maneja commits/ramas | Maneja PRs/releases |
| Usa `.git` | Usa remotos (`origin`) |
| No requiere internet | Generalmente sí |

---

# 4. Conceptos importantes

| Concepto | Idea rápida |
| --- | --- |
| Repositorio | Carpeta gestionada por Git |
| Branch / rama | Línea paralela de trabajo |
| Commit | Snapshot/checkpoint |
| Stage | Zona de preparación |
| HEAD | Dónde estás parado |
| Merge | Unión de ramas |
| Rebase | Reordenar historial |
| Pull Request | Pedido para integrar cambios |
| `.gitignore` | Archivos que Git ignora |

---

# 5. Ventajas de usar Git/GitHub

- Historial completo de cambios.
- Posibilidad de volver atrás.
- Trabajo colaborativo.
- Desarrollo paralelo con ramas.
- Backup remoto.
- Releases/versionado.
- Integración con CI/CD.

---

# 6. Comandos esenciales

| Acción | Comando |
| --- | --- |
| Inicializar repo | `git init` |
| Clonar repo | `git clone URL` |
| Ver estado | `git status` |
| Ver diferencias | `git diff` |
| Agregar cambios | `git add .` |
| Commit | `git commit -m "msg"` |
| Ver historial | `git log --oneline` |
| Ver ramas | `git branch` |
| Cambiar rama | `git checkout main` |
| Crear rama | `git checkout -b feature/x` |
| Ver remotos | `git remote -v` |
| Traer cambios | `git fetch origin` |
| Traer e integrar | `git pull origin main` |
| Subir cambios | `git push origin main` |
| Integrar ramas | `git merge rama` |
| Eliminar archivo | `git rm archivo.txt` |
| Renombrar archivo | `git mv viejo nuevo` |
| Guardar temporalmente | `git stash` |
| Recuperar stash | `git stash pop` |

Dato:
```text
git pull = git fetch + git merge
```

---

# 7. Volver atrás

| Riesgo | Comando | Uso |
| --- | --- | --- |
| Bajo | `git reset archivo.txt` | Sacar archivo del stage |
| Medio | `git checkout -- archivo.txt` | Descartar cambios locales |
| Alto | `git reset --hard HEAD~1` | Volver commit atrás |

---

# 8. Commits atómicos

```text
Un commit = un cambio lógico.
```

## Buenos ejemplos

```text
feat: agregar login
fix: corregir validación
docs: actualizar README
```

## Malos ejemplos

```text
cambios varios
update
arreglos
```

---

# 9. Ramas y workflow grupal

## Regla general

```text
Cada desarrollador trabaja en SU rama.
No trabajar directamente sobre main.
```

---

## Flujo típico

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

---

## Convenciones comunes

| Tipo | Ejemplo |
| --- | --- |
| Feature | `feature/login` |
| Fix | `fix/navbar` |
| Hotfix | `hotfix/crash` |
| Docs | `docs/readme-update` |

---

# 10. Merge conflicts

```text
Dos cambios incompatibles sobre la misma parte de un archivo.
```

| Paso | Acción |
| --- | --- |
| 1 | `git merge rama` |
| 2 | Git detecta conflicto |
| 3 | Editar archivo manualmente |
| 4 | `git add archivo` |
| 5 | `git commit` |

## Cómo evitarlos

- Pull frecuente.
- Ramas cortas.
- Commits pequeños.
- No trabajar todos sobre el mismo archivo.
- Mergear seguido.

---

# 11. Releases y Tags

| Concepto | Qué es |
| --- | --- |
| Release | Versión publicada oficialmente |
| Tag | Etiqueta fija sobre un commit |
| Hotfix | Arreglo urgente en producción |

| Acción | Comando |
| --- | --- |
| Crear tag | `git tag v1.0.0` |
| Ver tags | `git tag` |
| Subir tags | `git push origin --tags` |

Ejemplos:
```text
v1.0.0
v1.1.0
v2.0.0
```

---

# 12. Rebase vs Merge

| Tema | Merge | Rebase |
| --- | --- | --- |
| Qué hace | Une historiales | Reescribe historial |
| Historial | Mantiene bifurcaciones | Más lineal |
| Seguridad | Más seguro | Más delicado |
| Uso típico | Trabajo grupal | Limpiar historial |

---

## Merge

```text
A---B---C main
     \
      D---E feature
           \
            M
```

---

## Rebase

```text
A---B---C---D'---E'
```

Advertencia:
```text
No hacer rebase sobre ramas compartidas si no sabés bien qué estás haciendo.
```

---

# 13. Errores comunes

| Error | Problema |
| --- | --- |
| Trabajar en `main` | Riesgo de romper producción |
| Commits gigantes | Difícil debuggear |
| No hacer pull seguido | Más conflictos |
| `git push --force` | Puede sobrescribir historial |
| `git reset --hard` | Puede borrar cambios |
| Commits ambiguos | Historial confuso |





