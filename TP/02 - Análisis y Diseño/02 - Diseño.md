<br><br>

`Pending.`
- tema make file


Considerando el ejemplo visto en clase, se puede pensar una estructura así:

<br>

```txt
proyecto/
│
├─ frontend/
│  ├─ index.html
│  ├─ pag2.html
│  ├─ pag3.html
│  │
│  ├─ css/
│  │  └─ styles.css
│  │
│  ├─ js/
│  │  └─ main.js
│  │
│  ├─ assets/
│  │  └─ images/
│  │
│  └─ Dockerfile
│
├─ backend/
│  ├─ src/
│  │  ├─ api/
│  │  │  ├─ pokemons.js
│  │  │  └─ tipos.js
│  │  │
│  │  ├─ db/
│  │  │  ├─ pool.js
│  │  │  ├─ pokemons.js
│  |  |  ├─ schema.sql (contiene init)
│  |  |  ├─ seeds.sql
│  │  │  └─ tipos.js
│  │  │
│  │  └─ app.js
│  │
│  ├─ package.json
│  ├─ package-lock.json
│  └─ Dockerfile
│
│
├─ data/
|  └─ Archivos reales de PostgreSQL (generados automáticamente)
|
├─ docker-compose.yml
├─ .gitignore
├─ .dockerignore
├─ .env
├─ License
└─ README.md
```

<br><br><br>


### Construir Package

<br>

[La Clave](https://terrific.tools/code/package-json-generator)

<br>

- Incluir Start (para produccion), Dev (desarrollo)
- Dev dependencies: nodemon
- dependencies: dotenv, express, pg
- Scripts
  - "dev": "nodemon src/app.js"
  - "start": "node src/app.js"
- Incluir Type:Module
- Entrypoint: index.js? no sé por qué puso ese

<br>

Entonces al hacer: 

```shell
npm install
npm run dev
```

<br>

ya queda todo perfectamente funcionando. 
Para producción `npm start` (si ya hiciste npm install y está actualizado).

<br>

#### Ejemplo visto en Clase

<br>

```json
{
  "name": "pokeapi",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^5.2.1",
    "pg": "^8.21.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.14"
  },
  "type": "module"
}
```

<br><br><br>

### Construir env

<br>

[La Clave](https://www.w3schools.com/tools/tool_env_generator.php)

- Sección "Build from scratch"
- Tener esto abierto mientras se crea el archivo docker-compose
- Tambien reabrir el archivo al desarrollar en pool.js o al intentar conectar con dbeaver 

<br>



<br><br><br>

### Construir Dockerfiles

<br>

#### Frontend

<br>

- Imagen base: nginx ("Engine X")
- El `/usr/share/nginx/html` de `COPY . /usr/share/nginx/html` es un path de ejemplo.

<br>

```txt
FROM nginx:latest

COPY . /usr/share/nginx/html

EXPOSE 80
```

<br><br>

#### Backend

<br>

Usar: [La Clave](https://www.w3schools.com/tools/tool_dockerfile_generator.php)

<br>

- Imagen base: node:22
- Working Directory: carpeta de trabajo dentro del contenedor donde se copiará el backend. Por convención suele utilizarse /app.
- Instalar dependencias: npm install
- Puerto expuesto: 3000 o dejar vacío
- Comando de inicio:

```txt
Comandos de inicio:
├─ Opción 1: `CMD ["node", "app.js"]`
| (o node index.js según el archivo principal)
|
└─ Opción 2: `CMD ["npm", "run", "dev"]`
```

<br>

#### Cómo lo dejaría yo

<br>

```txt
FROM node:22

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "run", "dev"]
```

<br>

##### Ejemplo visto en Clase

<br>

```txt
FROM node:22

WORKDIR /app

COPY ./app /app

RUN npm install

CMD ["node", "app.js"]
```

<br>

- El copy está diferente porque el profesor usó esta estructura:

<br>

```txt
backend/
├─ Dockerfile
└─ app/
   ├─ package.json
   ├─ index.js
   └─ ...
```

<br><br><br>

### Construir docker-compose

<br>

[La Clave](https://selqio.com/tools/docker-compose-generator)

<br>

#### Cómo lo haría yo

```yml
services:
  frontend:
    build: ./frontend
    ports:
      - "${FRONTEND_PORT}:80"
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "${BACKEND_PORT}:3000"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:18
    ports:
      - "${DB_PORT}:5432"
    env_file:
      - .env
    volumes:
      - ./data:/var/lib/postgresql/data
      - ./backend/src/db/schema.sql:/docker-entrypoint-initdb.d/01-schema.sql:ro
      - ./backend/src/db/seeds.sql:/docker-entrypoint-initdb.d/02-seeds.sql:ro
```

<br>

con dotenv quedando:

<br>

```txt
# frontend puerto
FRONTEND_PORT=80


# backend puerto
BACKEND_PORT=3000


# backend con db envs
DB_HOST: db
DB_PORT: 5432
DB_USER: postgres
DB_PASSWORD: postgres
DB_NAME: mi_app_db


# database con postgresql envs
POSTGRES_USER: postgres
POSTGRES_PASSWORD: postgres
POSTGRES_DB: mi_app_db
```

<br>

#### Ejemplo visto en Clase

<br>

```yml
services:
  pokeapi:
    build: . # Buildear el Dockerfile de esta carpeta (.)
    image: backend # Ponele "backend" de nombre a la imagen
    ports:
      - "8000:8000"
    environment:
      DB_HOST: "db"
      DB_PORT: "5432"
      DB_USER: "backend_user"
      DB_PASS: "password-super-secreta"
      DB_NAME: "pokemon_db"

  db:
    image: postgres:18
    environment:
      POSTGRES_USER: "backend_user"
      POSTGRES_PASSWORD: "password-super-secreta"
      POSTGRES_DB: "pokemon_db"
    volumes:
      - ./data:/var/lib/postgresql
      - ./app/db/schemas.sql:/docker-entrypoint-initdb.d/schemas.sql:ro
```

<br><br><br>

### Construir dockerignore

<br>

[La Clave](https://devtoollab.com/tools/dockerignore-generator)

<br>

#### Ejemplo visto en Clase

<br>

```txt
app/node_modules/
```

<br><br><br>



### Construir gitignore

<br>

[La Clave](https://www.w3schools.com/tools/tool_gitignore_generator.php)

Qué no se sube al repo github?
- Credenciales, claves privadas, secretos, variables de entorno (ubicadas en `.env` + cosas como `.env.*`).
- Datos reales o sensibles de la base de datos (en este caso no hay porque usamos seeds)
- Carpeta `node_modules` y archivos temporales, logs y cachés.

<br>

Que sí se puede subir?
- `package.json`
- `package-lock.json`
- `.gitignore`
- `.dockerignore`
- `docker-compose.yml`
- `Dockerfile`
- Scripts SQL de inicialización (`init.sql`, `seeds.sql`)
- Código fuente
- README

<br>

#### Ejemplo visto en Clase

<br>

```txt
node_modules/
data/
.env
```

<br><br><br>

### Construir seeds

<br>

[La Clave](https://www.w3schools.com/tools/tool_data_generator.php)

<br><br><br>

### Construir README

<br>

[La Clave](https://www.w3schools.com/tools/tool_github_readme.php)

<br><br><br>

### Construir Licencia

<br>

[La Clave](https://www.w3schools.com/tools/tool_license_generator.php)

<br><br><br>

