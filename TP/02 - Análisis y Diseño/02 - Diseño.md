

```txt
proyecto/
├── .git/                         
│
├── Frontend/
│   ├── Dockerfile                 # Imagen del Frontend
│   ├── index.html                 
│   ├── pagina2.html               
│   ├── pagina3.html               
│   ├── css/
│   │   └── styles.css             
│   └── js/
│       └── main.js                
│
├── Backend/
│   ├── Dockerfile                 # Imagen del Backend
|   ├── package.json               # Paquetes
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


### Construir docker-compose

### Construir dockerignore

[LA Clave](https://devtoollab.com/tools/dockerignore-generator)



### Construir Package

[LA Clave](https://www.w3schools.com/tools/tool_package_json.php)

- Incluir Start, Test, Build, Dev
- Incluir Type:Module
- Entrypoint: app.js

### Construir env

[LA Clave](https://www.w3schools.com/tools/tool_env_generator.php)

- Sección "Build from scratch"

### Construir gitignore

[LA Clave](https://www.w3schools.com/tools/tool_gitignore_generator.php)


### Construir seeds

[LA Clave](https://www.w3schools.com/tools/tool_data_generator.php)

### Construir README

[LA Clave](https://www.w3schools.com/tools/tool_github_readme.php)

### Construir Licencia

[LA Clave](https://www.w3schools.com/tools/tool_license_generator.php)
