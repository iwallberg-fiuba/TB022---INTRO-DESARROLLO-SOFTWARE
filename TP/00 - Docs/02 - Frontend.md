

### Table of Contents



<br>

[El DOM](#El-DOM)
- [Ejemplo DOM](#Ejemplo-DOM)


Eventos
Renderizado
CSR
SSR

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

<br><br>

### Ejemplo DOM

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

<br><br>
