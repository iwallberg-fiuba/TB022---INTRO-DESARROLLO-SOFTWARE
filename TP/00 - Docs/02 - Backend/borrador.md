

## Asincronía con Express

¿Por qué Node.js usa asincronía?

Un servidor web recibe muchas requests al mismo tiempo.

```txt
Cliente A
Cliente B
Cliente C
Cliente D
```

Si cada request bloqueara el servidor hasta terminar:

```txt
Cliente A
↓
Esperar resultado
↓
Responder

Cliente B
↓
Esperar

Cliente C
↓
Esperar
```

el rendimiento sería muy bajo.

Node.js fue diseñado para evitar ese problema.

---

## Node.js

Node.js permite ejecutar JavaScript fuera del navegador.

```txt
JavaScript
↓
Node.js Runtime
↓
Sistema Operativo
```

Internamente utiliza:

```txt
JavaScript
├─ Single Thread
├─ Call Stack
├─ Event Loop
├─ APIs de Node.js
└─ Sistema Operativo
```

El código JavaScript sigue ejecutándose en un único hilo principal.

---

## Código Síncrono

Las instrucciones se ejecutan una detrás de otra.

```js
console.log("Inicio");
console.log("Consulta");
console.log("Fin");
```

```txt
Salida Esperada:

Inicio
Consulta
Fin
```

JavaScript no comienza la siguiente instrucción hasta terminar la anterior.

---

#### Problema

Supongamos que una consulta a PostgreSQL tarda 3 segundos.

Si Node.js trabajara de forma completamente síncrona:

```txt
Request
↓
Consultar PostgreSQL
↓
Esperar 3 segundos
↓
Responder
```

Durante esos 3 segundos no podría atender otras requests.

---

## Código Asíncrono

Node.js delega las tareas lentas a componentes externos.
Node.js puede manejar muchas conexiones concurrentes porque las tareas lentas (base de datos, archivos, red, APIs, etc.) 
se delegan mientras el hilo principal sigue disponible para ejecutar JavaScript.

```txt
Request
↓
Consulta PostgreSQL
↓
Delegar trabajo
↓
Seguir atendiendo requests
```

Cuando PostgreSQL termina:

```txt
PostgreSQL responde
↓
Event Loop
↓
Continuar ejecución
↓
Enviar respuesta
```

---

## Express

Express simplifica la creación de servidores HTTP.



```js
import express from "express";

const app = express();

app.listen(3000);
```

---

## Ruta Síncrona

```js
app.get("/", (req, res) => {
    res.send("Hola");
});
```

Flujo:

```txt
Request
↓
Express ejecuta la función
↓
Response
```

Todo ocurre inmediatamente.

---

## Ruta Asíncrona

Consulta a PostgreSQL:

```js
app.get("/usuarios", async (req, res) => {
    const resultado = await pool.query(
        "SELECT * FROM usuarios"
    );

    res.json(resultado.rows);
});
```

---

## ¿Qué ocurre internamente?

Llega una request:

```txt
Cliente
↓
GET /usuarios
↓
Express
↓
Handler
```

Se ejecuta:

```js
await pool.query(...)
```

Entonces Node.js hace algo parecido a:

```txt
Pedir consulta a PostgreSQL
↓
Seguir trabajando
```

Node.js no queda bloqueado esperando.

Puede continuar atendiendo otras requests.

---

## Promises

La consulta devuelve una Promise.

```js
const resultado = pool.query(
    "SELECT * FROM usuarios"
);
```

Estados posibles:

```txt
Pending
├─ Fulfilled
└─ Rejected
```

- Pending: todavía está ejecutándose.
- Fulfilled: terminó correctamente.
- Rejected: ocurrió un error.

Mientras la Promise está pendiente, Node.js puede seguir trabajando.

---

## async / await

### Sin async / await

```js
app.get("/usuarios", (req, res) => {
    pool.query(
        "SELECT * FROM usuarios"
    )
    .then(resultado => {
        res.json(resultado.rows);
    })
    .catch(error => {
        res.status(500).send(error.message);
    });
});
```

### Con async / await

```js
app.get("/usuarios", async (req, res) => {
    try {
        const resultado = await pool.query(
            "SELECT * FROM usuarios"
        );

        res.json(resultado.rows);
    } catch (error) {
        res.status(500).send(error.message);
    }
});
```

La lógica es la misma.

`async/await` sólo hace el código más fácil de leer.

---

## Event Loop

El Event Loop coordina la ejecución de tareas asíncronas.

Su trabajo es revisar continuamente:

```txt
¿La Call Stack está vacía?
↓
Sí
↓
Ejecutar tarea pendiente
```

Ejemplo:

```js
console.log("Inicio");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("Fin");
```

```txt
Salida Esperada:

Inicio
Fin
Timer
```

Aunque Timer sea 0.

Flujo:

```txt
console.log("Inicio")
↓
setTimeout(...)
↓
console.log("Fin")
↓
Call Stack vacía
↓
Event Loop toma callback
↓
console.log("Timer")
```

---

## Varias Requests Simultáneas

Supongamos:

```txt
Cliente A
↓
GET /usuarios

Cliente B
↓
GET /productos

Cliente C
↓
GET /categorias
```

Node.js recibe las tres requests.

```txt
Request A
↓
Consulta SQL

Request B
↓
Consulta SQL

Request C
↓
Consulta SQL
```

Las consultas son delegadas.

Node.js sigue libre para recibir nuevas requests.

Cuando PostgreSQL responde:

```txt
Resultado B listo
↓
Response B

Resultado A listo
↓
Response A

Resultado C listo
↓
Response C
```

No necesariamente responden en el mismo orden en que llegaron.

Responden cuando terminan.

---

## Flujo Completo

```txt
Cliente
↓
Request HTTP
↓
Express
↓
Ruta (Handler)
↓
await pool.query(...)
↓
Node.js delega la consulta
↓
Sigue atendiendo otras requests
↓
PostgreSQL responde
↓
Promise resuelta
↓
Event Loop
↓
Express continúa el handler
↓
res.json(...)
↓
Response HTTP
```
