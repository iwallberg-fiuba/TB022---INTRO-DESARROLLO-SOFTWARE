<br><br>

### Table of Contents

<br>

[El DOM](#El-DOM)
- [Flujo DOM](#Flujo-DOM)

Eventos
- pending 

[Renderizado](#Renderizado)
- [CSR](#CSR)
- [SSR](#SSR)
- [Comparación](#Comparación)

<br><br>

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

```
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

### Event Listeners
### Object Event
### preventDefault
### Propagation
### stopPropagation
### Delegación de Eventos


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
