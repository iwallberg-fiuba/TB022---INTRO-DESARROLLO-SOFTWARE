

<br><br>

### Table of Contents

- [Promesas](#promesas)
  - [Importante](#importante)  
- [HTML](#html)
- [Caso 1: then / throw / catch](#caso-1-then--throw--catch)
- [Caso 2: async / await](#caso-2-async--await-y-try--catch)

<br>

---

<br>

## Promesas

<br>

Las promesas permiten trabajar con operaciones que pueden tardar en completarse, sin bloquear el resto de la aplicación.

Mientras se espera que una promesa se resuelva, JavaScript puede seguir ejecutando otras tareas.

Ejemplo:

- Mientras se cargan las publicaciones o el feed de Instagram, igualmente se puede seguir interactuando con la aplicación:
  - Hacer scroll.
  - Abrir mensajes.
  - Navegar a otra sección.
  - Presionar botones.

Si la aplicación tuviera que esperar a que termine la carga antes de hacer cualquier otra cosa, la experiencia de usuario sería mucho peor.

---

<br>

### Importante

<br>

Existen 2 formas de trabajar con promesas:
- Caso 1: usando then-throw-catch
- Caso 2: usando try-catch y async-await (la más famosa)

<br>

Además
- El HTML es exactamente el mismo en ambos casos.
- La lógica de negocio es exactamente la misma en ambos casos.
- La request HTTP es exactamente la misma en ambos casos.
- Lo único que cambia es la forma de escribir el código dentro de la etiqueta `<script>`.


<br><br>

fetch
- fetch() es una función del BOM que permite realizar peticiones HTTP desde JavaScript.
- Su uso más común es pedir información a una API o backend.

<br>

```txt
JavaScript
↓
fetch()
↓
Request HTTP
↓
Backend
↓
Response HTTP
↓
JavaScript
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## HTML

<br>

<br>

```html
<html>
  <body>
    <!-- Contenedor principal -->
    <div class="input-container">
    
      <!-- Input donde el usuario ingresa el número del Pokémon -->
      <input
        type="number"
        id="inputNumerico"
        placeholder="Ingresa un numero..."
      >
    
      <!-- Botón que inicia la búsqueda -->
      <button id="addButton">
        Buscar Pokemon
      </button>
    
      <!-- Título que se actualizará dinámicamente -->
      <h1 id="tituloPokemon"></h1>
    
      <!-- Imagen que se actualizará dinámicamente -->
      <img id="imagenPokemon"/>
    
    </div>

    <script>
      // Código javascript
    </script>

  </body>
</html>
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Caso 1: then / throw / catch

<br>

```js
// URL base de la API.
const pokemonURL = "https://pokeapi.co/api/v2/pokemon/";


// Realiza una request HTTP a la PokeAPI.
// Devuelve una Promise que eventualmente contendrá la respuesta.
const GetPokemon = (numeroABuscar) => {
  return fetch(pokemonURL + numeroABuscar);
};


// Obtiene referencias a elementos del DOM.
const addButton = document.querySelector("#addButton");
const inputNumerico = document.querySelector("#inputNumerico");
const tituloPokemon = document.querySelector("#tituloPokemon");
const imagenPokemon = document.querySelector("#imagenPokemon");


// Se ejecuta cuando el usuario presiona el botón.
addButton.addEventListener("click", () => {

  // Obtiene el valor ingresado por el usuario.
  const pokemonABuscar = inputNumerico.value;


  // Estado de carga.
  // Se muestra mientras se espera la respuesta de la API.
  tituloPokemon.innerHTML = "Cargando...";
  imagenPokemon.src = "link_imagen_cargando";


  // Realiza la request.
  GetPokemon(pokemonABuscar)

    .then((response) => {

      // Verifica si la API respondió con un código HTTP exitoso.
      //
      // Ejemplos:
      // 200 OK  -> true
      // 404 Not Found -> false
      // 500 Internal Server Error -> false
      if (!response.ok) {

        // Convierte el error HTTP en un error JavaScript
        // para que pueda ser manejado por el catch.
        throw new Error(`Error HTTP ${response.status}`);

      }

      // Convierte el JSON recibido a un objeto JavaScript.
      //
      // response.json() también devuelve una Promise.
      return response.json();

    })

    .then((data) => {

      // La Promise anterior se resolvió correctamente.
      // data contiene la información del Pokémon.

      // Actualiza el nombre.
      tituloPokemon.innerHTML = data.species.name;

      // Actualiza la imagen.
      imagenPokemon.src = data.sprites.front_default;

      // Muestra información en consola para depuración.
      console.log(data.species.name);

    })

    .catch((error) => {

      // Manejo de errores.
      //
      // Puede ejecutarse por:
      // - Error HTTP (404, 500, etc.)
      // - Problemas de red
      // - API caída
      // - Errores durante el procesamiento de la respuesta

      tituloPokemon.innerHTML =
        "Oops pokemon no encontrado";

      imagenPokemon.src =
        "link_imagen_error";

      // Muestra el error real en consola.
      console.log(error);

    });

});
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Caso 2: async / await y try / catch

<br>

```js
// Obtiene referencias a elementos del DOM.
const addButton = document.querySelector("#addButton");
const inputNumerico = document.querySelector("#inputNumerico");
const tituloPokemon = document.querySelector("#tituloPokemon");
const imagenPokemon = document.querySelector("#imagenPokemon");


// URL base de la API.
const pokemonURL = "https://pokeapi.co/api/v2/pokemon/";


// Realiza una request HTTP.
// Devuelve una Promise.
const GetPokemon = (numeroABuscar) => {
  return fetch(pokemonURL + numeroABuscar);
};


// Función asíncrona.
// Permite utilizar await dentro de ella.
const addPokemon = async (numeroABuscar) => {

  try {

    // Estado de carga.
    tituloPokemon.innerHTML = "Cargando...";
    imagenPokemon.src = "link_imagen_cargando";


    // Espera la respuesta HTTP.
    const response = await GetPokemon(numeroABuscar);


    // Convierte el JSON a un objeto JavaScript.
    // response.json() también devuelve una Promise.
    const pokemonData = await response.json();


    // Actualiza el DOM con la información recibida.
    tituloPokemon.innerHTML =
      pokemonData.species.name;

    imagenPokemon.src =
      pokemonData.sprites.front_default;

  } catch (e) {

    // Manejo de errores.
    tituloPokemon.innerHTML =
      "Oops pokemon no encontrado";

    imagenPokemon.src =
      "LINK_IMAGEN_ERROR";

  }

};


// Evento click.
addButton.addEventListener("click", () => {

  // Obtiene el número ingresado por el usuario.
  const pokemonABuscar = inputNumerico.value;

  // Ejecuta la función asíncrona.
  addPokemon(pokemonABuscar);

});
```

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>
