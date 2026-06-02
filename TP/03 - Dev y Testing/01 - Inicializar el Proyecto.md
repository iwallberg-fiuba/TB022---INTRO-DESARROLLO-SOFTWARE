
### Table of Contents



### Requerimientos Previos

1. Tener todo lo de git y github ya hecho y configurado
2. Tener todo lo de docker ya creado
3. Descargar e instalar Docker Desktop y DBeaver.

---

Flujo de Desarrollo

1. Abrir Docker Desktop y dejarlo minimizado (ya va a estar corriendo).
2. Abrir el repositorio del proyecto en la IDE.
3. Verificar en qué rama estás con  `git status` o `git branch`
  - Si no estás en la tuya, `git switch nombre-rama-destino`
4. Traer los cambios nuevos con `git pull`
5. Parado en la carpeta raíz del proyecto, abrir la terminal del sistema operativo y levantar los contenedores:
- Si es la primera vez: `docker compose up --build -d`
- Para el resto de veces: `docker compose up -d`
- Si modificaste Dockerfiles, docker-compose, o dependencias (package.json): `docker compose up --build -d`


6. Abrir las herramientas necesarias según en dónde vas a programar (Frontend, Backend/API, BdDs):

- Frontend: pegar http://localhost:8080 en el navegador

- Backend/API: pegar http://localhost:3000 en el navegador

- Bases de datos:
  1. Abrir DBeaver y:
  - Si no es la primera vez que te conectas: con doble click sobre la conexión guardada ya entras.
  - Si es la primera vez que te conectas:
    1. Crear nueva conexión (Dbeaver se conecta al contenedor PostgreSQL).
    2. Completar datos (suele ser esta info):

```txt
Host: localhost
Port: 5432
Database: mi_app_db
User: postgres
Password: postgres
```

7. Programar y hacer los cambios deseados en el código mientras ves los resultados actualizarse en tiempo real.
8. Revisar los archivos que fueron modificados con `git status`
9. Hacer commit

```shell
git add .
git commit -m "mensaje"
```

10. Hacer Push con `git push`

Nota: Si el trabajo de la rama ya está terminado y listo para incorporarse a main, crear un Pull Request en GitHub.
Revisar Doc sobre Flujo de Git y Github.

11. Apagar Docker y contenedores (no borra nada) `docker compose down`


12. Recordar seguir updateando el README del proyecto.


