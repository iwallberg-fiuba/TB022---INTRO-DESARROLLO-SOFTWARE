<br>

`Pending.`
- Completar si falta algo
- Poner aca también tema ramas
- Poner aca también tema PR
- Poner aca también tema issues
- Emprolijar

## Flujo Completo

<br>

### 1. Abrir
```txt
Abrir la IDE con el repositorio
Abrir Docker App (dejarla minimizada)
Abrir Terminal Bash ubicado en la carpeta del repositorio
Git Bash puede causar problemas al instalar dependencias: usar WSL, dualboot o VM.
```

<br><br>

### 2. Git y Github
```txt
Desde Bash ubicado:
↓
git status
↓
Si no estás en tu rama:
git switch nombre-rama-destino
↓
git pull
```

<br><br>

### 3. Docker 
```txt
Desde mismo Bash
↓
¿Es la primera vez que levantas estos contenedores?,
¿Modificaste archivos y/o dependencias como: Dockerfile, docker-compose, package.json?
├── Si ambas respuestas son no: docker compose up -d
└── Si alguna respuesta es sí: docker compose up --build -d
```

<br><br>

### 4. Abrir Herramientas Según Capa

<br>

A) Frontend
```txt
Abrir navegador
↓
Ej. de URL: http://localhost:8080
↓
Desarrollar en tu IDE mientras ves los cambios en tu navegador.
```

<br>

B) Backend/API

```bash
¿Vas a ejecutar el backend por primera vez?,
¿Borraste la carpeta node_modules?,
¿Hiciste git pull y alguien agregó dependencias nuevas?,
¿Cambió package.json o package-lock.json?
├── Si todas las respuestas son no: npm run dev
└── Si alguna respuesta es sí: npm install → npm run dev
```

```txt
Abrir navegador
↓
Ej. de URL: http://localhost:3000
↓
Desarrollar en tu IDE mientras ves los cambios en tu navegador.
```

<br>

C) Base de datos
```txt
Abrir DBeaver
↓
¿Es la primera conexión al contenedor de PostgreSQL?
├── Si no: Abrir conexión guardada y listo. 
└── Si sí: Crear nueva conexión → Completar datos.

↓
Desarrollar.
```

<br>

Ejemplo de datos:
```txt
Host: localhost
Port: 5432 
Database: nombre_de_db
User: postgres
Password: postgres
```

<br><br>

### 5. Git y Github

<br>

Recordar:
- 1 commit por cambio relevante
- Mensaje del commit: Prefijo + descripción del cambio hecho

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

<br>

```txt
Venis de modificar archivos
↓
Volves a Bash ubicado
↓
git status
↓
git add .
↓
git commit -m "prefijo: descripción del cambio"
↓
git push
```

<br><br>

### 6. Apagar Docker y contenedores (no borra nada)

<br>

```shell
docker compose down
```

<br><br>

### 7. Si se desea hacer...

<br>

Pull Request (PR para Merge) o Crear un Issue:
- Ver `01 - Git y Github` → `05 - Colaboradores.md`

<br><br><br>



