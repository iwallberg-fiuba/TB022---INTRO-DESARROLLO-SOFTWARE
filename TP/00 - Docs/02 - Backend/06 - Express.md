


---

## Utilidades

- Express.js es un paquete del tipo framework para Node.js
- La ventaje principal que trae express es reducir la cantidad de código, pero manteniendo las mismas lógicas de Node.js
- Node.js hace todo lo que Express.js puede hacer, pero en más líneas de código o en líneas más difíciles de leer.


### Crear servidor HTTP

```js
import express from "express";

const app = express();

app.get("/", (req, res) => {
    res.send("Hola");
});

app.listen(3000);
```

```txt
app.listen(3000)
↓
Servidor iniciado
↓
Escucha requests en el puerto 3000
↓
Llega una request
↓
Express la procesa
↓
Envía una response
```

### Definir rutas

Una ruta (*route*) indica qué debe hacer el servidor cuando recibe una request para una URL y un método HTTP determinados.

Las rutas son la base de una API, ya que permiten asociar distintas URLs y métodos HTTP con diferentes funcionalidades del backend.

Express permite definir rutas de forma sencilla mediante métodos como:

```js
app.get(...)
app.post(...)
app.put(...)
app.patch(...)
app.delete(...)
```

Ejemplo:

>[!NOTE]
>La ruta `/` representa la ruta raíz (*root route*), es decir, la página principal del sitio web o de la API.

```js
app.get("/", (req, res) => {
    res.send("Bienvenido");
});

app.get("/usuarios", (req, res) => {
    res.send("Lista de usuarios");
});

app.get("/productos", (req, res) => {
    res.send("Lista de productos");
});
```

Al ejecutar estas instrucciones, Express registra las rutas:

```txt
GET /
→ Bienvenido

GET /usuarios
→ Lista de usuarios

GET /productos
→ Lista de productos
```

Cuando llega una request, Express analiza el método HTTP y la ruta solicitada, 
busca una coincidencia entre las rutas registradas y ejecuta la función asociada.

Por ejemplo:

```txt
GET /usuarios
↓
Express recibe la request
↓
Busca una ruta GET /usuarios
↓
Encuentra la coincidencia
↓
Ejecuta la función asociada
↓
res.send("Lista de usuarios")
↓
Envía la response
```



### Requests

Recordemos elementos de la HTTP Request:

```txt
Request
├─ Método HTTP (GET, POST, PUT, DELETE, ...)
├─ Ruta (/usuarios, /productos, ...)
├─ Headers
├─ Query Parameters
├─ Parámetros de ruta
└─ Body
```

Express recibe esta información a través del objeto `req` (*request*).

```js
app.get("/usuarios/:id", (req, res) => {
    console.log(req.params.id);
});
```

Por ejemplo, si llega:

```txt
GET /usuarios/15
```

Express procesa la request y permite acceder al valor:

```txt
req.params.id
↓
15
```

### Enviar responses

### Crear APIs REST

### Leer datos enviados por el cliente

### Middleware

### Servidor y Base de Datos

### Separar lógica en múltiples archivos

















---

## Estructuras

```js
import express from "express";

const app = express();

app.listen(3000, () => {
    console.log("Servidor iniciado en http://localhost:3000");
});
```

Explicación:

### App

De la parte:

```js
const app = express();
```

`app` representa la aplicación Express.

A través de `app` se configuran:

```txt
app
├─ rutas
├─ middlewares
├─ configuración del servidor
└─ manejo de requests y responses
```

---

### App Listen

`app.listen()` inicia el servidor.

```js
app.listen(3000);
```

Significa:

```txt
Servidor
↓
Escuchar el puerto 3000
↓
Esperar requests
```

Con mensaje en consola:

```js
app.listen(3000, () => {
    console.log("Servidor iniciado");
});
```

---

### Request y Response

De la parte:
```js
(req, res) => {
    // lógica
}
```

En Express, cada vez que llega una request, se ejecuta una función.

Esa función recibe dos objetos principales:

```txt
req → request
res → response
```

---

### `req`

`req` representa la request del cliente.

Contiene información como:

