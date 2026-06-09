
<br><br>

### Table of Contents

<br>

`Pending`
Del package `pg`:
- Pool
- Client
- Pool local y pool postgres -> usar variables de entorno

<br>

[Definiciones](#Definiciones)

[Paquetes TP](#Paquetes-TP)

[Instalar Paquetes](#Instalar-Paquetes)

[Modules](#Modules)
- [Module Systems](#Module-Systems)
- [Importante](#Importante)

[Usar Paquetes TP](#Usar-Paquetes-TP)
- [pg y dotenv](#pg-y-dotenv)
- [Express](#Express)
- [nodemon](#nodemon)

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

<br><br>

---

<br>

## Paquetes TP

<br><br>

| Paquete | Función |
|----------|----------|
| **Express.js** (Framework) | Facilita la creación de servidores web y APIs que reciben solicitudes y envían respuestas. |
| **pg** (Librería) | Permite conectar aplicaciones Node.js con PostgreSQL y ejecutar consultas SQL. |
| **dotenv** (Librería) | Lee un archivo `.env` y carga sus valores como variables de entorno para que la aplicación pueda acceder a configuraciones como puertos, usuarios, contraseñas o claves de API. |
| **nodemon** (Dev Tool) | Reinicia automáticamente la aplicación al detectar cambios en los archivos durante el desarrollo. |


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

---

<br>

## Instalar Paquetes TP

<br>

```bash
npm install express pg dotenv
npm install --save-dev nodemon
```

<br>

- `--save-dev` (o `-D`) guarda las dependencias como `devDependencies` en `package.json`.
- Se utiliza para herramientas de desarrollo que no son necesarias para ejecutar la aplicación en producción.

<br><br><br>

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

<br><br>

---

<br>

## Modules

<br>

Los módulos permiten dividir una aplicación en múltiples archivos reutilizables, evitando que todo el código quede en un único archivo.
Cada archivo puede exportar funcionalidades para que otros archivos las utilicen.

<br>

```txt
Backend/
├─ app.js
├─ database.js
├─ routes.js
└─ utils.js
```

<br><br><br>

### Module Systems

<br>

Formas de importar y exportar código (paquetes y/o archivos). 
- `JavaScript` trae `ES Modules`.
- `Node.js` trae `CommonJS`.

<br>

| ES Modules (moderno) | CommonJS (tradicional de Node.js) |
|----------|----------|
| `import express from "express";` | `const express = require("express");` |
| `export default app;` | `module.exports = app;` |

<br>

- Para importar paquetes, no hace falta poner la ruta. Node.js automáticamente la busca.
- Para archivos propios, se debe poner la ruta `"./archivo.js;"`.

<br><br><br>

### Importante 

<br>

El paquete "dotenv" requiere añadir esto al ser importado:

<br>

```js
import dotenv from "dotenv";

dotenv.config();
```

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

---

<br>

## Usar Paquetes TP

<br>

1. Instalar los paquetes
2. Importar los paquetes en el código (si aplica)
3. Usarlo

<br><br><br>

### pg y dotenv

<br>

- `pg` permite conectarse a PostgreSQL y ejecutar consultas SQL.
- `dotenv` permite ocultar datos escritos en el archivo `.env` del repositorio.

<br><br>

Ejemplo sin `dotenv`:

<br>

```js
import pg from "pg";

const { Client } = pg;

const client = new Client({
    host: "localhost",
    user: "postgres",
    password: "postgres",
    database: "mi_db"
});
```

<br>

* host puede ser "db", depende de Docker.
* database va el nombre de tu database.

<br>

Ejemplo CON `dotenv`:

<br>

```js
import dotenv from "dotenv";
import pg from "pg";

dotenv.config();

const { Client } = pg;

const client = new Client({
    host: process.env.DB_HOST,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME
});
```

<br><br><br>

### Express

<br>

Permite crear servidores web y APIs con mayor facilidad.

<br>

Ejemplo:

<br>

```js
const app = express();

app.get("/", (req, res) => {
    res.send("Hola mundo");
});

app.listen(3000);
```

<br><br><br>

### nodemon

<br>

La 1ra vez:
1. ir a `package.json`

<br>

```json
{
  "name": "mi-app",
  "type": "module",
  "dependencies": {
    "express": "^5.0.0",
    "dotenv": "^17.0.0",
    "pg": "^8.0.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.0"
  }
}
```

<br>

2. Añadir la sección `"scripts"` para que quede así:

<br>

```json
{
  "name": "mi-app",
  "type": "module",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "dependencies": {
    "express": "^5.0.0",
    "dotenv": "^17.0.0",
    "pg": "^8.0.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.0"
  }
}
```

<br>

3. Antes de desarrollar, SIEMPRE correr el comando:

<br>

```bash
npm run dev
```

<br>

Así, nodemon reiniciará automáticamente la aplicación cada vez que detecte cambios en los archivos, permitiéndote ver las actualizaciones en tiempo real.

<br>

4. Si estás en producción, corres:

```bash
npm run start
```

<br>

Así, no se usará nodemon, ya que en producción no es necesario reiniciar automáticamente la aplicación cuando cambia el código.


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>



