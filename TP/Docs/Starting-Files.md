
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

<br><br>

### Requerimientos Previos

1. Tener todo lo de git y github ya hecho y configurado

<br>

Extra: [Imagenes Oficiales Disponibles para Docker](https://hub.docker.com/search?badges=official)

<br>

---

<br>

## TREE

<br>

Esta es la estructura que debe tener el repo. <br>
Crear las carpetas y archivos vacíos por ahora. <br>
Más adelante detallo qué contendrán los archivos docker y de entorno. <br>

```txt
proyecto/
├── .git/                         
│
├── frontend/
│   ├── Dockerfile                 # Imagen del frontend (explicada más adelante)
│   ├── index.html                 # (Puede estar vacío)
│   ├── pagina2.html               # (Puede estar vacío)
│   ├── pagina3.html               # (Puede estar vacío)
│   ├── css/
│   │   └── styles.css             # (Puede estar vacío)
│   └── js/
│       └── main.js                # (Puede estar vacío)
│
├── backend/
│   ├── Dockerfile                 # Imagen del backend Node.js. (explicada más adelante)
│   └── src/                       # (Puede estar vacío)
│   
│
├── database/                      # (Puede estar vacío)
│
├── docker-compose.yml             # Levanta frontend + backend + postgres. (explicada más adelante)
├── .env                           # Variables de conexión, puertos, secretos, etc. (explicada más adelante)
├── .dockerignore                  # Archivos ignorados al crear imágenes Docker. (explicada más adelante)
├── .gitignore                     # Archivos ignorados por git. (explicada más adelante)
├── README.md                      # Explicación del proyecto.
└── LICENSE                        # Licencia del proyecto. No aplica en este caso.
```

<br>

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


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

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

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>


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

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>


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

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>


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


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>


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



