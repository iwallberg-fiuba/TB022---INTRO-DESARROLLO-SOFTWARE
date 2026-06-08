

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

| Tipo | Flujo | Características | Ejemplos |
|--------|--------|--------|--------|
| **Por Assembly** | Código fuente → Compilador → Assembly → Assembler → Código máquina → Ejecutable → CPU | El compilador genera código Assembly que luego es convertido a código máquina por un assembler. | C, C++ (compiladores antiguos) |
| **Por Bytecode y VM** | Código fuente → Compilador → Bytecode → VM / Runtime → Código máquina → CPU | El compilador genera bytecode portable que es ejecutado por una máquina virtual o runtime. | Java, C#, Kotlin |
| **Directo** | Código fuente → Compilador → Código máquina → Linker → Ejecutable → CPU | El compilador genera código máquina directamente y luego se crea el ejecutable. | C, C++, Rust, Go |
| **Por Interpretación / JIT** | Código fuente → Runtime → Interpretación o JIT → Código máquina → CPU | El runtime interpreta o compila parcialmente el código mientras se ejecuta, sin generar previamente un ejecutable completo. | JavaScript, Python, PHP, Ruby |

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

