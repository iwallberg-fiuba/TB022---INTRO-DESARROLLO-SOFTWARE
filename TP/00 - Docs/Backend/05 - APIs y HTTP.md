

<br><br>

### Table of Contents

<br>

[HTTP Estructuras](#HTTP-Estructuras)
- [Request](#Request)
- [Response](#Response)
- [Status Line](#Status-Line)
  - [Método y Ruta](#Método-y-Ruta)
  - [Versión](#Versión)
  - [Status Codes (Response)](#Status-Codes-Response)
- [Header](#Header)
- [Body](#Body)
- [Flujo HTTP](#Flujo-HTTP)

<br>

---

<br>

## HTTP Estructuras

<br><br>

### Request

<br>

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

<br>

Ejemplo de cómo se ve:

<br>

```http
POST /usuarios HTTP/1.1
Content-Type: application/json
Authorization: Bearer abc123

{
  "nombre": "Ana",
  "edad": 25
}
```

<br><br><br>


### Response

<br>

```txt
Response HTTP
├─ Status Line
│  ├─ Versión HTTP
│  ├─ Status Code
│  └─ Status Message
├─ Headers
└─ Body
```

<br>

Ejemplo de cómo se ve:

<br>

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 5,
  "nombre": "Ana",
  "edad": 25
}
```

<br><br><br><br>

### Status Line

<br>

#### Método y Ruta

<br>

Siguiendo REST, serían algo como:

<br>

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

<br><br><br><br>

#### Versión

<br>

Express y Node suelen usar HTTP/1.1, es algo que manejan internamente.

<br><br><br><br>

#### Status Codes (Response)

<br>

Los status codes indican el resultado de la solicitud. Cada Status Code tiene su Status Message.
El ejemplo más famoso es Status code: `404` y mensaje `Not Found`

<br>

[Codes y Messages](https://www.w3schools.com/tools/tool_http_status.php)

<br><br><br><br>

### Headers

<br>

Los headers contienen información adicional sobre la solicitud o la respuesta.

<br>

| Header | Función |
|----------|----------|
| Content-Type | Indica el tipo de dato enviado. |
| Authorization | Envía credenciales o tokens. |
| Accept | Indica qué tipo de respuesta acepta el cliente. |
| User-Agent | Identifica al cliente que realiza la petición. |

<br><br><br><br>

### Body

<br>

El body contiene los datos que se desean enviar en formato JSON generalmente.

Se utiliza principalmente en métodos como POST, PUT o PATCH.

<br><br><br><br>

### Flujo HTTP

<br>

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

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

