
### Stacks
Las tecnologías, lenguajes, etc. que se utilizan. <br>

```txt
Frontend
├── HTML
├── CSS
├── JavaScript
└── Nginx

Backend
└── Node.js ---> npm ---> npx 
               ├── Express.js
               ├── nodemon |
               └── dotenv  |
                           └── Linters

Database 
└── PostgreSQL

Infraestructura
├── Docker (con Docker compose, imagenes custom e imagenes oficiales)
├── Git
└── GitHub (con Github Actions tal vez?)
```


#### Sobre Docker y los Stacks
```txt
Imágenes Oficiales
├── node
├── nginx
└── postgres

Imágenes Customs
├── frontend-image (FROM nginx)
└── backend-image (FROM node)
```

<br>

Eso resulta en los siguientes contenedores:

<br>

```txt
Contenedores
│
├── frontend-container
│   └── frontend-image
│
├── backend-container
│   └── backend-image
│
└── database-container
    └── postgres:<version elegida>
```


<br><br><br>


### Sobre Node.js

Node.js: Entorno de ejecución para JavaScript fuera del navegador. Se utiliza principalmente para desarrollar aplicaciones backend y APIs. Node.js incluye a npm.
- npm: Gestor de paquetes de Node.js. Permite instalar, actualizar y eliminar dependencias, así como ejecutar scripts definidos en package.json. npm incluye a npx.
  - npx: Ejecuta paquetes y herramientas de Node.js sin necesidad de instalarlos globalmente. Si el paquete ya existe en el proyecto, lo utiliza; si no, puede descargarlo temporalmente para ejecutarlo.

  
En este caso, instalar con... <br>
npm
- Express.js: Framework para crear servidores web y APIs HTTP.
- nodemon: Herramienta de desarrollo que reinicia automáticamente la aplicación al detectar cambios.
- dotenv: Librería para cargar variables de entorno desde un archivo .env.

<br>

npx
- Linters

<br><br><br>

### Tree

<br>

```txt
proyecto/
├── .git/                         # Carpeta interna de Git
├── .github/
│   └── workflows/
│       └── ejemplo.yml                 # Automatizaciones de GitHub Actions
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
│       └── main.js                # JavaScript del Frontend
│
├── backend/
│   ├── Dockerfile                 # Imagen del backend Node.js
│   ├── package.json               # Dependencias y scripts npm
│   ├── package-lock.json          # Versiones exactas de dependencias
│   └── src/
│       ├── app.js                 # Configuración de Express
│       ├── server.js              # Punto de entrada
│       ├── routes/
│       │   └── users.routes.js    # Endpoints relacionados a usuarios
│       ├── controllers/
│       │   └── users.controller.js # Lógica de negocio
│       ├── models/
│       │   └── users.model.js     # Consultas a la base de datos
│       └── db/
│           └── connection.js      # Conexión a PostgreSQL
│   
│
├── database/
│   ├── init.sql                   # Script inicial de PostgreSQL
│   └── seeds.sql                  # Datos de prueba
│
├── docker-compose.yml             # Levanta frontend + backend + postgres
├── .env                           # Variables de conexión, puertos, secretos, etc.
├── .dockerignore                  # Archivos ignorados al crear imágenes Docker
├── .gitignore                     # Archivos ignorados por Git
├── README.md                      # Explicación del proyecto
└── LICENSE                        # Licencia del proyecto
```

<br><br><br>


#### Sobre `.env`

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


### Docker Estructuras de Archivos

#### Docker-compose.yml

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



#### Dockerfile (Frontend)

```txt
# Imagen oficial de Nginx
FROM nginx: # poner versión deseada

# Copia los archivos del frontend al lugar donde Nginx sirve sitios web
COPY . /usr/share/nginx/html

# Puerto interno donde escucha Nginx
EXPOSE 80
```



#### Dockerfile (Backend)

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


### Sobre los ignored

#### Plantilla `.gitignore`
Aquellos archivos, carpetas, configuraciones, etc. que git no debe subir al repositorio. <br>

Cómo se ve: <br>

```txt
node_modules/      # Dependencias instaladas por npm
.env               # Contraseñas, API keys, etc.
*.log              # Logs
dist/              # Archivos compilados
build/             # Archivos compilados
.vscode/           # Configuración personal de VS Code
.idea/             # Configuración de IntelliJ/WebStorm
```



#### Plantilla `.dockerignore`
Aquellos archivos y carpetas que Docker no debe copiar al construir una imagen. <br>
Es muy común que repita algunas de las cosas mencionadas en el `.gitignore`. <br>

Cómo se ve: <br>

```txt
node_modules/      # Se reinstalan dentro del contenedor
.git/              # Historial de Git innecesario
.gitignore
README.md
*.log
.env
```

<br>

