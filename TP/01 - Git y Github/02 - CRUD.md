
<br>

### Flujo completo

<br>

```text
Crear repositorio:
git init
↓
git status
↓
Crear rama y cambiarse a ella:
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
Si la branch está lista para mergear:
git switch main
↓
git merge feature/login
↓
git branch -d feature/login
↓
git status
```

<br>

- Ver cambios sin commitear: `git diff`
- Ver qué cambios que trajo el último commit + autor, fecha, mensaje: `git show HEAD`
- Ver autor, fecha, mensaje del último commit: `git log -1`
- Ver autor, fecha, mensaje de todos los commits: `git log`
- Ver diferencias entre ramas: `git diff rama1 rama2`

<br><br>

---

<br>

### Commits y mensajes atomicos

<br>

Que haya un commit por cambio específico. <br>
Tener en cuenta los prefijos y después poner el mensaje. <br>

Ejemplo: `git commit -m "fix: validación de contraseña corregida"`

<br>

| Prefijo     | Uso                        |
| ----------- | -------------------------- |
| `feat:`     | Nueva funcionalidad        |
| `fix:`      | Corrección de errores      |
| `docs:`     | Documentación              |
| `refactor:` | Reorganización de código   |
| `test:`     | Pruebas                    |
| `style:`    | Formato, espacios, linting |
| `chore:`    | Tareas de mantenimiento    |
| `perf:`     | Mejoras de rendimiento     |

<br><br>

---

<br>

### Nombres de ramas

<br>

Se recomienda usar nombres descriptivos. <br>
Ejemplos:

```text
feature/login
feature/navbar
fix/error-validacion
docs/readme
refactor/estructura
test/usuarios
```

<br>

| Prefijo   | Uso                      |
| --------- | ------------------------ |
| feature/  | Nueva funcionalidad      |
| fix/      | Corrección de errores    |
| docs/     | Documentación            |
| refactor/ | Reorganización de código |
| test/     | Pruebas                  |

<br><br><br>
