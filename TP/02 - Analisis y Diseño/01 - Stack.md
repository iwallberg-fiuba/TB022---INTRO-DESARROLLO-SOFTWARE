


### Análisis de requerimientos
Tener esto presente durante la lectura y seguimiento.

<br>

| Requerimientos | Información |
| --- | --- |
| Funcionales (`BREGAM`) | Definen **qué hace** el sistema. Suelen expresarse con verbos: **B**uscar, **R**egistrar, **E**nviar, **G**enerar, **A**ctualizar, **M**ostrar. |
| No Funcionales (`SEMECA`) | Definen **cómo debe funcionar** el sistema. Ejemplos: **S**eguro, **E**scalable, **M**antenible, **E**ficiente, **C**onfiable, **A**ccesible. |

<br><br>

1. Leer la Consigna del TP.

### Diseño

2. Pensar el posible Stack. No es necesario tener una idea clara sobre qué va a hacer el sitio web todavía, pero ya se puede pensar el Stack según la consigna y las herramientas vistas en clase. Lo único a tener en cuenta es que si se utilizan herramientas no vistas en clase, deben poder ser defendidas y justificadas en el oral.

```txt
Frontend?
├── HTML
├── CSS
└── JavaScript
```

```txt
Backend?
└──  JavaScript: Node.js
```
Node.js incluye npm, que incluye npx.

npm:

npx:

```txt
Base de datos
└── PostgreSQL + DBeaver
```

```txt
Herramientas Adicionales
├── Docker (con Docker compose, imagenes custom e imagenes oficiales)
├── Git
└── GitHub (con Github Actions tal vez?)
```


3. Revisar el Stack y perfeccionarlo.


Entonces, ahora el Stack del Frontend sería así:
```txt
Frontend
├── HTML
├── CSS
├── JavaScript
└── Nginx
```



Entonces, con npm o npx se pueden usar paquetes como:
- Express.js:
- nodemon:
- dotenv: archivo para poner variables de conexión, puertos, secretos, etc.
- linters.

En mi caso, usaría todos con npm a excepción de linters (si es que los termino utilizando).

Entonces, ahora el Stack del Backend sería algo así:

```txt
Backend
└── Node.js
    └── Packages
        ├── Express.js
        ├── nodemon
        └── dotenv
```

La base de datos queda igual.

```txt
Herramientas Adicionales
├── Docker
|   ├── imagenes
|   |     ├── Frontend (imagen custom -> Dockerfile)
|   |     ├── Backend (imagen custom -> otro Dockerfile más)
|   |     └── Base de datos (imagen oficial de PostgreSQL -> se declara en el docker-compose)     
|   |
|   └── docker-compose (para facilitar el build)
|       └── volumenes
|           ├── Para PostgreSQL
|           ├── Para inicializar la base de datos
|           └── Para los datos
|        
├── Git
└── GitHub (con Github Actions tal vez?)
```


Stack

```txt
Frontend
├── HTML
├── CSS
├── JavaScript
└── Nginx

Backend
└── Node.js
    └── Packages
        ├── Express.js
        ├── nodemon
        └── dotenv

Base de datos
└── PostgreSQL + DBeaver

Herramientas Adicionales
├── Docker
|   ├── .dockerignore (archivos y variables ignorados al crear imagenes)
|   ├── imagenes
|   |     ├── Frontend (imagen custom con Nginx -> Dockerfile)
|   |     ├── Backend (imagen custom con Node -> otro Dockerfile más)
|   |     └── Base de datos (imagen oficial de PostgreSQL -> se declara en el docker-compose)     
|   |
|   └── docker-compose (para facilitar el build)
|       └── volumenes
|           ├── Para PostgreSQL
|           ├── Para inicializar la base de datos
|           └── Para los datos
|        
├── Git
|   └── .gitignore (archivos y variables ignorados al subir el repo para proteger datos sensibles)
└── GitHub (con Github Actions tal vez?)
```

Con respecto a docker, esto:
```txt
Imágenes Oficiales
├── node
├── nginx
└── postgres

Imágenes Customs
├── frontend-image (FROM nginx)
└── backend-image (FROM node)
```

Resulta en los siguientes contenedores:

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


4. Pensar cómo se traduce esto en la estructura de los archivos. Sigue sin ser necesario saber exactamente qué va a hacer el sitio web.
