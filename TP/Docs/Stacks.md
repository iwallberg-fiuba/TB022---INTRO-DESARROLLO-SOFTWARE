
<br><br>

### Table of Contents

<br>

[Stacks](#stacks)
- [Sobre Docker](#sobre-docker)

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


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br>


