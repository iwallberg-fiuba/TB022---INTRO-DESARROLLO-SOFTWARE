


### Table of Contents




---


## REST APIs

Una REST API es una forma de organizar una API HTTP alrededor de los recursos (= ENTIDADES DE TU APP), donde las URLs identifican recursos y los métodos HTTP indican las acciones sobre ellos.
Además, es stateless: cada request es independiente al resto.


### Qué es de REST y qué no?

REST tiene más que ver con la forma en la que vemos y organizamos los elementos.
Trae "Conceptos propios" pero que justamente hablan sobre cómo ordenar o no algo.


| Concepto                           | HTTP | REST                          |
| ---------------------------------- | ---- | ----------------------------- |
| Request                            | ✅    | ❌                             |
| Response                           | ✅    | ❌                             |
| Headers                            | ✅    | ❌                             |
| Body                               | ✅    | ❌                             |
| Métodos HTTP (`GET`, `POST`, etc.) | ✅    | REST los utiliza              |
| Status Codes (`200`, `404`, etc.)  | ✅    | REST los utiliza              |
| URL                                | ✅    | REST las utiliza              |
| Ruta (Path)                        | ✅    | REST las utiliza              |
| Query Parameters                   | ✅    | REST los utiliza              |
| Cliente-Servidor                   | ❌    | Uno de los principios de REST |
| Recursos (`usuarios`, `productos`) | ❌    | ✅                             |
| Endpoints organizados por recursos | ❌    | ✅                             |
| Stateless                          | ❌    | ✅                             |



### HTTP Methods

Esto existe independientemente de REST, REST sólo arma una convención sobre cómo lo vemos y organizamos.

| Método   | Acción                   |
| -------- | ------------------------ |
| `GET`    | Obtener datos            |
| `POST`   | Crear datos              |
| `PUT`    | Reemplazar completamente |
| `PATCH`  | Modificar parcialmente   |
| `DELETE` | Eliminar                 |


### Rutas

Esto existe independientemente de REST, REST sólo arma una convención sobre cómo lo vemos y organizamos.


```txt
https://api.ejemplo.com/usuarios  } esto es la URL
│       │              │
│       │              └─ Ruta (path)
│       └─ Dominio
└─ Protocolo
```


#### Parámetros

Esto existe independientemente de REST, REST sólo arma una convención sobre cómo lo vemos y organizamos.


| Tipo              | Ejemplo                 | Uso                                   |
| ----------------- | ----------------------- | ------------------------------------- |
| Parámetro de ruta | `/usuarios/{id}`           | Identificar un recurso específico     |
| Query parameter   | `/usuarios?page={valor}` | Filtrar, ordenar o paginar resultados |
| Query parameter   | `/usuarios?{columna}={valor}`  | Filtrar resultados                    |
| Query parameter   | `/usuarios?sort={columna}` | Ordenar resultados                    |



### Recursos

- Recursos = entidades de tu app en la base de datos. 
- REST propone que cada recurso tenga su RUTA

Ejemplo:
```
Usuarios      → /usuarios
Productos     → /productos
Pedidos       → /pedidos
Canciones     → /canciones
```

Entonces:
- Acción = Método HTTP
- Recurso = Entidades de la app
- Cada recurso tendrá su propia ruta


### Endpoints

Al sumar Método HTTP + Ruta, obtenemos un Endpoint.

Esto existe independientemente de REST, REST sólo arma una convención sobre cómo lo vemos y organizamos.

Ejemplos:


| Acción                                        | Método y ruta (= Endpoint)  |
| --------------------------------------------- | --------------------------- |
| Obtener todos los usuarios                    | `GET /usuarios`             |
| Obtener todos los usuarios mayores de 18 años | `GET /usuarios?edadMin=18`  |
| Obtener la segunda página de usuarios         | `GET /usuarios?page=2`      |
| Obtener usuarios ordenados por nombre         | `GET /usuarios?sort=nombre` |
| Obtener un usuario específico                 | `GET /usuarios/{id}`        |
| Crear un usuario                              | `POST /usuarios`            |
| Actualizar completamente un usuario           | `PUT /usuarios/{id}`        |
| Actualizar parcialmente un usuario            | `PATCH /usuarios/{id}`      |
| Eliminar un usuario                           | `DELETE /usuarios/{id}`     |






## HTTP Estructuras

### Request

```txt
Request HTTP
├─ Request Line
│  ├─ Método
│  ├─ Ruta
│  └─ Versión HTTP
├─ Headers
└─ Body

Endpoint = Método + Ruta
```

Ejemplo de cómo se ve:

```http
POST /usuarios HTTP/1.1
Content-Type: application/json
Authorization: Bearer abc123

{
  "nombre": "Ana",
  "edad": 25
}
```


## Response

```txt
Response HTTP
├─ Status Line
│  ├─ Versión HTTP
│  ├─ Status Code
│  └─ Status Message
├─ Headers
└─ Body
```


Ejemplo de cómo se ve:
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 5,
  "nombre": "Ana",
  "edad": 25
}
```

### Status Line

#### Método y Ruta

Siguiendo REST, serían algo como:

| Acción                                        | Método y ruta (= Endpoint)  |
| --------------------------------------------- | --------------------------- |
| Obtener todos los usuarios                    | `GET /usuarios`             |
| Obtener todos los usuarios mayores de 18 años | `GET /usuarios?edadMin=18`  |
| Obtener la segunda página de usuarios         | `GET /usuarios?page=2`      |
| Obtener usuarios ordenados por nombre         | `GET /usuarios?sort=nombre` |
| Obtener un usuario específico                 | `GET /usuarios/{id}`        |
| Crear un usuario                              | `POST /usuarios`            |
| Actualizar completamente un usuario           | `PUT /usuarios/{id}`        |
| Actualizar parcialmente un usuario            | `PATCH /usuarios/{id}`      |
| Eliminar un usuario                           | `DELETE /usuarios/{id}`     |



#### Versión

Express y Node suelen usar HTTP/1.1, es algo que manejan internamente.


#### Status Code - Solo de Response
Los status codes indican el resultado de la solicitud. Cada Status Code tiene su Status Message.
El ejemplo más famoso es Status code: `404` y mensaje `Not Found`


[Codes y Messages](https://www.w3schools.com/tools/tool_http_status.php)


### Headers
Los headers contienen información adicional sobre la solicitud o la respuesta.

| Header | Función |
|----------|----------|
| Content-Type | Indica el tipo de dato enviado. |
| Authorization | Envía credenciales o tokens. |
| Accept | Indica qué tipo de respuesta acepta el cliente. |
| User-Agent | Identifica al cliente que realiza la petición. |

### Body

El body contiene los datos que se desean enviar en formato JSON generalmente.

Se utiliza principalmente en métodos como POST, PUT o PATCH.


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






