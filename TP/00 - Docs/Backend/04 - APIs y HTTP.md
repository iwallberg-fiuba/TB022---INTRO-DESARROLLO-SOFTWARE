

Antes de ver status line, ver 
- Methods
- REST API
- Ruta
- Endpoints en profundidad

alpine
---


## REST APIs

Una REST API es una forma de organizar una API HTTP alrededor de los recursos (= ENTIDADES DE TU APP), donde las URLs identifican recursos y los métodos HTTP indican las acciones sobre ellos.


### HTTP Methods

Esto existe independientemente de REST, REST sólo arma una convención sobre cómo usarlo en conjunto con los otros elementos HTTP.

| Método   | Acción                   |
| -------- | ------------------------ |
| `GET`    | Obtener datos            |
| `POST`   | Crear datos              |
| `PUT`    | Reemplazar completamente |
| `PATCH`  | Modificar parcialmente   |
| `DELETE` | Eliminar                 |

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

Al sumar Método HTTP + Ruta, obtenemos un Endpoint.

Los Endpoints existen independientemente de REST, REST sólo arma una convención sobre cómo usarlo en conjunto con los otros elementos HTTP.

Ejemplos:

| Acción                              | Método y ruta (= Endpoint) |
| ----------------------------------- | -------------------- |
| Obtener todos los usuarios          | `GET /usuarios`      |
| Obtener un usuario específico       | `GET /usuarios/5`    |
| Crear un usuario                    | `POST /usuarios`     |
| Actualizar completamente un usuario | `PUT /usuarios/5`    |
| Actualizar parcialmente un usuario  | `PATCH /usuarios/5`  |
| Eliminar un usuario                 | `DELETE /usuarios/5` |





---


## HTTP Request

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


## HTTP Response

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






