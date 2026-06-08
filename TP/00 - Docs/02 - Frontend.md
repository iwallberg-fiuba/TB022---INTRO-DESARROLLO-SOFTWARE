<br><br>

### Table of Contents

<br>

[El DOM](#El-DOM)
- [Flujo DOM](#Flujo-DOM)

<br>

[Eventos](#Eventos)
- [Event Listeners](#Event-Listeners)
- [Objecto Event](#Objeto-Event)
- [preventDefault](#preventDefault)
- [Propagation](#Propagation)
- [stopPropagation](#stopPropagation)
- [Delegación](#Delegación)
- [Relación con el DOM](#Relación-con-el-DOM)

<br>

[Renderizado](#Renderizado)
- [CSR](#CSR)
- [SSR](#SSR)
- [Comparación](#Comparación)

<br>

---

<br>

## El DOM

<br>

El DOM es la representación del HTML que el navegador crea en memoria para que JavaScript pueda leerlo y modificarlo.

<br>

```html
<body>
    <h1 id="titulo">Hola</h1>
    <button class="btn">Click</button>
</body>
```

<br>

Se transforma internamente en algo parecido a:

<br>

```txt
document
└─ html
   └─ body
      ├─ h1#titulo
      └─ button.btn
```

<br>

JavaScript busca elementos dentro de ese árbol:

<br>

```js
const titulo = document.getElementById("titulo");
const boton = document.querySelector(".btn");
```

<br>

Y puede modificarlos:

<br>

```js
titulo.textContent = "Texto cambiado";
```

<br>

Resultado:

<br>

```html
<h1 id="titulo">Texto cambiado</h1>
```

<br><br><br>

### Flujo DOM

<br>

```txt
HTML
↓
El navegador crea el DOM
↓
Usuario interactúa
↓
JavaScript recibe el evento
↓
JavaScript busca y modifica elementos del DOM
↓
El navegador actualiza la pantalla
```

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

## Eventos

<br>

Los eventos son mecanismos que permiten que JavaScript detecte acciones o cambios ocurridos en la página y ejecute código en respuesta.

<br>

```txt
Usuario o navegador realiza una acción
↓
Se dispara un evento
↓
JavaScript lo detecta
↓
Ejecuta una función
↓
Puede modificar el DOM
↓
El navegador vuelve a renderizar la página
```

<br>

```txt
Eventos
├─ Event Listeners
├─ Objeto Event
├─ preventDefault()
├─ Propagación (Bubbling)
├─ stopPropagation()
└─ Delegación de eventos

Eventos más comunes:
- Mouse: click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave.
- Teclado: keydown, keyup.
- Formularios: submit, input, change, focus, blur.
- Ventana y documento: load, resize, scroll.
```

<br><br><br><br>

### Event Listeners

<br>

Los event listeners ("escuchadores de eventos") permiten asociar una función a un evento específico.

<br>

```js
boton.addEventListener("click", () => {
    console.log("Click detectado");
});
```

<br>

```txt
Evento
↓
Listener
↓
Función
```

<br><br><br><br>

### Object Event

<br>

Cuando ocurre un evento, JavaScript crea automáticamente un objeto Event con información sobre lo sucedido. <br>
Esa información puede verse usando `console.log`.

<br>

Se muestran datos como:
- Elemento que disparó el evento.
- Posición del mouse.
- Tecla presionada.
- Tipo de evento.
- Momento en que ocurrió.

<br>

```js
boton.addEventListener("click", (event) => {
    console.log(event);
});
```

<br>

```txt
Evento
↓
Objeto Event
↓
Información del evento
```

<br><br><br><br>

### preventDefault

<br>

Impide que el navegador ejecute la acción predeterminada asociada a un evento.

<br>

```js
formulario.addEventListener("submit", (e) => {
    e.preventDefault();
});
```

<br><br><br>

Sin `preventDefault()`:

<br>

```txt
Submit
↓
Se envía el formulario
↓
La página se recarga
```

<br><br>

Con `preventDefault()`:

<br>

```txt
Submit
↓
JavaScript toma el control
↓
No hay recarga
```

<br><br><br><br>

### Propagation

<br>

Propagación de Eventos (Event Bubbling). <br>

Los eventos no ocurren solamente sobre el elemento clickeado. <br>

Después de ejecutarse en ese elemento, el evento se propaga hacia sus contenedores padres.

<br>

```txt
document
└─ body
   └─ div
      └─ button
```

<br>

Entonces un click en el botón es:

<br>

```txt
button
↓
div
↓
body
↓
document
```

<br>

A esto se lo llama bubbling.

<br><br><br><br>


### stopPropagation

<br>

Detiene la propagación del evento.

<br>

```js
e.stopPropagation();
```

<br>

```txt
button
↓
(stopPropagation)
↓
La propagación termina
```

<br><br><br><br>

### Delegación de Eventos

<br>

Consiste en colocar un único listener en un contenedor y aprovechar la propagación para detectar eventos ocurridos en sus hijos. <br>

Permite que el funcionamiento sea dinámico. <br>

En lugar de tener 100 botones para 100 eventos, se utiliza:

<br>

```HTML
<ul id="lista">
    <li>Uno</li>
    <li>Dos</li>
    <li>Tres</li>
</ul>
```

<br>

```js
const lista = document.getElementById("lista");

lista.addEventListener("click", (event) => {
    console.log(event.target.textContent);
});
```

<br>

```txt
Click en li
↓
Evento ocurre en li
↓
Bubbling
↓
Llega al ul
↓
El listener del ul se ejecuta
↓
event.target indica qué li fue clickeado.
Si el clickeado fue "Dos", entonces event.target vale <li>Dos</li>
```

<br>

```txt
Hijo recibe el click
↓
El evento sube (bubbling)
↓
Padre lo captura
↓
event.target identifica al hijo original
```

<br><br><br><br>

### Relación con el DOM

<br>

Los eventos y el DOM trabajan juntos constantemente.

<br>

```txt
DOM
↓
Evento
↓
JavaScript
↓
Modificación del DOM
↓
Renderizado
```

<br>

Ejemplo:

<br>

```txt
Usuario hace click
↓
Evento click
↓
JavaScript cambia un texto
↓
El DOM se actualiza
↓
La pantalla cambia
```

<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

## Renderizado

<br>

Renderizar es el proceso de generar lo que ve el usuario en pantalla.

<br>

```txt
Datos + HTML + CSS + JavaScript
↓
Navegador
↓
Página visible
```

<br><br><br>

### CSR

<br>

Client-Side Rendering. El renderizado ocurre en el navegador del usuario.

<br>

```txt
Usuario entra a la página
↓
Servidor envía HTML casi vacío + JavaScript
↓
Se descarga y ejecuta JavaScript
↓
JavaScript obtiene datos
↓
JavaScript construye la interfaz
↓
Se muestra la página
```

<br>

### Ejemplo

<br>

Servidor devuelve:

<br>

```HTML
<body>
  <div id="app"></div>
  <script src="app.js"></script>
</body>
```

<br>

JavaScript responde:

<br>

```js
document.getElementById("app").innerHTML =
  "<h1>Hola</h1>";
```

<br><br>

| Categoría   | Detalles                                               |
| ----------- | ------------------------------------------------------ |
| Ventajas    | Interfaces muy interactivas                            |
|             | Menos trabajo para el servidor                         |
|             | Navegación rápida una vez cargada la aplicación        |
| Desventajas | Primera carga más lenta                                |
|             | Peor SEO                                               |
|             | El usuario puede ver una pantalla vacía mientras carga |
| Tecnologías | React                                                  |
|             | Vue                                                    |
|             | Angular                                                |
|             | Svelte                                                 |


<br><br><br>

### SSR

<br>

Server-Side Rendering. El renderizado ocurre en el servidor.

<br>

```txt
Usuario entra a la página
↓
Servidor obtiene datos
↓
Servidor genera HTML completo
↓
Envía HTML al navegador
↓
La página aparece inmediatamente
```

<br>

### Ejemplo

<br>

El servidor genera:

<br>

```HTML
<body>
  <h1>Hola</h1>
</body>
```

<br>

El navegador solo tiene que mostrarlo.

<br><br>

| Categoría   | Detalles                                         |
| ----------- | ------------------------------------------------ |
| Ventajas    | Primera carga más rápida                         |
|             | Mejor SEO                                        |
|             | El usuario ve contenido antes                    |
| Desventajas | Más trabajo para el servidor                     |
|             | Cada página requiere procesamiento en el backend |
| Tecnologías | Next.js                                          |
|             | Nuxt                                             |
|             | SvelteKit                                        |
|             | Django Templates                                 |
|             | Laravel Blade                                    |


<br><br><br><br>

### Comparación

<br>

| Aspecto            | CSR        | SSR                |
| ------------------ | ---------- | ------------------ |
| Dónde se renderiza | Navegador  | Servidor           |
| HTML inicial       | Casi vacío | Completo           |
| Primera carga      | Más lenta  | Más rápida         |
| SEO                | Peor       | Mejor              |
| Carga del servidor | Menor      | Mayor              |
| Interactividad     | Excelente  | Excelente (con JS) |


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>