```txt
req
├─ req.params
├─ req.query
├─ req.body
├─ req.headers
├─ req.method
└─ req.url
```

---

### `res`

`res` representa la response que el servidor enviará al cliente.

Permite responder con:

```txt
res
├─ res.send()
├─ res.json()
├─ res.status()
└─ res.redirect()
```

---

# Rutas

Una ruta indica qué debe hacer el servidor cuando recibe una request específica.

Ejemplo:

```js
app.get("/", (req, res) => {
    res.send("Hola");
});
```

Significa:

```txt
Si llega una request GET a "/"
↓
Ejecutar esta función
↓
Responder "Hola"
```

---

# Métodos HTTP en Express

Express permite definir rutas según el método HTTP.

```js
app.get(...)
app.post(...)
app.put(...)
app.patch(...)
app.delete(...)
```

| Método | Uso habitual | Ejemplo |
|---|---|---|
| GET | Obtener datos | Ver usuarios |
| POST | Crear datos | Crear usuario |
| PUT | Reemplazar datos | Reemplazar usuario completo |
| PATCH | Modificar parte de los datos | Cambiar nombre de usuario |
| DELETE | Eliminar datos | Borrar usuario |

---

# Ejemplo de rutas

```js
app.get("/usuarios", (req, res) => {
    res.send("Lista de usuarios");
});

app.post("/usuarios", (req, res) => {
    res.send("Usuario creado");
});

app.put("/usuarios/:id", (req, res) => {
    res.send("Usuario reemplazado");
});

app.patch("/usuarios/:id", (req, res) => {
    res.send("Usuario modificado");
});

app.delete("/usuarios/:id", (req, res) => {
    res.send("Usuario eliminado");
});
```

---

# Enviar respuestas

## Texto

```js
app.get("/", (req, res) => {
    res.send("Hola");
});
```

---

## JSON

```js
app.get("/usuario", (req, res) => {
    res.json({
        id: 1,
        nombre: "Ana"
    });
});
```

Respuesta:

```json
{
    "id": 1,
    "nombre": "Ana"
}
```

---

## Status HTTP

```js
app.get("/usuarios", (req, res) => {
    res.status(200).json({
        mensaje: "Usuarios encontrados"
    });
});
```

Ejemplo con error:

```js
app.get("/usuarios", (req, res) => {
    res.status(404).json({
        error: "Usuarios no encontrados"
    });
});
```

---

# Parámetros de ruta

Los parámetros de ruta sirven para capturar valores dentro de la URL.

```js
app.get("/usuarios/:id", (req, res) => {
    res.send(req.params.id);
});
```

Request:

```txt
GET /usuarios/15
```

Valor obtenido:

```txt
15
```

Porque:

```txt
/usuarios/:id
↓
/usuarios/15
↓
id = 15
```

Ejemplo más completo:

```js
app.get("/usuarios/:id", (req, res) => {
    const id = req.params.id;

    res.json({
        mensaje: "Usuario encontrado",
        id: id
    });
});
```

---

# Query Parameters

Los query parameters son datos opcionales enviados al final de la URL.

Ejemplo:

```txt
GET /usuarios?edad=20
```

Se leen con `req.query`.

```js
app.get("/usuarios", (req, res) => {
    const edad = req.query.edad;

    res.json({
        edad: edad
    });
});
```

También puede haber varios:

```txt
GET /usuarios?edad=20&pais=Argentina
```

```js
app.get("/usuarios", (req, res) => {
    res.json({
        edad: req.query.edad,
        pais: req.query.pais
    });
});
```

Resultado:

```json
{
    "edad": "20",
    "pais": "Argentina"
}
```

Importante:

```txt
Los query parameters llegan como texto.
```

---

# Body

El body es información enviada dentro de la request.

Se usa mucho en requests `POST`, `PUT` y `PATCH`.

Ejemplo de body JSON:

```json
{
    "nombre": "Ana",
    "edad": 20
}
```

Para que Express pueda leer JSON, se agrega:

```js
app.use(express.json());
```

Ejemplo:

