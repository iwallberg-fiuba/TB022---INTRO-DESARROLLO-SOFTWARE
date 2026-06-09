
<br><br>

`Pending.`

### Table of Contents

<br>


endpoints






<br><br>

---

<br>



## APIs

### Qué es una API

Una API (Application Programming Interface) es un conjunto de reglas que permite que dos aplicaciones se comuniquen e intercambien información.

Actúa como intermediaria entre un cliente que realiza una solicitud y un servidor que procesa la solicitud y devuelve una respuesta.

La API es la "puerta de entrada" que utiliza el cliente para acceder a los recursos del servidor.

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

| Cliente                      | Ejemplo               |
| ---------------------------- | --------------------- |
| Navegador web                | Chrome, Firefox, Edge |
| Aplicación móvil             | Instagram, WhatsApp   |
| Aplicación de escritorio     | Discord, Spotify      |
| Programa que consume una API | Postman, curl         |


### Intercambio de información

El cliente envía una petición (*request*) a través de la API.

El servidor recibe la petición, ejecuta la lógica necesaria (consultar una base de datos, realizar cálculos, validar datos, etc.) y devuelve una respuesta (*response*).

Pero, como asegurarse de que se entienden?
Ejemplo:
Un frances puede intentar hablar con un alemán, pero si no establecen un protocolo (ej: hablar en ingles, que ambos saben) no se van a entender.

Ahí entra HTTP. HTTP (HyperText Transfer Protocol) es el protocolo utilizado para intercambiar información entre clientes y servidores en la web. Define cómo se envían las solicitudes y cómo se reciben las respuestas.

En este caso, se usará:
- Cliente = Navegador = Frontend = HTML, CSS y JS
- Backend = Servidor = Node.js + Express.js
- Protocolo = HTTP

Por ejemplo:

1. El usuario hace click en "Ver usuarios".
2. El frontend / cliente envía una HTTP Request a la API.
3. La API ejecuta lógica en el backend / servidor.
4. El backend consulta PostgreSQL.
5. PostgreSQL devuelve datos.
6. El backend genera una HTTP Response.
7. La API la envía al frontend / cliente.
8. El frontend / cliente muestra los datos.

```txt
Usuario
    ↓
Frontend / Cliente
    ↓ HTTP Request
API / Backend / Servidor
    ↓ Query SQL
Base de datos
    ↓ Datos
Backend / Servidor
    ↓ HTTP Response
Frontend / Cliente
    ↓
Usuario
```

### Ejemplos de APIs

| API             | Función                                                                 |
| --------------- | ----------------------------------------------------------------------- |
| Google Maps API | Obtener mapas, rutas y ubicaciones.                                     |
| OpenWeather API | Consultar información meteorológica.                                    |
| GitHub API      | Acceder a repositorios, usuarios y commits.                             |
| Spotify API     | Consultar artistas, álbumes y canciones.                                |
| API propia      | Permitir que un frontend se comunique con el backend de una aplicación. |











## HTTP Requests y Responses


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

| Acción                              | Método y ruta        |
| ----------------------------------- | -------------------- |
| Obtener todos los usuarios          | `GET /usuarios`      |
| Obtener un usuario específico       | `GET /usuarios/5`    |
| Crear un usuario                    | `POST /usuarios`     |
| Actualizar completamente un usuario | `PUT /usuarios/5`    |
| Actualizar parcialmente un usuario  | `PATCH /usuarios/5`  |
| Eliminar un usuario                 | `DELETE /usuarios/5` |



### Flujo HTTP

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

