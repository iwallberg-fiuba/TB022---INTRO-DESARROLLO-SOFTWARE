




---

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
