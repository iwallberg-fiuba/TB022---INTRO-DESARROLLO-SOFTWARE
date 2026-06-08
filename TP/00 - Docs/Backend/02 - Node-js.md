
<br><br>

### Table of Contents

[Definiciones](#Definiciones)

[Paquetes TP](#Paquetes-TP)

[Instalar Paquetes](#Instalar-Paquetes)

[Usar Paquetes](#Usar-Paquetes)

[Modules](#Modules)

<br>

---

<br>

## Definiciones

<br>

- El runtime de JavaScript, Node.js, trae `npm` (que además trae `npx`).
- Gracias a `npm`, se pueden instalar paquetes y/o dependencias.
- Pueden servir para el Frontend, Backend, o la Base de datos.


<br><br>

| Concepto | Qué es | Ejemplo |
|-----------|-----------|-----------|
| Gestor de paquetes | Herramienta para instalar, actualizar y eliminar paquetes | `npm`, `pip`, `apt`, `cargo` |
| Ejecutor de paquetes | Ejecuta paquetes sin necesidad de instalarlos globalmente / que queden instalados con persistencia. | `npx` es parte de `npm` |
| Paquete | Unidad distribuible de código o herramientas que puede instalarse | `dotenv`, `nodemon`, `pg` |
| Dependencia | Paquete que un proyecto necesita para funcionar o desarrollarse | `express`, `pg`, `dotenv`, `nodemon` |
| Módulo | Archivo o conjunto de archivos que exportan funcionalidades reutilizables | `fs`, `path`, `./utils.js` |
| Librería (tipo de paquete) | Conjunto de funcionalidades que llamás desde tu código | React, jQuery, Lodash |
| Framework (tipo de paquete) | Estructura que organiza una aplicación y llama a tu código | Express, Next.js, Angular |
| Dev Tool (tipo de paquete) | Herramienta que ayuda durante el desarrollo, pero no forma parte de la lógica de la aplicación | `Nodemon`, `Vite`, `TypeScript`, `Webpack`, linters |


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>






## Paquetes TP

| Paquete | Función |
|----------|----------|
| **Express.js** (Framework) | Facilita la creación de servidores web y APIs que reciben solicitudes y envían respuestas. |
| **pg** (Librería) | Permite conectar aplicaciones Node.js con PostgreSQL y ejecutar consultas SQL. |
| **dotenv** (Librería) | Lee un archivo `.env` y carga sus valores como variables de entorno para que la aplicación pueda acceder a configuraciones como puertos, usuarios, contraseñas o claves de API. |
| **nodemon** (Dev Tool) | Reinicia automáticamente la aplicación al detectar cambios en los archivos durante el desarrollo. |


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>





## Instalar Paquetes

<br>

```bash
npm install express pg dotenv
npm install --save-dev nodemon
```

<br>

- `--save-dev` (o `-D`) guarda las dependencias como `devDependencies` en `package.json`.
- Se utiliza para herramientas de desarrollo que no son necesarias para ejecutar la aplicación en producción.

<br>

Al instalar paquetes, npm crea o actualiza (si ya existe):

<br>

- `package.json`: guarda las dependencias que necesita el proyecto y los rangos de versiones compatibles.
- `package-lock.json`: guarda las versiones exactas instaladas, incluyendo las dependencias de las dependencias, para garantizar instalaciones reproducibles.


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>





## Usar paquetes

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>




## Modules

<br>

modulos: imports, exports, requires


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>




