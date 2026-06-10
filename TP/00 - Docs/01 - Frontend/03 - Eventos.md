
<br><br>

### Table of Contents

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
