
<br><br>

### Table of Contents

<br>

[HTML](#HTML)

<br>

[CSS](#CSS)

<br>

- [Selectores CSS](#Selectores-CSS)
  - [Por Clase en CSS](#Por-Clase-en-CSS)
  - [Por Etiqueta en CSS](#Por-Etiqueta-en-CSS)
  - [Por ID en CSS](#Por-ID-en-CSS)

<br>

[JavaScript](#JavaScript)
- [Selectores JS](#Selectores-JS)
  - [Por Clase en JS](#Por-Clase-en-JS)
  - [Por Etiqueta en JS](#Por-Etiqueta-en-JS)
  - [Por ID en JS](#Por-ID-en-JS)
- [Ejemplo](#Ejemplo)

<br>

[Tabla Selectores](#Tabla-Selectores)

<br><br>

---

<br>

## HTML

<br>

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mi página</title>

    <!-- Conexión con CSS -->
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>

    <!-- Etiqueta -->
    <h1>
        Título
    </h1>

    <!-- Clase -->
    <button class="btn">
        Click
    </button>

    <!-- ID -->
    <h2 id="titulo-unico">
        Texto único
    </h2>


    <!-- Conexión con JavaScript -->
    <script src="js/app.js"></script>

</body>
</html>
```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

## CSS

<br>

### Selectores CSS

<br>

#### Por Clase en CSS

<br>

```css
.btn {
    background-color: green;
}
```

<br><br>

#### Por ID en CSS

<br>

```css
#titulo-unico {
    color: purple;
}
```

<br><br>

#### Por Etiqueta en CSS

<br>

```css
/* html → documento completo */

html {
    height: 100%;
}

/* body → contenido visible de la página */

body {
    font-family: Arial, sans-serif;
}

/* asterisco → todos los elementos */

* {
    margin: 0;
    padding: 0;
}

/* h3 → todos los h3 */

h3 {
    color: red;
}
```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

## JavaScript

<br>

### Selectores JS

<br>

#### Por Clase en JS

<br>

```js
/* Primer elemento encontrado */
const boton = document.querySelector(".btn");

/* Todos los elementos */
const botones = document.querySelectorAll(".btn");
```

<br><br>

#### Por ID en JS

<br>

```js
const titulo = document.getElementById("titulo-unico");
```

<br><br>

#### Por Etiqueta en JS

<br>

```js
const encabezados = document.querySelectorAll("h3");
```

<br><br><br>

### Ejemplo

<br>

```js
const boton = document.querySelector(".btn");
const titulo = document.getElementById("titulo2");

boton.addEventListener("click", () => {
    titulo.textContent = "Texto cambiado";
});
```

<br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br>

---

<br>

## Tabla Selectores

<br>

| Tipo | HTML | CSS | JavaScript |
|-----------|-----------|-----------|-----------|
| Clase (primer elemento) | `class="btn"` | `.btn` | `querySelector(".btn")` |
| Clase (todos) | `class="btn"` | `.btn` | `querySelectorAll(".btn")` |
| ID | `id="titulo-unico"` | `#titulo-unico` | `getElementById("titulo-unico")` |
| Etiqueta | `<h3>` | `h3` | `querySelectorAll("h3")` |


<br><br><br>

[Volver a Table of Contents](#Table-of-Contents)

<br><br>


