
<br><br>

`Pending.`

### Table of Contents

<br>

- Compilador
- Runtime
- Node.js
- Paquetes


## APIs

* Qué es una API
* Cliente y servidor
* Intercambio de información
* Ejemplos de APIs

## HTTP

* Qué es HTTP
* Request y Response
* Mensaje HTTP
* Headers
* Body
* Status Codes (200, 404, 500, etc.)

## HTTP Methods y CRUD

* GET → Read
* POST → Create
* PUT/PATCH → Update
* DELETE → Delete

Tabla CRUD ↔ HTTP.

## REST API

* Qué es REST
* Recursos
* Convenciones REST
* URLs
* Stateless

## Endpoints

* Qué es un endpoint
* Parámetros de ruta
* Query parameters
* Ejemplos

```txt
/api/users
/api/users/1
/api/products
```

## Ciclo HTTP completo

```txt
Cliente
↓
HTTP Request
↓
Endpoint
↓
Backend
↓
Base de datos
↓
HTTP Response
↓
Cliente
```



## Promises y asincronía

* Callbacks
* Promises
* then
* catch
* async/await
* fetch


<br><br>

---

<br>

# Conceptos Previos

## Compilador

Toma código escrito por humanos y lo transforma a otro formato que la computadora entiende mejor. No es necesario memorizar los siguientes conceptos pero sí leerlos con atención para entender lo siguiente.

| Concepto              | Definición                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------ |
| Assembly              | Lenguaje de programación de bajo nivel legible por humanos                                 |
| Assembler             | Programa que traduce Assembly a código máquina                                             |
| Código máquina        | Instrucciones entendidas directamente por la CPU                                           |
| Bytecode              | Instrucciones intermedias entendidas por una VM                                            |
| Compilador            | Traduce código fuente a Assembly, bytecode o código máquina                                |
| Intérprete            | Lee y ejecuta instrucciones durante la ejecución del programa                              |
| JIT (Just-In-Time)    | Compila partes del programa a código máquina mientras se ejecuta                           |
| Ejecutable            | Archivo que contiene código listo para ser ejecutado                                       |
| Runtime               | Entorno que ejecuta el programa y le da acceso al sistema                                  |
| VM (Virtual Machine)  | En este caso, describe un software que ejecuta bytecode y lo traduce a código máquina      |
| Lenguaje compilado    | Genera código máquina o un ejecutable antes de ejecutarse                                  |
| Lenguaje interpretado | Se ejecuta mediante un intérprete o runtime sin generar previamente un ejecutable completo |
| Lenguaje JIT          | Combina interpretación y compilación durante la ejecución                                  |
| Linker                | Une archivos objeto y librerías para generar el ejecutable final                           |


### Posibles flujos

#### 1) Por Assembly

```txt
Código fuente
↓
Compilador
↓
Assembly
↓
Assembler
↓
Código máquina
↓
Ejecutable
↓
CPU
```

Ejemplos: C, C++ en compiladores viejos.


#### 2) Por Bytecode y VM

```txt
Código fuente
↓
Compilador
↓
Bytecode
↓
VM / Runtime
↓
Código máquina
↓
CPU
```

Ejemplos: Java, C#, Kotlin.


#### 3) Directo

```txt
Código fuente
↓
Compilador
↓
Código máquina
↓
Linker
↓
Ejecutable
↓
CPU
```

Ejemplos: C, C++, Rust, Go.


#### 4) Por Interpretación / JIT

- El programa se traduce y se ejecuta al mismo tiempo, sin generar previamente un archivo ejecutable completo.
- El código es leído por un runtime, que lo interpreta o lo compila parcialmente mientras se ejecuta.
- Para ello, el runtime puede incluir varios componentes internos, como intérpretes, compiladores, máquinas virtuales y herramientas de gestión de memoria.
- Por eso, en los lenguajes interpretados modernos, tanto el intérprete como el compilador suelen formar parte del mismo runtime.

```txt
Código fuente
↓
Runtime
↓
Interpretación o JIT
↓
Código máquina
↓
CPU
```

