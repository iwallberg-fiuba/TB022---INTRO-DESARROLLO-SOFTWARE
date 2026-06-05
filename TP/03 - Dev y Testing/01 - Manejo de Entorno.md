<br>

## Flujo Completo

<br>

### 1. Abrir
```txt
Abrir la IDE con el repositorio
Abrir Docker App (dejarla minimizada)
Abrir Terminal Git Bash ubicado en la carpeta del repositorio
```

<br><br>

### 2. Git y Github
```txt
Desde Git Bash ubicado:
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
Desde la misma Git Bash
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
Abrir tu navegador
↓
Ej. de URL: http://localhost:8080
↓
Desarrollar en tu IDE mientras ves los cambios en tu navegador.
```

<br>

B) Backend/API
```txt
Abrir tu navegador
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

Ejemplo de Datos:
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
Volves a tu Git Bash ubicado
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

### 6. Apagar Docker y contenedores (no borra nada) `docker compose down`

<br><br>

### 7. Si se desea hacer Pull Request...

<br>

```
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

### 8. Recordar seguir updateando el README del proyecto.

<br><br><br>

