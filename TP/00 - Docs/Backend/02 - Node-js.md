
<br><br>

### Table of Contents

<br>

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
| Módulo | Archivo o conjunto de archivos que exportan funcionalidades reutilizables y pueden importarse desde otros archivos | `fs`, `path`, `./utils.js` |
| node_modules | Carpeta donde npm instala las dependencias y sus dependencias | `node_modules/express`, `node_modules/pg` |
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

- Archivo `package.json`: guarda las dependencias que necesita el proyecto y los rangos de versiones compatibles.
- Archivo `package-lock.json`: guarda las versiones exactas instaladas, incluyendo las dependencias de las dependencias, para garantizar instalaciones reproducibles.
- Carpeta `node_modules`: contiene todos los paquetes instalados que utiliza el proyecto.
- Es decir, `package.json` y `package-lock.json` solo describen qué instalar, pero no contienen el código de los paquetes.

<br>

```txt
Backend/
├─ package.json
├─ package-lock.json
├─ ...
└─ node_modules/
```

<br>

```txt
Paquete
↓
Se instala con npm
↓
Aparece en node_modules
↓
Sus módulos pueden importarse
```

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>





## Usar paquetes

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>




## Modules

<br>

Los módulos permiten dividir una aplicación en múltiples archivos reutilizables, evitando que todo el código quede en un único archivo.
Cada archivo puede exportar funcionalidades para que otros archivos las utilicen.

```txt
Aplicación
├─ app.js
├─ database.js
├─ routes.js
└─ utils.js
```

### Module Systems

Formas de importar y exportar código (paquetes o archivos). 
- JavaScript trae ES Modules.
- Node.js trae CommonJS.

```js
// ES Modules
import express from "express";
export default app;
```

```js
// CommonJS
const express = require("express");
module.exports = app;
```

<br>



<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>




