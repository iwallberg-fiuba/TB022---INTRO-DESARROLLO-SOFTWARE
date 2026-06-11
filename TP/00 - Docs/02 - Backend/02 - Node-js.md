
<br><br>

### Table of Contents

<br>

[Definiciones](#Definiciones)

[Paquetes TP](#Paquetes-TP)

[Modules](#Modules)
- [Module Systems](#Module-Systems)
- [Importante](#Importante)

[Usar Paquetes *](#Usar-Paquetes)
- [pg y dotenv](#pg-y-dotenv)
- [Express](#Express)

<br>

`* Muy simplificado para ver ejemplos. Idea más desarrollada archivos después.`

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
- `JavaScript` trae `ES Modules` (el que usamos).
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

## Usar Paquetes

<br>

>[!NOTE]
>Muy simplificado para ver ejemplos. Idea más desarrollada archivos después.

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

[Volver a Table of Contents](#Table-of-Contents)

<br>



