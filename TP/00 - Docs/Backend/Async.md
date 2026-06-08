

## Promises y asincronía

### Qué es la asincronía

La asincronía permite ejecutar tareas que pueden tardar tiempo sin bloquear el resto del programa.

Ejemplos:

- Consultar una API.
- Leer un archivo.
- Realizar una consulta a una base de datos.

```txt
Programa
    ↓
Inicia tarea lenta
    ↓
Sigue ejecutándose
    ↓
Recibe resultado cuando termina
```

### Callbacks

Un callback es una función que se pasa como argumento para ejecutarse cuando una tarea finaliza.

```js
setTimeout(() => {
    console.log("Hola");
}, 1000);
```

Problema:

```txt
Callback
    ↓
Otro callback
    ↓
Otro callback
    ↓
Callback Hell
```

### Promises

Una Promise representa el resultado futuro de una operación asíncrona.

| Estado | Significado |
|----------|----------|
| Pending | En ejecución |
| Fulfilled | Completada correctamente |
| Rejected | Ocurrió un error |

```txt
Pending
 ├─ Fulfilled
 └─ Rejected
```

### then

Se ejecuta cuando la Promise finaliza correctamente.

```js
fetch("/api/users")
    .then(response => response.json())
    .then(data => console.log(data));
```

### catch

Se ejecuta cuando ocurre un error.

```js
fetch("/api/users")
    .catch(error => console.error(error));
```

### async/await

Permite trabajar con Promises utilizando una sintaxis más simple y legible.

```js
async function obtenerUsuarios() {
    const response = await fetch("/api/users");
    const data = await response.json();

    console.log(data);
}
```

Manejo de errores:

```js
async function obtenerUsuarios() {
    try {
        const response = await fetch("/api/users");
        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

### fetch

`fetch()` permite realizar requests HTTP desde JavaScript.

```js
const response = await fetch("/api/users");
const data = await response.json();
```

### Relación con los paquetes del proyecto

La asincronía es una característica propia de JavaScript, no un paquete.

Sin embargo, los paquetes del backend suelen utilizar Promises y `async/await` internamente.

Ejemplo con PostgreSQL:

```js
const result = await pool.query(
    "SELECT * FROM users"
);
```

Flujo típico:

```txt
Frontend (JavaScript)
    ↓
fetch()
    ↓
HTTP Request
    ↓
Endpoint (Express)
    ↓
pg consulta PostgreSQL
    ↓
Promise pendiente
    ↓
await espera sin bloquear
    ↓
PostgreSQL devuelve datos
    ↓
Promise resuelta
    ↓
Express construye la respuesta
    ↓
HTTP Response
    ↓
fetch() recibe la respuesta
    ↓
await o then()
    ↓
Datos disponibles
```

