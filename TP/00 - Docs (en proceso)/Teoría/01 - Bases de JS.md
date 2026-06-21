
<br><br>

### Table of Contents

<br>

- [Notas](#notas)
- [Variables](#variables)
- [Tipos Primitivos](#tipos-primitivos)
- [Tipos Compuestos](#tipos-compuestos)
- [Estructuras de Control](#estructuras-de-control)
- [Funciones](#funciones)
- [Módulos](#módulos)
- [Ejercicio 1](#ejercicio-1)
- [Ejercicio 2](#ejercicio-2)


<br><br>

---

<br>

## Notas

<br>

- Ejecutar un archivo JavaScript: `node archivo.js` (siendo el nombre del archivo el 1er parámetro)
- Con parámetros adicionales: `node archivo.js argumento`
- El punto y coma `;` es opcional en JavaScript. Se recomienda ser consistente: usarlo siempre o no usarlo nunca.
- Las variables en JavaScript funcionan de forma diferente a las de muchos otros lenguajes. Se declaran con `const`, `let` o `var` (nunca usar `var`). Una variable declarada con `const` es no-mutable, es decir, no puede ser reasignada una vez definida (aunque si contiene un objeto o un array, su contenido sí puede modificarse). Por otro lado, las variables declaradas con `let` son mutables, es decir, pueden cambiar de valor durante la ejecución del programa (de forma similar a las variables tradicionales de otros lenguajes).
- El `==` en JavaScript es diferente. Preferir siempre `===` en lugar de `==`, ya que `===` compara valor y tipo de dato, mientras que `==` intenta convertir tipos antes de comparar (además de ser más lento). Es decir, el `===` funciona como el `==` del resto de los lenguajes de programación.

<br>

```js
5 === "5" // false
5 == "5"  // true
```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Variables

<br>

Las variables viven en el entorno en el que son declaradas.

<br>

```js
// Mutables

let edad = 20;

// var: Nunca usar.


// No mutables

const numero = 10;

const numero = 30;

console.log("numero", numero);

// Error: una constante no puede reasignarse.
// numero = 10;

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Tipos Primitivos

<br>

Los tipos de datos tienen métodos y operadores propios.

<br>

```js
// Strings
const nombre = "Juan";
const apellido = "Pérez";
const nombreCompleto = nombre + " " + apellido;
console.log("nombreCompleto", nombreCompleto);
console.log("El nombre completo de juan tiene", nombreCompleto.length, "letras");

// Para saber si una cadena de texto contiene otra cadena de texto
console.log("nombreCompleto.includes('Juan')", nombreCompleto.includes ("Juan") ) ;

// Orden alfabético
console.log("Juan > Pedro", "Juan" > "Pedro");


// Numbers (enteros y flotantes)
const edad = 19;
const altura = 1.72;
const temperatura = -5.5;


// Booleans

const aprobado = true;
const conectado = false;

// null

const usuario = null;
const fechaNacimiento = null;

// undefined

let direccion;
console.log(direccion); // Imprimiría "undefined" o "error", porque si bien la variable existe, no tiene un valor asignado aún.

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Tipos Compuestos

<br>

Los tipos de datos tienen métodos y operadores propios.

<br>

```js
// Arreglos
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log("array", array);
console.log("array[0]", array[0]);
console.log("array.length", array.length)

const soloPares = array.filter((elemento) => elemento % 2 === 0);
console.log("solo_pares", soloPares) ;

const cantidadDePares = array.filter((elemento) => elemento % 2 === 0).length;
console.log("cantidad_de_pares", cantidadDePares) ;

const arrayMultiplicadoPorDos = array.map((elemento) => elemento * 2);
console.log("array_multiplicado_por_dos", arrayMultiplicadoPorDos);
console.log("arrayOriginal", array);



// Objetos: agrupan variables.

const objeto = {
  nombre: "Juan",
  apellido: "Pérez",
  edad: 30,
  ciudad: "Bragado",
};

console.log("objeto", objeto);

// 2 formas de acceder
console.log("objeto.nombre", objeto.nombre);
console.log("objeto[nombre]", objeto["nombre"]);


// Podemos componer objetos con arrays
const alumno = {
  nombre: "Juan",
  apellido: "Pérez",
  edad: 30,
  ciudad: "Bragado",
  materias: ["Matemáticas", "Física", "Química"],
};

console.log ("alumno", alumno);

// Y al mismo tiempo, podemos hacer un arreglo de objetos
const alumno2 = {
  nombre: "Pedro",
  apellido: "Gómez",
  edad: 25,
  ciudad: "Buenos Aires",
  materias: ["Matemáticas", "Física", "Química"],
};

const materia = [alumno, alumno2]

console.log ("materia", materia);

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Estructuras de Control

<br>

```js
// Estructuras de control.

// Ejemplo de IF

console.log("Ejemplo de if");
const edad = parseInt(process.argv[2]);
// Primer argumento: archivo
// Segundo argumento: edad
// ejemplo: node archivo.js 18

if (edad >= 18) {
  console.log("Eres mayor de edad");
}
  
if (edad < 18) {
  console.log("Eres menor de edad");
}

// Ejemplo de IF-ELSE

console.log("Ejemplo de if-else");

if (edad >= 18) {
  console.log("Eres mayor de edad");
} else {
  console.log("Eres menor de edad");
}

// Ejemplo de for

console.log("Ejemplo de for");

for (let i = 0; i < edad; i++) {
  console.log("Hola Mundo");
}

// Ejemplo de while
console.log("Ejemplo de while");

let i = 0;
while (i < edad) {
  console.log("Hola Mundo");
  i++;
}

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Funciones

<br>

Hay 2 formas de definir funciones:
1. Declarándola
2. Usando "flecha" (arrow function)

<br>

```js
// 1. Declarando la funcion
// (forma explícita)
function suma(a, b) {
  return a + b;
}
console.log("suma(2,3)", suma(2,3));

// (forma implícita)
const hola = (saludo) => console.log(saludo)

hola("Nico como estas?")



// 2. Usando una funcion "flecha" (arrow function)
const suma2 = (a, b) => {
  return a + b;
}

console.log("suma2(2,3)", suma2(2,3));

// Adentro de una funcion, podemos hacer todo lo que queramos!
// Pero tengamos en cuenta que tienen su propio scope (dentro del scope de la aplicación)

// Mala práctica:
let nombre = "Juan";
function saludar() {
  let nombre_bis = "Pedro";
  console.log("Hola " + nombre);
  console.log("Hola " + nombre_bis);
}
saludar();

// console.log(nombre_bis); no funcionaría al no estar dentro de la función.
console.log(nombre);

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Módulos

<br>

### Exportar

<br>

```js
// Documentación

/**
* @param {*} n, número hasta el cual se suman los números
* @returns la suma de los números desde 1 hasta n
*/


// La función a exportar:

export const sumatoria = (n) => {
  let suma = 0;
  for (let i = 1; i <= n; i++) {
    suma += i;
    return suma;
}

```

<br>

### Importar

<br>

```js
import { sumatoria } from "./sumatoria.js";

// Importa la función sumatoria del archivo "./sumatoria.js"

const n = 10;
const resultado = sumatoria(n);
console.log(`La suma de los numeros desde 1 hasta ${n} es ${resultado} );
```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Ejercicio 1

<br>

Implementar una funcion que reciba un array de alumnos (Compuesto por nombre, apellido y notas)
y devuelva todos los alumnos que esten aprobados (Promedio de nota mayor a 4).

<br>

```js
import { alumnos } from "./alumnos.js";

// Ejercicio 1:
// Implementar una funcion que reciba un array de alumnos (Compuesto por nombre, apellido y notas)
// y devuelva todos los alumnos que esten aprobados (Promedio de nota mayor a 4).

const alumnoAprobado = (alumno) => {
  const totalNotas = alumno.notas.length;

  // const sumatoria = alumno.notas. reduce((a, b) => a +b, 0)
  let sumatoria = 0;
  for (let i = 0; i < totalNotas; i++) {
    sumatoria += alumno.notas[i]
  }
    return (sumatoria/totalNotas) >= 4
}

// Devolver los alumnos aprobados (>=4)
const aprobados = (alumnos) => {
  return alumnos.filter( (x) => alumnoAprobado(x))
}

console.log("Los alumnos aprobados son:")
console.log(aprobados(alumnos))

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>

## Ejercicio 2

<br>

Implementar una funcion que reciba un numero(n) y una lista de alumnos.
Debe devolver los primeros n alumnos de la lista.

<br>

```js
import { alumnos } from "./alumnos.js";

// Ejercicio 2:
// Implementar una funcion que reciba un numero(n) y una lista de alumnos.
// Debe devolver los primeros n alumnos de la lista.

const calcularPromedio = (alumno) => {
  const totalNotas = alumno.notas.length;
  
  // const sumatoria = alumno.notas.reduce((a, b) => a +b, 0)
  let sumatoria = 0;
  for (let i = 0; i < totalNotas; i++) {
    sumatoria += alumno.notas[i]
  }
  return (sumatoria/totalNotas);
}

const compararAlumnos = (a,b) => {
  return calcularPromedio(b) - calcularPromedio(a)
}

const ordenarPorPromedio = (alumnos) => {
  return alumnos.sort( (a,b) => compararAlumnos(a,b) )
}

console.log("alumnos, ordenados", ordenarPorPromedio(alumnos))

const primerosAlumnos = (alumnos, n) => {
  const alumnosOrdenados = ordenarPorPromedio(alumnos);
  return alumnosOrdenados.slice(0, n)
}

console.log(primerosAlumnos (alumnos, 1))

```

<br>

<br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br><br>



