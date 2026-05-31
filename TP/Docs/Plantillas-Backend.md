
<br><br>

### Table of Contents

<br>

[TREE](#tree)

[Plantillas](#plantillas)
- [env](#env)
- [docker-compose](#docker-compose)
- [Dockerfile - Frontend](#dockerfile---frontend)
- [Dockerfile - Backend](#dockerfile---backend)
- [gitignore](#gitignore)
- [dockerignore](#dockerignore)

<br>

--- 

<br><br>

## TREE

<br>

```txt
proyecto/
├── .git/                         # Carpeta interna de Git
├── .github/
│   └── workflows/
│       └── ejemplo.yml            # Automatizaciones de GitHub Actions (opcional)
│
├── frontend/
│   ├── Dockerfile                 # Imagen del frontend
│   ├── nginx.conf                 # Configuración para servir HTML/CSS/JS
│   ├── index.html                 
│   ├── pagina2.html               
│   ├── pagina3.html               
│   ├── css/
│   │   └── styles.css             
│   └── js/
│       └── main.js                # JavaScript del Frontend.
│
├── backend/
│   ├── Dockerfile                 # Imagen del backend Node.js.
│   ├── package.json               # Dependencias y scripts npm.
│   ├── package-lock.json          # Versiones exactas de dependencias.
│   └── src/
│       ├── app.js                 # Configuración de Express.
│       ├── server.js              # Entrypoint
│       ├── routes/
│       │   └── users.routes.js    # Endpoints relacionados a usuarios.
│       ├── controllers/
│       │   └── users.controller.js   # "Lógica de negocio".
│       ├── models/
│       │   └── users.model.js     # Consultas a la base de datos.
│       └── db/
│           └── connection.js      # Conexión a PostgreSQL.
│   
│
├── database/
│   ├── init.sql                   # Script inicial de PostgreSQL.
│   └── seeds.sql                  # Datos de prueba.
│
├── docker-compose.yml             # Levanta frontend + backend + postgres.
├── .env                           # Variables de conexión, puertos, secretos, etc.
├── .dockerignore                  # Archivos ignorados al crear imágenes Docker.
├── .gitignore                     
├── README.md                      # Explicación del proyecto.
└── LICENSE                        # Licencia del proyecto. No aplica en este caso.
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Plantillas

<br>

### env

<br>

```txt
# PostgreSQL
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB= # nombre deseado de la base de datos

# Datos de la Base a la que intenta conectarse el Backend
DB_HOST=db
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME= # debe tener el mismo valor que POSTGRES_DB

# Puertos
POSTGRES_PORT=5432
BACKEND_PORT=3000
FRONTEND_PORT=8080
```

<br><br><br>

### docker-compose

<br>

```yml
services:

  # Frontend (HTML, CSS y JavaScript servido por Nginx)
  frontend:
    build: ./frontend
    container_name: # nombre-del-proyecto-frontend

    ports:
      # Permite acceder al sitio web desde el navegador.
      - "${FRONTEND_PORT}:80"

    depends_on:
      - backend

  backend:
    build: ./backend
    container_name: # nombre-del-proyecto-backend

    ports:
      # Permite acceder a la API desde herramientas externas como el navegador, Postman, Thunder Client, etc.
      - "${BACKEND_PORT}:3000"

    # Variables que recibirá el backend (están declaradas en el .env)
    environment:
      DB_HOST: ${DB_HOST}
      DB_PORT: ${DB_PORT}
      DB_USER: ${DB_USER}
      DB_PASSWORD: ${DB_PASSWORD}
      DB_NAME: ${DB_NAME}

    depends_on:
      - db

  # Base de datos PostgreSQL
  db:
    image: postgres: # poner versión deseada
    container_name: # nombre-del-proyecto-database

    # Variables utilizadas por PostgreSQL
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}

  ports:
    # Permite conectarse a PostgreSQL desde herramientas externas como DBeaver, pgAdmin, psql, etc.
    - "${POSTGRES_PORT}:5432"

    volumes:

      # Volumen persistente donde PostgreSQL almacena los datos
      - postgres_data:/var/lib/postgresql/data

      # Scripts SQL ejecutados automáticamente al crear la base por primera vez
      - ./database/init.sql:/docker-entrypoint-initdb.d/01-init.sql
      - ./database/seeds.sql:/docker-entrypoint-initdb.d/02-seeds.sql

volumes:

  postgres_data:
```

<br><br><br>

### Dockerfile - Frontend

<br>

```txt
# Imagen oficial de Nginx
FROM nginx: # poner versión deseada

# Copia los archivos del frontend al lugar donde Nginx sirve sitios web
COPY . /usr/share/nginx/html

# Puerto interno donde escucha Nginx
EXPOSE 80
```

<br><br><br>

### Dockerfile - Backend

<br>

```txt
# Imagen oficial de Node.js
FROM node: # poner versión deseada

# Carpeta de trabajo dentro del contenedor
WORKDIR /app

# Copia package.json y package-lock.json
COPY package*.json ./

# Instala dependencias
RUN npm install

# Copia el resto del código
COPY . .

# Puerto interno donde escucha Express
EXPOSE 3000

# Durante el desarrollo se suele usar nodemon para reiniciar
# automáticamente la aplicación al detectar cambios.
CMD ["npm", "run", "dev"]

# En producción (cuando ya se desplegó a los usuarios finales) normalmente se ejecuta el servidor directamente
# sin herramientas de desarrollo:
# CMD ["npm", "start"]
```

<br><br><br>

### gitignore
Aquellos archivos, carpetas, configuraciones, etc. que git no debe subir al repositorio. <br>

```txt
node_modules/      # Dependencias instaladas por npm
.env               # Contraseñas, API keys, etc.
*.log              # Logs
dist/              # Archivos compilados
build/             # Archivos compilados
.vscode/           # Configuración personal de VS Code
.idea/             # Configuración de IntelliJ/WebStorm
```

<br><br><br>

### dockerignore
Aquellos archivos y carpetas que Docker no debe copiar al construir una imagen. <br>
Es muy común que repita algunas de las cosas mencionadas en el `.gitignore`. <br>

```txt
node_modules/      # Se reinstalan dentro del contenedor
.git/              # Historial de Git innecesario
.gitignore
README.md
*.log
.env
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br>



