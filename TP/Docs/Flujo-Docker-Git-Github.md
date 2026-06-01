
Table of Contents

Conexión con docker
- Qué usar de docker
- Conexión con base de datos

DBeaver

etapa: desarrollo
- flujo para crear las cosas
- flujo para conectar las cosas
- flujo para cuando estas desarrollando sobre las estructuras ya conectadas y creadas

etapa: Testings
- flujo para crear testeos
- flujo para correr testeos

etapa: deployment
- flujo deployment

---

Requerimientos Previos

1. Tener todo lo de git y github ya hecho y configurado
2. Tener todo lo de docker ya creado

---

1. Abrir la app de Docker y dejarla minimizada.
2. Abrir el repo del proyecto en la IDE
3. Verificar en qué rama estás `git status` o `git branch`
4. Si estás en la que no es tuya, `git switch nombre-rama-destino`
5. Traer los cambios nuevos con `git pull`
6. Parado en la carpeta raíz del proyecto, abrir la terminal del sistema operativo y levantar los contenedores:
- Si es la primera vez que los levantas: `docker compose up --build -d`
- Para el resto de veces: `docker compose up -d`
- Si modificaste Dockerfiles: `docker compose up --build -d`
7. Abrir el navegador y pegar estos links (suelen ser así)
  Si vas a programar...
  - Frontend: http://localhost:8080
  - Backend/API: http://localhost:3000
  - Bases de datos con PostgreSQL desde DBeaver: localhost:5432
8. Programar y hacer los cambios deseados en el código mientras ves los resultados actualizarse en tiempo real en el navegador.
9. Revisar cambios en los archivos con `git status`
10. Hacer commit

```shell
git add .
git commit -m "mensaje"
```

11. Hacer Push con `git push`

Nota: Si la rama ya está terminada, es decir, no planeas editarla nunca más y ya puede mergearse con main, hacer Pull Request.
(En el archivo sobre el flujo de git y github está lo de cómo hacer pull request)

12. Apagar Docker y contenedores (no borra nada) `docker compose down`







