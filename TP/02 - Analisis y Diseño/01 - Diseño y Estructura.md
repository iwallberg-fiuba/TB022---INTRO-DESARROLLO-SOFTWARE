
<br><br>

### Table of Contents

<br>

[Visto en clase](#Visto-en-clase)
- [Stacks](#1--Stacks)
- [Infraestructura con Docker](#2--Infraestructura-con-Docker)
- [Conexiones](#3--Conexiones)
 
<br>

[Lo elegido](#Lo-elegido)
- [Visualizarlo](#1--Visualizarlo)
- [El Stack para el README](#2--El-Stack-para-el-README)
- [Arquitectura de Archivos](#3--Arquitectura-de-Archivos)
- [docker-compose](#4--docker-compose)
- [Dockerfile del Frontend](#5--Dockerfile-del-Frontend)
- [Dockerfile del Backend](#6--Dockerfile-del-Backend)
- [env](#7--env)
- [dockerignore](#8--dockerignore)
- [gitignore](#9--gitignore)
- [schemas](#10--schemas)
- [init](#11--init)
- [seeds](#12--seeds)


<br><br>

---

<br>

## Visto en clase

<br>

No es necesario tener una idea demasiado concreta del proyecto todavía, ya que la consigna pide un sitio web y las herramientas vistas en clase condicionan bastante el stack.

<br>

Lo importante es identificar qué herramientas se van a usar y recordar que, si se agregan tecnologías no vistas en clase, deben poder ser defendidas y justificadas en el oral.

<br><br><br>

### 1. Stacks

<br>

```text
Frontend
├── HTML
├── CSS
└── JavaScript

Backend
├── Node.js
└── Express.js

Base de datos
└── PostgreSQL

Infraestructura
├── Docker
└── Bash

Control de versiones
├── Git
└── GitHub

Package management
├── npm
└── npx

Packages
├── Express.js
└── nodemon

Herramientas extra
├── DBeaver
└── Postman / Thunder Client
```

<br><br><br>

### 2. Infraestructura con Docker

<br>

```text
Imágenes oficiales
├── node
└── postgres

Imágenes personalizadas
├── frontend-image
└── backend-image
    └── FROM node

Servicios en docker-compose.yml
├── frontend
├── backend
└── database

Contenedores
├── frontend-container
│   └── frontend-image
├── backend-container
│   └── backend-image
└── database-container
    └── postgres:<version-elegida>

Volúmenes
└── postgres_data
    └── Persistencia de datos de PostgreSQL

.dockerignore
└── Archivos ignorados al construir imágenes
```

<br><br><br>

### 3. Conexiones

<br>

```text
Frontend
    ↓ HTTP
Backend/API
    ↓ SQL
Base de datos
```

<br><br>

[Volver a la Table of Contents](#Table-of-Contents)

<br>

---

<br>

## Lo elegido

<br><br>

### 1. Visualizarlo

<br>

```text
Frontend
├── HTML
├── CSS
└── JavaScript
│
│ HTTP
▼
Backend
├── Node.js
├── Express.js
├── nodemon
└── dotenv
│
│ SQL
▼
PostgreSQL

Infraestructura
└── Docker
    ├── .dockerignore
    ├── Dockerfile frontend
    │   └── Imagen personalizada
    ├── Dockerfile backend
    │   └── Imagen personalizada
    ├── docker-compose.yml
    │   └── Orquesta los servicios
    │       ├── frontend
    │       ├── backend
    │       └── database
    └── Volúmenes
        └── postgres_data
            └── Persistencia de PostgreSQL


Control de versiones
├── Git
│   └── .gitignore
└── GitHub

Package management
├── npm
└── npx

Herramientas extra
├── DBeaver
└── Postman / Thunder Client
```

<br><br><br>

### 2. El Stack para el README

<br>

```text
Frontend
├── HTML
├── CSS
└── JavaScript

Backend
└── Node.js + Express.js

Base de datos
└── PostgreSQL

Infraestructura
└── Docker
```

<br><br><br>

### 3. Arquitectura de Archivos

<br>

Finalmente, pensar cómo se traduce esta separación en carpetas y archivos.

<br>

Sigue sin ser necesario tener una idea completamente cerrada del proyecto.

<br>

La estructura de carpetas debería reflejar la arquitectura definida anteriormente, separando claramente frontend, backend, base de datos, configuración e infraestructura.

<br>

La consigna (+ instrucciones en clase) pedían:

<br>

- 3 páginas HTML
- 3 contenedores (Frontend, Backend, database)
- Schemas.sql: archivo con la información sobre cómo crear las tablas para la base de datos
- Readme
- Uso de git y github
- Uso de los .ignore

<br>

```txt
proyecto/
├── .git/                         
│
├── frontend/
│   ├── Dockerfile                 # Imagen del Frontend
│   ├── index.html                 
│   ├── pagina2.html               
│   ├── pagina3.html               
│   ├── css/
│   │   └── styles.css             
│   └── js/
│       └── main.js                
│
├── backend/
│   ├── Dockerfile                 # Imagen del Backend
│   └── src/                       
│   
├── database/                      
│   ├── init.sql                   
|   ├── schemas.sql
│   └── seeds.sql                  
│
├── docker-compose.yml             # Levanta todo, define Postgres para database + persistencias
├── .env                           
├── .dockerignore                  
├── .gitignore                     
├── README.md                      
└── LICENSE                        # Licencia del proyecto. No aplica en este caso.
```

<br><br><br>

### 4. docker-compose

<br>

Archivo de Docker que funciona como la herramienta para definir y levantar varios contenedores a la vez. <br>
Puede definir: Servicios, Puertos, Volúmenes, Variables de entorno, Dependencias, Redes.

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

### 5. Dockerfile del Frontend

<br>

Archivo de Docker que contiene las instrucciones para construir la imagen del Frontend.

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

### 6. Dockerfile del Backend

<br>

Archivo de Docker que contiene las instrucciones para construir la imagen del Backend.

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

### 7. env

<br>

Secretos que se deben ignorar (como puertos, claves, etc).

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

### 8. dockerignore

<br>

Variables, archivos y carpetas que deben ignorarse al levantarse los contenedores

<br>

```txt
node_modules/      # Se reinstalan dentro del contenedor
.git/              # Historial de Git innecesario
.gitignore
README.md
*.log
.env
```

<br><br><br>

### 9. gitignore

<br>

Variables, archivos y carpetas que git debe ignorar.

<br>

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

### 10. Schemas

<br>

Archivo sql que describe el esquema para recrear las tablas para la base de datos.

<br>

```sql
CREATE TABLE usuarios ( ...
); ...
```

<br><br><br>

### 11. Init

<br>

Archivo sql que inicializa la base de datos.

<br>

```sql
CREATE DATABASE proyecto_db;

CREATE TABLE usuarios ( ...
); ...
```

<br><br><br>

### 12. seeds

<br>

Archivo sql que contiene datos de prueba. Datos falsos que representarían los futuros usuarios. <br>
Este archivo sí puede subirse al repositorio sólo porque son datos falsos.

<br>

```sql
INSERT INTO usuarios (nombre, email)
VALUES
('Juan Pérez', 'juan@email.com'),
('María Gómez', 'maria@email.com'),
('Pedro López', 'pedro@email.com');
```

<br><br><br>

[Volver a la Table of Contents](#Table-of-Contents)

<br><br>





