<br>

Falta emprolijar

## Flujo Completo


1. Abrir

```txt
Abrir la IDE con el repositorio
Abrir Docker App (dejarla minimizada)
Abrir Terminal Git Bash ubicado en la carpeta del repositorio
```

2. Git y Github
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

2. Docker 

```txt
Desde la misma Git Bash
↓
¿Es la primera vez que levantas estos contenedores?,
¿Modificaste archivos y/o dependencias como: Dockerfile, docker-compose, package.json?
├── Si ambas respuestas son no: docker compose up -d
└── Si alguna respuesta es sí: docker compose up --build -d
```

3. Abrir Herramientas Según Capa

Frontend
```txt
Abrir tu navegador
↓
Ej. de URL: http://localhost:8080
↓
Desarrollar en tu IDE mientras ves los cambios en tu navegador.
```
Backend/API
```txt
Abrir tu navegador
↓
Ej. de URL: http://localhost:3000
↓
Desarrollar en tu IDE mientras ves los cambios en tu navegador.
```


Base de datos
```txt
Abrir DBeaver
↓
¿Es la primera conexión al contenedor de PostgreSQL?
├── Si no: Abrir conexión guardada y listo. 
└── Si sí: Crear nueva conexión → Completar datos.

↓
Desarrollar.
```

Ejemplo de Datos:
Host: localhost
Port: 5432 
Database: nombre_de_db
User: postgres
Password: postgres

4. Git y Github (cerrar)

<br>
Recordar antes:
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

<br><br>

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

5. Apagar Docker y contenedores (no borra nada) `docker compose down`

6. Si se desea hacer Pull Request...

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

<br>

7. Recordar seguir updateando el README del proyecto.

<br><br>

