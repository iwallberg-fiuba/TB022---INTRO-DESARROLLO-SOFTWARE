


## HTTP Estructuras

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

Los métodos HTTP indican qué acción desea realizar el cliente sobre un recurso.

| Método | Función |
|----------|----------|
| GET | Obtener información |
| POST | Crear información |
| PUT | Reemplazar información existente |
| PATCH | Modificar parcialmente información existente |
| DELETE | Eliminar información |


Recordar que URL es todo el link y ruta es la parte final:

```txt
https://api.ejemplo.com/usuarios
│       │              │
│       │              └─ Ruta (path)
│       └─ Dominio
└─ Protocolo
```

Los endpoints son la combinación de método y ruta.

| Acción | Método y ruta (=Endpoint) |
|----------|----------|
| Obtener todos los usuarios | `GET /usuarios` |
| Obtener un usuario | `GET /usuarios/5` |
| Crear un usuario | `POST /usuarios` |
| Actualizar un usuario | `PATCH /usuarios/5` |
| Eliminar un usuario | `DELETE /usuarios/5` |





Headers
Los headers contienen información adicional sobre la solicitud o la respuesta.

| Header | Función |
|----------|----------|
| Content-Type | Indica el tipo de dato enviado. |
| Authorization | Envía credenciales o tokens. |
| Accept | Indica qué tipo de respuesta acepta el cliente. |
| User-Agent | Identifica al cliente que realiza la petición. |



Status
Los status codes indican el resultado de la solicitud. Cada Status Code tiene su Status Message.
El ejemplo más famoso es Status code: `404` y mensaje `Not Found`


[Codes y Messages](https://www.w3schools.com/tools/tool_http_status.php)



### Body

El body contiene los datos que se desean enviar.

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






