
<br><br>

`Pending.`

### Table of Contents

<br>









<br><br>

---

<br>


---


# Node.js

- JavaScript nació como un lenguaje pensado para ejecutarse dentro del navegador. Ser parte del Frontend y nada más.
- El navegador actuaba como runtime y proporcionaba herramientas para interactuar con páginas web (DOM, eventos, almacenamiento, etc.).
- Por eso, originalmente, sin un navegador no era posible ejecutar código JavaScript.

A algunos les gustó JavaScript y decidieron crear el runtime Node.js (construido sobre V8, el compilador de Google Chrome) para que JavaScript pudiera usarse fuera del navegador y así usarse oara desarrollar aplicaciones Backend.

Gracias a Node.js, JavaScript puede:
- Crear servidores web
- Construir APIs REST
- Leer y escribir archivos
- Conectarse a bases de datos
- Ejecutar scripts y automatizaciones
- Conectarse a herramientas del sistema


# Packages

| Concepto                    | Qué es                                                                                         | Ejemplo                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Gestor de paquetes          | Herramienta para instalar, actualizar y eliminar paquetes                                      | `npm`, `pip`, `apt`, `cargo`                                     |
| Ejecutor de paquetes          | Ejecuta paquetes sin necesidad de instalarlos globalmente / que queden instalados con persistencia.                                   | `npx` es parte de `npm`                                     |
| Paquete                     | Unidad distribuible de código o herramientas que puede instalarse                              | `dotenv`, `nodemon`, `pg`                                        |
| Librería (tipo de paquete)  | Conjunto de funcionalidades que llamás desde tu código                                         | React, jQuery, Lodash                                            |
| Framework (tipo de paquete) | Estructura que organiza una aplicación y llama a tu código                                     | Express, Next.js, Angular                                        |
| Dev Tool (tipo de paquete)  | Herramienta que ayuda durante el desarrollo, pero no forma parte de la lógica de la aplicación | `Nodemon`, `Vite`, `TypeScript`, `Webpack`, linters |


### Instalación de paquetes

```bash
npm install express pg dotenv
npm install --save-dev nodemon
```

- `--save-dev` (o `-D`) guarda las dependencias como `devDependencies` en `package.json`.
- Se utiliza para herramientas de desarrollo que no son necesarias para ejecutar la aplicación en producción.

Al instalar paquetes, npm crea o actualiza:

- `package.json`: guarda las dependencias que necesita el proyecto y los rangos de versiones compatibles.
- `package-lock.json`: guarda las versiones exactas instaladas, incluyendo las dependencias de las dependencias, para garantizar instalaciones reproducibles.


| Paquete        | Función                                                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Express.js** | Facilita la creación de servidores web y APIs que reciben solicitudes y envían respuestas.                                                                                      |
| **pg**         | Permite conectar aplicaciones Node.js con PostgreSQL y ejecutar consultas SQL.                                                                                                  |
| **dotenv**     | Lee un archivo `.env` y carga sus valores como variables de entorno para que la aplicación pueda acceder a configuraciones como puertos, usuarios, contraseñas o claves de API. |
| **nodemon**    | Reinicia automáticamente la aplicación al detectar cambios en los archivos durante el desarrollo.                                                                               |






## APIs

### Qué es una API

Una API (Application Programming Interface) es un conjunto de reglas que permite que dos aplicaciones se comuniquen e intercambien información.

Actúa como intermediaria entre un cliente que realiza una solicitud y un servidor que procesa la solicitud y devuelve una respuesta.

### Cliente y servidor

- **Cliente:** aplicación que solicita información o realiza una acción.
- **Servidor:** aplicación que recibe la solicitud, la procesa y devuelve una respuesta.

```txt
Cliente
    ↓ Solicitud
Servidor
    ↓ Respuesta
Cliente
````

### Intercambio de información

El cliente envía una petición (*request*) a través de la API.

El servidor recibe la petición, ejecuta la lógica necesaria (consultar una base de datos, realizar cálculos, validar datos, etc.) y devuelve una respuesta (*response*).

```txt
Cliente
    ↓ Request
API / Servidor
    ↓ Response
Cliente
```

### Ejemplos de APIs

| API             | Función                                                                 |
| --------------- | ----------------------------------------------------------------------- |
| Google Maps API | Obtener mapas, rutas y ubicaciones.                                     |
| OpenWeather API | Consultar información meteorológica.                                    |
| GitHub API      | Acceder a repositorios, usuarios y commits.                             |
| Spotify API     | Consultar artistas, álbumes y canciones.                                |
| API propia      | Permitir que un frontend se comunique con el backend de una aplicación. |

La API es la "puerta de entrada" que utiliza el cliente para acceder a los recursos del servidor.

```txt
Frontend (cliente)
        ↓
      API
        ↓