Ejemplos: JavaScript, Python, PHP, Ruby.






### Runtime
o Entorno de Ejecución

Es el conjunto de programas, bibliotecas y servicios que permiten que un programa se ejecute y pueda interactuar con la memoria, el sistema operativo y el hardware → El software que ejecuta un programa y le proporciona acceso a recursos como memoria, archivos, red y servicios del sistema operativo.

```txt
Runtime
├─ Ejecuta el programa
├─ Administra memoria
├─ Maneja errores
├─ Accede a archivos
├─ Gestiona comunicaciones de red
├─ Gestiona procesos e hilos
└─ Facilita el debugging (opcional)
```

Para analizar los runtimes, se suelen hacer las pregunas:
- ¿Cuántas responsabilidades tiene el runtime? → ¿Cuántas tareas realiza el runtime mientras el programa está ejecutándose?
- ¿Cuánta infraestructura agrega? → ¿Cuántos componentes extra necesitás para ejecutar el programa?
- ¿Cuánto depende el programa de él? → Si saco el runtime, ¿qué tan roto queda el programa?

Cuanto más grande el runtime, más trabajo hace por vos.


| Lenguaje   | Compilador         | Runtime             | Tamaño del Runtime |
| ---------- | ------------------ | ------------------- | ------------------ |
| JavaScript | V8 (JIT)           | Node.js / Navegador | Grande             |
| Java       | javac              | JVM                 | Muy grande         |
| C#         | csc (Roslyn)       | CLR                 | Muy grande         |
| Python     | CPython            | CPython             | Grande             |
| PHP        | Zend Engine        | Zend Engine         | Grande             |
| Ruby       | YARV/MRI           | MRI Ruby            | Grande             |
| Go         | Go Compiler        | Go Runtime          | Mediano            |
| Rust       | rustc              | Rust Runtime        | Chico              |
| C++        | G++, Clang++, MSVC | C++ Runtime         | Chico              |
| C          | GCC, Clang, MSVC   | C Runtime (libc)    | Mínimo             |


---


# Node.js

- JavaScript nació como un lenguaje pensado para ejecutarse dentro del navegador. Ser parte del Frontend y nada más.
- El navegador actuaba como runtime y proporcionaba herramientas para interactuar con páginas web (DOM, eventos, almacenamiento, etc.).
- Por eso, originalmente, sin un navegador no era posible ejecutar código JavaScript.

A algunos les gustó JavaScript y decidieron crear el runtime Node.js (construido sobre V8, el compilador de Google Chrome) para que JavaScript pudiera usarse fuera del navegador y así usarse oara desarrollar aplicaciones Backend.

Gracias a Node.js, JavaScript puede:
- Crear servidores web
- Construir APIs REST
- Leer y escribir archivos
- Conectarse a bases de datos
- Ejecutar scripts y automatizaciones
- Conectarse a herramientas del sistema


# Packages

| Concepto                    | Qué es                                                                                         | Ejemplo                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Gestor de paquetes          | Herramienta para instalar, actualizar y eliminar paquetes                                      | `npm`, `pip`, `apt`, `cargo`                                     |
| Ejecutor de paquetes          | Ejecuta paquetes sin necesidad de instalarlos globalmente / que queden instalados con persistencia.                                   | `npx` es parte de `npm`                                     |
| Paquete                     | Unidad distribuible de código o herramientas que puede instalarse                              | `dotenv`, `nodemon`, `pg`                                        |
| Librería (tipo de paquete)  | Conjunto de funcionalidades que llamás desde tu código                                         | React, jQuery, Lodash                                            |
| Framework (tipo de paquete) | Estructura que organiza una aplicación y llama a tu código                                     | Express, Next.js, Angular                                        |
| Dev Tool (tipo de paquete)  | Herramienta que ayuda durante el desarrollo, pero no forma parte de la lógica de la aplicación | `Nodemon`, `Vite`, `TypeScript`, `Webpack`, linters |


- dotenv, express.js, pg, nodemon
- instalacion con npm y ejecucion con npx y tema archivo package








