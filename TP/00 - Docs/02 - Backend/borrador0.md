
`Pending.`

```txt
JavaScript
├─ Single Thread
├─ Call Stack
├─ Código Síncrono
├─ Código Asíncrono
│   ├─ Web APIs / Node APIs
│   ├─ Task Queue
│   ├─ Microtask Queue
│   └─ Event Loop
└─ Técnicas de Asincronía
    ├─ Callbacks
    ├─ Promises
    └─ async / await
```

---

## Single Thread

JavaScript es *single-threaded*, es decir, el código JavaScript se ejecuta en un único hilo principal (*main thread*).

Por eso sólo puede ejecutar una instrucción a la vez.

```js
console.log("A");
console.log("B");
console.log("C");
```

```txt
Salida Esperada:

A
B
C
```

No puede ejecutar A y B simultáneamente.

---

## Call Stack

La Call Stack (pila de llamadas) es una estructura donde JavaScript guarda las funciones que está ejecutando.

Cada vez que una función comienza a ejecutarse, entra en la pila.

Cuando termina, sale de la pila.

```js
function saludar() {
    console.log("Hola");
}

saludar();
```

```txt
Call Stack

saludar()
↓
console.log()
↓
vacía
```

JavaScript siempre ejecuta primero lo que está arriba de la pila.

---

## Código Síncrono

En el código síncrono las instrucciones se ejecutan una después de otra, en orden.

JavaScript no comienza una instrucción hasta haber terminado la anterior.

```js
console.log("A");
console.log("B");
console.log("C");
```

```txt
Salida Esperada:

A
B
C
```

---

## Código Asíncrono

Algunas tareas pueden tardar mucho tiempo:

- Consultar una API.
- Leer un archivo.
- Consultar una base de datos.
- Esperar una acción del usuario.

Si JavaScript esperara de forma síncrona, toda la aplicación quedaría bloqueada.

Por eso existe la asincronía.

La asincronía es posible porque el entorno donde corre JavaScript (navegador o Node.js) dispone de componentes externos capaces de trabajar en paralelo.

```txt
JavaScript (1 hilo)
│
├─ Web APIs (Browser)
├─ Node APIs (Node.js)
├─ Sistema Operativo
└─ Red
```

Por ejemplo:

```js
setTimeout(() => {
    console.log("Hola");
}, 5000);
```

JavaScript no se queda contando 5 segundos.

Hace algo parecido a:

```txt
JavaScript
↓
"Browser, avisame en 5 segundos"
↓
Sigue ejecutando código
```

El navegador o Node.js se encargan del temporizador.

Cuando termina, el callback queda esperando para ser ejecutado.

---

### Task Queue

La Task Queue (cola de tareas) almacena callbacks listos para ejecutarse.

Por ejemplo:

```js
setTimeout(() => {
    console.log("Hola");
}, 5000);
```

Flujo:

```txt
setTimeout()
↓
Web API / Node API
↓
Termina el temporizador
↓
Task Queue
```

Las tareas permanecen allí hasta que JavaScript pueda ejecutarlas.

---

### Microtask Queue

Existe una cola especial llamada Microtask Queue.

Se utiliza principalmente para:

- Promises
- async / await
- queueMicrotask()

```txt
Microtask Queue
↓
Promises
async / await
```

Tiene prioridad sobre la Task Queue.

---

### Event Loop

El Event Loop es el mecanismo que coordina la ejecución de tareas asíncronas.

Su trabajo consiste en comprobar continuamente si la Call Stack está vacía.

Si está vacía:

1. Ejecuta primero las tareas de la Microtask Queue.
2. Luego ejecuta las tareas de la Task Queue.

```txt
Call Stack
↓
¿Vacía?
↓ Sí
Microtask Queue
↓
Task Queue
↓
Ejecutar tarea
```

Ejemplo:

```js
console.log("Inicio");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("Fin");
```

```txt
Salida Esperada:

Inicio
Fin
Timer
```

Aunque el timeout sea 0.

Flujo:

```txt
console.log("Inicio")
↓
setTimeout(...)
↓
console.log("Fin")
↓
Call Stack vacía
↓
Event Loop toma callback
↓
console.log("Timer")
```

---

#### Prioridad de Microtasks

```js
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

```txt
Salida Esperada:

A
D
C
B
```

Flujo:

```txt
Call Stack
↓
Microtask Queue
↓
Task Queue
```

Por eso la Promise se ejecuta antes que el setTimeout.

---

## Técnicas de Asincronía

A lo largo de la evolución de JavaScript aparecieron distintas formas de trabajar con operaciones asíncronas.

```txt
Código Asíncrono
↓
Callbacks
↓
Promises
↓
async / await
```

---

### Callbacks

Un callback es una función que se pasa como argumento para ejecutarse más tarde.

```js
setTimeout(() => {
    console.log("Hola");
}, 1000);
```

La función:

```js
() => {
    console.log("Hola");
}
```

es el callback.

Flujo:

```txt
setTimeout()
↓
Se registra el callback
↓
JavaScript sigue ejecutando código
↓
Termina el temporizador
↓
Task Queue
↓
Event Loop
↓
Se ejecuta el callback
```

#### Problema: Callback Hell

Cuando varias operaciones asíncronas se anidan unas dentro de otras.

```js
paso1(() => {
    paso2(() => {
        paso3(() => {
            paso4(() => {
                console.log("Fin");
            });
        });
    });
});
```

El código se vuelve difícil de leer y mantener.

---

### Promises

Una Promise representa un resultado que estará disponible en el futuro.

Estados posibles:

```txt
Pending
├─ Fulfilled
└─ Rejected
```

- Pending: todavía no terminó.
- Fulfilled: terminó correctamente.
- Rejected: ocurrió un error.

Ejemplo:

```js
const promesa = fetch("/usuarios");
```

JavaScript recibe la Promise inmediatamente y continúa ejecutando otras instrucciones.

---

#### then()

Se ejecuta cuando la Promise se resuelve correctamente.

```js
fetch("/usuarios")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    });
```

---

#### catch()

Se ejecuta cuando ocurre un error.

```js
fetch("/usuarios")
    .then(response => response.json())
    .catch(error => {
        console.error(error);
    });
```

---

#### Flujo

```txt
Promise
↓
Pending
├─ Fulfilled → then()
└─ Rejected → catch()
```

---

### async / await

async / await es una sintaxis más moderna para trabajar con Promises.

Internamente sigue utilizando Promises.

---

#### Con Promises

```js
fetch("/usuarios")
    .then(response => response.json())
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error(error);
    });
```

---

#### Con async / await

```js
async function obtenerUsuarios() {
    try {
        const response = await fetch("/usuarios");
        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

---

#### await

`await` pausa la ejecución de la función `async` hasta que la Promise termine.

```js
const response = await fetch("/usuarios");
```

No bloquea toda la aplicación.

Sólo pausa esa función específica.

---


```txt
JavaScript
↓
Single Thread
↓
Call Stack
↓
Código Síncrono
↓
Código Asíncrono
├─ Web APIs / Node APIs
├─ Task Queue
├─ Microtask Queue
└─ Event Loop
↓
Callbacks
↓
Promises
↓
async / await
```

