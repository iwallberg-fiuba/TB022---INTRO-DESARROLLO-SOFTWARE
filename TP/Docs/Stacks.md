
<br><br>

### Table of Contents

<br>

[Stacks](#stacks)
- [Sobre Docker](#sobre-docker)
- [Sobre Node.js](#sobre-nodejs)

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

### Sobre Node.js

<br>

Node.js: Entorno de ejecución para JavaScript fuera del navegador. Se utiliza principalmente para desarrollar aplicaciones backend y APIs. Node.js incluye a npm.
- npm: Gestor de paquetes de Node.js. Permite instalar, actualizar y eliminar dependencias, así como ejecutar scripts definidos en package.json. npm incluye a npx.
  - npx: Ejecuta paquetes y herramientas de Node.js sin necesidad de instalarlos globalmente. Si el paquete ya existe en el proyecto, lo utiliza; si no, puede descargarlo temporalmente para ejecutarlo.

<br>

Instalar con... <br>
npm
- Express.js: Framework para crear servidores web y REST APIs HTTP.
- nodemon: Herramienta de desarrollo que reinicia automáticamente la aplicación al detectar cambios.
- dotenv: Librería para cargar variables de entorno desde un archivo .env.

<br>

npx
- Linters


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br>