```js
app.post("/usuarios", (req, res) => {
    const nombre = req.body.nombre;
    const edad = req.body.edad;

    res.json({
        mensaje: "Usuario recibido",
        nombre: nombre,
        edad: edad
    });
});
```

Flujo:

```txt
Cliente envía JSON
↓
Express lee el body con express.json()
↓
La ruta accede a req.body
↓
Servidor responde
```

---

# Params vs Query vs Body

| Tipo | Dónde viaja | Cómo se lee | Ejemplo |
|---|---|---|---|
| Params | En la ruta | `req.params` | `/usuarios/15` |
| Query | En la URL después de `?` | `req.query` | `/usuarios?edad=20` |
| Body | Dentro de la request | `req.body` | `{ "nombre": "Ana" }` |

---

# Middleware

Un middleware es una función que se ejecuta entre la request y la ruta final.

```txt
Request
↓
Middleware
↓
Ruta
↓
Response
```

Ejemplo:

```js
app.use((req, res, next) => {
    console.log("Llegó una request");
    next();
});
```

`next()` significa:

```txt
Continuar con el siguiente middleware o ruta
```

Si no se llama a `next()` y tampoco se responde, la request queda colgada.

---

## Middleware `express.json()`

Este middleware permite leer bodies en formato JSON.

```js
app.use(express.json());
```

Sin esto, `req.body` puede aparecer vacío o `undefined`.

---

## Middleware propio

```js
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
```

Si llega:

```txt
GET /usuarios
```

Se muestra:

```txt
GET /usuarios
```

---

# Orden de ejecución

El orden importa.

```js
app.use(express.json());

app.use((req, res, next) => {
    console.log("Middleware");
    next();
});

app.get("/", (req, res) => {
    res.send("Hola");
});
```

Flujo:

```txt
Request
↓
express.json()
↓
Middleware propio
↓
Ruta GET /
↓
Response
```

---

# API REST con Express

Una API REST suele organizar recursos usando rutas.

Ejemplo con recurso `usuarios`:

```txt
GET    /usuarios       → obtener todos los usuarios
GET    /usuarios/:id   → obtener un usuario
POST   /usuarios       → crear usuario
PUT    /usuarios/:id   → reemplazar usuario
PATCH  /usuarios/:id   → modificar usuario
DELETE /usuarios/:id   → eliminar usuario
```

---

# Ejemplo completo sin base de datos

```js
import express from "express";

const app = express();

app.use(express.json());

const usuarios = [
    { id: 1, nombre: "Ana" },
    { id: 2, nombre: "Juan" }
];

app.get("/usuarios", (req, res) => {
    res.json(usuarios);
});

app.get("/usuarios/:id", (req, res) => {
    const id = Number(req.params.id);

    const usuario = usuarios.find(usuario => usuario.id === id);

    if (!usuario) {
        return res.status(404).json({
            error: "Usuario no encontrado"
        });
    }

    res.json(usuario);
});

app.post("/usuarios", (req, res) => {
    const nuevoUsuario = {
        id: usuarios.length + 1,
        nombre: req.body.nombre
    };

    usuarios.push(nuevoUsuario);

    res.status(201).json(nuevoUsuario);
});

app.listen(3000, () => {
    console.log("Servidor iniciado en http://localhost:3000");
});
```

---

# Express y base de datos

Express no es la base de datos.

Express recibe la request y envía la response.

La base de datos guarda y devuelve datos.

```txt
Cliente
↓
Express
↓
Base de datos
↓
Express
↓
Cliente
```

Ejemplo con PostgreSQL:

```js
app.get("/usuarios", async (req, res) => {
    const resultado = await pool.query(
        "SELECT * FROM usuarios"
    );

    res.json(resultado.rows);
});
```

---

# Express y asincronía

Express no crea la asincronía.

La asincronía viene de JavaScript y Node.js.

Express simplemente permite usar funciones asíncronas dentro de las rutas.

```js
app.get("/usuarios", async (req, res) => {
    const resultado = await pool.query(
        "SELECT * FROM usuarios"
    );

    res.json(resultado.rows);
});
```

Flujo:

```txt
Request
↓
Express ejecuta la ruta
↓
Se consulta la base de datos
↓
Node.js no se bloquea
↓
La base de datos responde
↓
Express envía la response
```

