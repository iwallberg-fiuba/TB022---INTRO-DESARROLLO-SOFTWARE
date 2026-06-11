<br><br>

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
│  │  │  └─ tipos.js
│  │  │
│  │  └─ app.js
│  │
│  ├─ package.json
│  ├─ package-lock.json
│  └─ Dockerfile
│
├─ database/
│  ├─ schema.sql
│  └─ seeds.sql
│
├─ docker-compose.yml
├─ .gitignore
├─ .dockerignore
├─ .env
├─ License
└─ README.md
```

<br><br><br>

### Construir Dockerfiles

<br>

[La Clave](https://www.w3schools.com/tools/tool_dockerfile_generator.php)

<br>

#### Frontend
- nginx ("Engine X") y Alpine
- Comando?
- Puerto Expuesto?
- Working Directory?

<br><br>

#### Backend
- Node y Alpine
- Comando?
- Puerto Expuesto?
- Working Directory?

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

<br><br><br>

### Construir docker-compose

<br>

[La Clave](https://selqio.com/tools/docker-compose-generator)

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

### Construir Package

<br>

[La Clave](https://terrific.tools/code/package-json-generator)

<br>

- Incluir Start (para produccion), Dev (desarrollo)
- Dev dependencies: nodemon
- dependencies: dotenv, express, pg
- Scripts
  - "dev": nodemon directorioapp
  - "start": node directorioapp
- Incluir Type:Module
- Entrypoint: index.js

<br>

Entonces al hacer: 

```shell
npm install
npm run dev
```

<br>

ya queda todo perfectamente funcionando. 
Para producción `npm start` (si ya hiciste npm install y está actualizado).

<br><br>

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

<br><br><br><br>

### Construir env

<br>

[La Clave](https://www.w3schools.com/tools/tool_env_generator.php)

- Sección "Build from scratch"

<br><br><br>

### Construir gitignore

<br>

[LA Clave](https://www.w3schools.com/tools/tool_gitignore_generator.php)

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

