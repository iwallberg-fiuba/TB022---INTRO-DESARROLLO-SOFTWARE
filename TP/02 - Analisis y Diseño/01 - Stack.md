### Diseño y Arquitectura

<br><br>

### Lo visto en clase

<br>

No es necesario tener una idea demasiado concreta del proyecto todavía, ya que la consigna pide un sitio web y las herramientas vistas en clase condicionan bastante el stack.

<br>

Lo importante es identificar qué herramientas se van a usar y recordar que, si se agregan tecnologías no vistas en clase, deben poder ser defendidas y justificadas en el oral.

<br>

#### 1. Stack y Arquitectura

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

<br>

```text
Frontend
    ↓ HTTP
Backend/API
    ↓ SQL
Base de datos
```

<br><br>

#### 2. Infraestructura con Docker

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

<br><br>

### Lo elegido

<br><br>

#### 1. Visualizar todo lo elegido

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

<br><br>

#### 2. Escribir el Stack oficial para el README

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

<br><br>

#### 3. Pensar la estructura de archivos

<br>

Finalmente, pensar cómo se traduce esta separación en carpetas y archivos.

<br>

Sigue sin ser necesario tener una idea completamente cerrada del proyecto.

<br>

La estructura de carpetas debería reflejar la arquitectura definida anteriormente, separando claramente frontend, backend, base de datos, configuración e infraestructura.

<br>

La consigna (+ instrucciones en clase) pedían:
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
