
<br><br>

### Table of Contents

<br>

[Stacks](#stacks)
- [Sobre Docker](#sobre-docker)

[TREE](#tree)

<br>

Agregar una sección sobre REST APIs?

<br>

--- 

<br><br>

## Stacks
Las tecnologías, lenguajes, etc. que se utilizan en el proyecto. <br>

Nota: pueden usarse otros siempre que se sepa defender y explicar su uso, tanto en el código como en el oral.

<br>

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

<br><br>

### Sobre Docker

<br>

```txt
Imágenes Oficiales
├── node
├── nginx
└── postgres

Imágenes Customs
├── frontend-image (FROM nginx)
└── backend-image (FROM node)
```

Que resulta en los siguientes contenedores:

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


<br>

[Volver a Table of Contents](#table-of-contents)

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

<br><br>