---

# Manejo de errores

Cuando algo puede fallar, se usa `try/catch`.

```js
app.get("/usuarios", async (req, res) => {
    try {
        const resultado = await pool.query(
            "SELECT * FROM usuarios"
        );

        res.json(resultado.rows);
    } catch (error) {
        res.status(500).json({
            error: "Error interno del servidor"
        });
    }
});
```

---

# Organización de archivos

En proyectos reales no se suele poner todo en un solo archivo.

Una estructura posible:

```txt
backend/
├─ package.json
├─ src/
│  ├─ app.js
│  ├─ server.js
│  ├─ routes/
│  │  └─ usuarios.routes.js
│  ├─ controllers/
│  │  └─ usuarios.controller.js
│  └─ db/
│     └─ pool.js
└─ .env
```

---

## `app.js`

```js
import express from "express";
import usuariosRoutes from "./routes/usuarios.routes.js";

const app = express();

app.use(express.json());

app.use("/usuarios", usuariosRoutes);

export default app;
```

---

## `server.js`

```js
import app from "./app.js";

app.listen(3000, () => {
    console.log("Servidor iniciado en http://localhost:3000");
});
```

---

## `usuarios.routes.js`

```js
import express from "express";
import {
    obtenerUsuarios,
    obtenerUsuarioPorId,
    crearUsuario
} from "../controllers/usuarios.controller.js";

const router = express.Router();

router.get("/", obtenerUsuarios);
router.get("/:id", obtenerUsuarioPorId);
router.post("/", crearUsuario);

export default router;
```

---

## `usuarios.controller.js`

```js
export function obtenerUsuarios(req, res) {
    res.json([
        { id: 1, nombre: "Ana" },
        { id: 2, nombre: "Juan" }
    ]);
}

export function obtenerUsuarioPorId(req, res) {
    const id = req.params.id;

    res.json({
        id: id,
        nombre: "Ana"
    });
}

export function crearUsuario(req, res) {
    const nombre = req.body.nombre;

    res.status(201).json({
        mensaje: "Usuario creado",
        nombre: nombre
    });
}
```

---

# Router

`express.Router()` permite separar rutas en archivos distintos.

En vez de hacer todo así:

```js
app.get("/usuarios", ...);
app.post("/usuarios", ...);
app.get("/productos", ...);
app.post("/productos", ...);
```

Se puede separar:

```txt
routes/
├─ usuarios.routes.js
└─ productos.routes.js
```

Ejemplo:

```js
const router = express.Router();
```

Luego:

```js
router.get("/", obtenerUsuarios);
router.post("/", crearUsuario);
```

Y en `app.js`:

```js
app.use("/usuarios", usuariosRoutes);
```

Eso significa:

```txt
Todas las rutas de usuariosRoutes empiezan con /usuarios
```

Entonces:

```js
router.get("/", obtenerUsuarios);
```

queda como:

```txt
GET /usuarios
```

Y:

```js
router.get("/:id", obtenerUsuarioPorId);
```

queda como:

```txt
GET /usuarios/:id
```

---

# Resumen visual

```txt
Cliente
↓
Request HTTP
↓
Node.js
↓
Express
↓
Middleware
↓
Ruta
↓
Controller
↓
Base de datos, si hace falta
↓
Controller
↓
Response HTTP
↓
Cliente
```

---

# Resumen final

Express.js es un framework para Node.js que facilita la creación de servidores web y APIs HTTP.

No reemplaza a Node.js.

No es una base de datos.

No crea la asincronía.

Su función principal es hacer más simple el manejo de:

```txt
Express
├─ servidor HTTP
├─ rutas
├─ métodos HTTP
├─ request
├─ response
├─ middlewares
├─ routers
└─ APIs REST
```

En una API típica:

```txt
Cliente
↓
Hace una request
↓
Express recibe la request
↓
Express busca la ruta correspondiente
↓
Se ejecuta la lógica del backend
↓
Opcionalmente se consulta una base de datos
↓
Express envía una response
↓
Cliente recibe la respuesta
```
