
`Pending.`


```txt

```


```txt
proyecto/
├── .git/                         
│
├── Frontend/
│   ├── Dockerfile                 
│   ├── index.html                 
│   ├── pagina2.html               
│   ├── pagina3.html               
│   ├── css/
│   │   └── styles.css             
│   └── js/
│       └── main.js                
│
├── Backend/
│   ├── Dockerfile                 
|   ├── package.json               
│   └── src/                       
│   
├── database/                      
│   ├── init.sql                   
|   ├── schemas.sql
│   └── seeds.sql                  
│
├── docker-compose.yml             
├── .env                           
├── .dockerignore                  
├── .gitignore                     
├── README.md                      
└── LICENSE                        # Licencia del proyecto. No aplica en este caso.
```


### Construir Dockerfiles

[LA Clave](https://www.w3schools.com/tools/tool_dockerfile_generator.php)

#### Frontend
- nginx ("Engine X") y Alpine
- Comando?
- Puerto Expuesto?
- Working Directory?

#### Backend
- Node y Alpine
- Comando?
- Puerto Expuesto?
- Working Directory?

##### Ejemplo visto en Clase

```txt
FROM node:22

WORKDIR /app

COPY ./app /app

RUN npm install

CMD ["node", "app.js"]
```


### Construir docker-compose

[LA Clave](https://selqio.com/tools/docker-compose-generator)

#### Ejemplo visto en Clase

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


### Construir dockerignore

[LA Clave](https://devtoollab.com/tools/dockerignore-generator)

#### Ejemplo visto en Clase

```txt
app/node_modules/
```

### Construir Package

[LA Clave](https://www.w3schools.com/tools/tool_package_json.php)

- Incluir Start, Test, Build, Dev
- Incluir Type:Module
- Entrypoint: app.js

#### Ejemplo visto en Clase

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


### Construir env

[LA Clave](https://www.w3schools.com/tools/tool_env_generator.php)

- Sección "Build from scratch"

### Construir gitignore

[LA Clave](https://www.w3schools.com/tools/tool_gitignore_generator.php)

#### Ejemplo visto en Clase

```txt
node_modules/
data/
.env
```

### Construir seeds

[LA Clave](https://www.w3schools.com/tools/tool_data_generator.php)

### Construir README

[LA Clave](https://www.w3schools.com/tools/tool_github_readme.php)

### Construir Licencia

[LA Clave](https://www.w3schools.com/tools/tool_license_generator.php)
