
<br><br>

`Pending.`

### Table of Contents

<br>







<br><br>

---

<br>



## APIs

### Definición

Una API (Application Programming Interface) es un conjunto de reglas que permite que dos aplicaciones se comuniquen e intercambien información.

Actúa como intermediaria entre un cliente que realiza una solicitud y un servidor que procesa la solicitud y devuelve una respuesta.

La API es la "puerta de entrada" que utiliza el cliente para acceder a los recursos del servidor.


### Comunicación

El cliente envía una petición (*request*) a través de la API.

El servidor recibe la petición, ejecuta la lógica necesaria (consultar una base de datos, realizar cálculos, validar datos, etc.) y devuelve una respuesta (*response*).

Pero, como asegurarse de que se entienden?
Ejemplo:
Un frances puede intentar hablar con un alemán, pero si no establecen un protocolo (ej: hablar en ingles, que ambos saben) no se van a entender.

#### HTTP

Ahí entra HTTP. HTTP (HyperText Transfer Protocol) es el protocolo utilizado para intercambiar información entre clientes y servidores en la web. Define cómo se envían las solicitudes y cómo se reciben las respuestas.

Entonces:
 **Cliente:** aplicación que solicita información o realiza una acción.
- **Servidor:** aplicación que recibe la solicitud, la procesa y devuelve una respuesta.
- API
- API vs Backend
- HTTP
- Request
- Response

En este caso, se usará:
- Cliente = Navegador = Frontend = HTML, CSS y JS
- Backend = Servidor = Node.js + Express.js
- Protocolo = HTTP

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

Por ejemplo:
1. El usuario hace click en "Ver usuarios".
2. El frontend / cliente envía una HTTP Request a la API.
3. La API ejecuta lógica en el backend / servidor.
4. El backend consulta PostgreSQL.
5. PostgreSQL devuelve datos.
6. El backend genera una HTTP Response.
7. La API la envía al frontend / cliente.
8. El frontend / cliente muestra los datos.




















