
<br><br>

### Table of Contents

<br>

[APIs](#APIs)
- [Definición](#Definición)
- [Comunicación](#Comunicación)
    - [HTTP](#HTTP)
- [Resumen](#Resumen)

<br>

---

<br>

## APIs

<br>

### Definición

<br>

Una API (Application Programming Interface) es un conjunto de reglas que permite que dos aplicaciones se comuniquen e intercambien información.

<br>

Actúa como intermediaria entre un cliente que realiza una solicitud y un servidor que procesa la solicitud y devuelve una respuesta.

<br>

La API es la "puerta de entrada" que utiliza el cliente para acceder a los recursos del servidor.

<br><br><br><br>

### Comunicación

<br>

El cliente envía una request a través de la API.

El servidor recibe la request, ejecuta la lógica necesaria (consultar una base de datos, realizar cálculos, validar datos, etc.) y devuelve una response.

Pero, ¿cómo se aseguran de que se entienden?

Del mismo modo que dos personas necesitan acordar un idioma para comunicarse, los sistemas necesitan acordar un conjunto de reglas para comunicarse llamado protocolo.

Por ejemplo, un francés puede intentar hablar con un alemán, pero si no establecen un idioma común (por ejemplo, inglés) no podrán entenderse correctamente.

<br><br>

#### HTTP

<br>

Siguiendo con la analogía, en la web ese "idioma" suele ser HTTP (HyperText Transfer Protocol).

HTTP es el protocolo utilizado para intercambiar información entre clientes y servidores. Define las reglas que ambos deben seguir para comunicarse correctamente, incluyendo cómo se construyen las requests y responses, qué métodos pueden utilizarse (GET, POST, PUT, etc.) y cómo se representan los datos intercambiados.

<br><br><br><br>

### Resumen

<br><br>

Entonces:
- **Cliente:** aplicación que solicita información o realiza una acción.
- **Servidor:** aplicación que recibe la solicitud, la procesa y devuelve una respuesta.
- **API (Application Programming Interface):** interfaz que define cómo dos sistemas pueden comunicarse e intercambiar información.
- **API vs Backend:** la API es la interfaz de comunicación; el backend es la aplicación que implementa la lógica de negocio. Una API suele formar parte del backend.
- **HTTP (HyperText Transfer Protocol):** protocolo que define las reglas para intercambiar información entre clientes y servidores mediante requests y responses.
- **Request:** mensaje enviado por el cliente al servidor para solicitar una operación o información.
- **Response:** mensaje enviado por el servidor al cliente con el resultado de procesar una request.

<br><br>

En este caso, se usará:
- Cliente = Navegador = Frontend = HTML, CSS y JS
- Backend = Servidor = Node.js + Express.js
- Protocolo = HTTP

<br><br>

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

<br><br>

Por ejemplo:
1. El usuario hace click en "Ver usuarios".
2. El frontend / cliente envía una HTTP Request a la API.
3. La API ejecuta lógica en el backend / servidor.
4. El backend consulta PostgreSQL.
5. PostgreSQL devuelve datos.
6. El backend genera una HTTP Response.
7. La API la envía al frontend / cliente.
8. El frontend / cliente muestra los datos.

<br><br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>

















