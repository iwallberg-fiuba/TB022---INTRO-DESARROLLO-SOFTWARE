


4. Pensar cómo se traduce esto en la estructura de los archivos. Sigue sin ser necesario saber exactamente qué va a hacer el sitio web.

```txt
proyecto/
├── .git/                         
│
├── frontend/
│   ├── Dockerfile                 # Imagen del Frontend
│   ├── index.html                 # (Puede estar vacío)
│   ├── pagina2.html               # (Puede estar vacío)
│   ├── pagina3.html               # (Puede estar vacío)
│   ├── css/
│   │   └── styles.css             # (Puede estar vacío)
│   └── js/
│       └── main.js                # (Puede estar vacío)
│
├── backend/
│   ├── Dockerfile                 # Imagen del Backend
│   └── src/                       # (Puede estar vacío)
│   
├── database/                      # (Puede estar vacío)
│   ├── init.sql                   # (Puede estar vacío)
│   └── seeds.sql                  # (Puede estar vacío)
│
├── docker-compose.yml             # Levanta todo
├── .env                           # (Puede estar vacío)
├── .dockerignore                  # (Puede estar vacío)
├── .gitignore                     # (Puede estar vacío)
├── README.md                      # (Puede estar vacío)
└── LICENSE                        # Licencia del proyecto. No aplica en este caso.
```

5. Pensar y revisar que la estructura cumpla los requerimientos.
6. Pensar qué podrían contener los `archivos de docker` (dockerfiles, docker-compose) para lograr que el proyecto cumpla los requerimientos.

- docker-compose
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


- Dockerfile (Frontend)

```txt
# Imagen oficial de Nginx
FROM nginx: # poner versión deseada

# Copia los archivos del frontend al lugar donde Nginx sirve sitios web
COPY . /usr/share/nginx/html

# Puerto interno donde escucha Nginx
EXPOSE 80
```

- Dockerfile (Backend)

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



7. Pensar qué podrían contener los `archivos de configuración` (env, dockerignore, gitignore)

- env
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

- gitignore
```txt
node_modules/      # Dependencias instaladas por npm
.env               # Contraseñas, API keys, etc.
*.log              # Logs
dist/              # Archivos compilados
build/             # Archivos compilados
.vscode/           # Configuración personal de VS Code
.idea/             # Configuración de IntelliJ/WebStorm
```

- dockerignore
```txt
node_modules/      # Se reinstalan dentro del contenedor
.git/              # Historial de Git innecesario
.gitignore
README.md
*.log
.env
```