Backend + Base de datos
```

## HTTP

### Qué es HTTP

HTTP (HyperText Transfer Protocol) es el protocolo utilizado para intercambiar información entre clientes y servidores en la web.

Define cómo se envían las solicitudes y cómo se reciben las respuestas.

```txt
Cliente
    ↓ HTTP Request
Servidor
    ↓ HTTP Response
Cliente
```

### Request y Response

#### Request

Es la solicitud enviada por el cliente al servidor.

Puede incluir:
- Método (GET, POST, PUT, DELETE, etc.)
- URL
- Headers
- Body

#### Response

Es la respuesta enviada por el servidor al cliente.

Puede incluir:
- Status Code
- Headers
- Body

```txt
Cliente
    ↓ Request
Servidor
    ↓ Response
Cliente
```

### Mensaje HTTP

Un mensaje HTTP está compuesto por:

```txt
Línea inicial
Headers

Body
```

Ejemplo:

```http
POST /usuarios HTTP/1.1
Host: ejemplo.com
Content-Type: application/json

{
  "nombre": "Ana"
}
```

### Headers

Los headers contienen información adicional sobre la solicitud o la respuesta.

Ejemplos:

| Header | Función |
|----------|----------|
| Content-Type | Indica el tipo de dato enviado. |
| Authorization | Envía credenciales o tokens. |
| Accept | Indica qué tipo de respuesta acepta el cliente. |
| User-Agent | Identifica al cliente que realiza la petición. |

### Body

El body contiene los datos que se desean enviar.

Se utiliza principalmente en métodos como POST, PUT o PATCH.

Ejemplo:

```json
{
  "nombre": "Ana",
  "edad": 25
}
```

### Status Codes

Los status codes indican el resultado de la solicitud.

| Código | Significado |
|----------|----------|
| 200 OK | La solicitud fue exitosa. |
| 201 Created | Recurso creado correctamente. |
| 204 No Content | Operación exitosa sin contenido de respuesta. |
| 400 Bad Request | Solicitud inválida. |
| 401 Unauthorized | Falta autenticación. |
| 403 Forbidden | Acceso denegado. |
| 404 Not Found | Recurso no encontrado. |
| 500 Internal Server Error | Error interno del servidor. |

Clasificación general:

| Rango | Tipo |
|---------|---------|
| 1xx | Informativos |
| 2xx | Éxito |
| 3xx | Redirección |
| 4xx | Error del cliente |
| 5xx | Error del servidor |





## HTTP CRUD y Methods


Los métodos HTTP indican qué acción desea realizar el cliente sobre un recurso.

| Método | Función |
|----------|----------|
| GET | Obtener información |
| POST | Crear información |
| PUT | Reemplazar información existente |
| PATCH | Modificar parcialmente información existente |
| DELETE | Eliminar información |


### Ejemplos

Obtener todos los usuarios:

```http
GET /usuarios
```

Obtener un usuario específico:

```http
GET /usuarios/5
```

Crear un usuario:

```http
POST /usuarios
```

Actualizar completamente un usuario:

```http
PUT /usuarios/5
```

Actualizar parcialmente un usuario:

```http
PATCH /usuarios/5
```

Eliminar un usuario:

```http
DELETE /usuarios/5
```

### Flujo típico

```txt
Cliente
    ↓ POST /usuarios
Servidor
    ↓ 201 Created

Cliente
    ↓ GET /usuarios
Servidor
    ↓ 200 OK

Cliente
    ↓ PATCH /usuarios/5
Servidor
    ↓ 200 OK

Cliente
    ↓ DELETE /usuarios/5
Servidor
    ↓ 204 No Content
```









## REST API

### Qué es REST

REST (Representational State Transfer) es un estilo de arquitectura para diseñar APIs.

Define un conjunto de convenciones para organizar recursos, URLs y métodos HTTP de forma consistente.

Una API que sigue estas convenciones se denomina **REST API**.

### Recursos

Un recurso es cualquier entidad sobre la que la API permite realizar operaciones.

Ejemplos:

- usuarios
- productos
- pedidos
- canciones

En REST, cada recurso se identifica mediante una URL.

```txt
/usuarios
/productos
/pedidos
/canciones
```

### Convenciones REST

Las REST APIs suelen seguir estas convenciones:

- Los recursos se nombran con sustantivos.
- Las URLs representan recursos.
- Las acciones se indican mediante métodos HTTP.
- Se utilizan códigos de estado HTTP adecuados.
- Los recursos suelen nombrarse en plural.

Ejemplos:

```http
GET    /usuarios
GET    /usuarios/5
POST   /usuarios
PATCH  /usuarios/5
DELETE /usuarios/5
```

### URLs

Las URLs identifican recursos específicos.

Ejemplos:

```txt
/usuarios
```

Colección de usuarios.

```txt
/usuarios/5
```

Usuario con id 5.

```txt
/usuarios/5/pedidos
```

Pedidos pertenecientes al usuario con id 5.

### Stateless

REST es **stateless** (sin estado).

Cada request debe contener toda la información necesaria para ser procesada.

El servidor no debe depender de información almacenada de requests anteriores.

```txt
Request 1
↓
Servidor procesa
↓
Respuesta

Request 2
↓
Servidor procesa nuevamente
↓
Respuesta
```

Cada request es independiente de las demás.

### Ejemplo completo

```txt
Cliente
    ↓ GET /usuarios/5
Servidor
    ↓ Busca usuario 5
Servidor
    ↓ 200 OK + datos

Cliente
    ↓ DELETE /usuarios/5
Servidor
    ↓ Elimina usuario 5
Servidor
    ↓ 204 No Content
```

La URL identifica el recurso y el método HTTP indica la acción a realizar sobre él.







## Endpoints

### Qué es un endpoint

Un endpoint es una URL específica de una API a la que un cliente puede enviar requests para interactuar con un recurso.

Cada endpoint representa una operación o acceso a un recurso determinado.

Ejemplos:

```txt
/api/users
/api/users/1
/api/products
```

### Parámetros de ruta

Los parámetros de ruta (*path parameters*) identifican recursos específicos dentro de la URL.

Ejemplos:

```txt
/api/users/1
```

Obtiene el usuario con id 1.

```txt
/api/products/25
```

Obtiene el producto con id 25.

Generalmente se representan así:

```txt
/api/users/:id
/api/products/:id
```

### Query Parameters

Los query parameters permiten filtrar, ordenar o personalizar la información solicitada.

Se agregan después de `?` en la URL.

Ejemplos:

```txt
/api/users?age=20
```

Usuarios cuya edad sea 20.

```txt
/api/products?category=electronics
```

Productos de la categoría electronics.

```txt
/api/users?page=2&limit=10
```

Segunda página de resultados mostrando 10 elementos.

### Ejemplos

| Endpoint | Descripción |
|-----------|-----------|
| `/api/users` | Obtener todos los usuarios |
| `/api/users/1` | Obtener el usuario con id 1 |
| `/api/users?age=20` | Filtrar usuarios por edad |
| `/api/products` | Obtener todos los productos |
| `/api/products/25` | Obtener el producto con id 25 |
| `/api/products?category=electronics` | Filtrar productos por categoría |

### Comparación

| Tipo | Ejemplo | Uso |
|--------|--------|--------|
| Parámetro de ruta | `/api/users/1` | Identificar un recurso específico |
| Query parameter | `/api/users?age=20` | Filtrar o modificar la consulta |

### Ejemplo completo

```txt
GET /api/users/1
```

Obtiene un usuario específico.

```txt
GET /api/users?page=2&limit=10
```

Obtiene la segunda página de usuarios con un máximo de 10 resultados.

```txt
GET /api/products?category=electronics
```

Obtiene productos filtrados por categoría.











## Ciclo HTTP completo

Cuando un cliente necesita información o desea realizar una acción, envía un request HTTP a un endpoint de la API.

El backend recibe la solicitud, ejecuta la lógica correspondiente y, si es necesario, consulta o modifica datos en la base de datos.

Finalmente, el backend genera una respuesta HTTP y la devuelve al cliente.

```txt
Cliente
    ↓ HTTP Request
Endpoint
    ↓
Backend
    ↓
Base de datos
    ↓
Backend
    ↓ HTTP Response
Cliente
```

### Ejemplo

Un usuario abre una página que muestra todos los productos:

```txt
Cliente
    ↓ GET /api/products
Endpoint
    ↓
Backend
    ↓ SELECT * FROM products
Base de datos
    ↓ Lista de productos
Backend
    ↓ 200 OK + datos
Cliente
```

### Qué ocurre en cada etapa

| Etapa | Función |
|---------|---------|
| Cliente | Envía la solicitud. |
| HTTP Request | Contiene método, URL, headers y opcionalmente body. |
| Endpoint | Identifica qué recurso o acción se solicita. |
| Backend | Ejecuta la lógica de negocio. |
| Base de datos | Almacena y devuelve datos. |
| HTTP Response | Contiene status code, headers y opcionalmente body. |
| Cliente | Recibe y utiliza la respuesta. |

### Relación entre conceptos

```txt
Cliente
    ↓
HTTP Request
    ↓
Método HTTP + URL
    ↓
Endpoint
    ↓
Backend (Express)
    ↓
Base de datos (PostgreSQL)
    ↓
HTTP Response
    ↓
Cliente
```

Este flujo es la base del funcionamiento de la mayoría de las aplicaciones web modernas.


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

