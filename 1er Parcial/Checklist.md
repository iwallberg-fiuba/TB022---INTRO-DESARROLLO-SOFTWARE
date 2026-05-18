
table of contents

Pendientes:
- Table of contents
- SQL cheatsheet
- Docker cheatsheet
- Bash checklist
- Bash cheatsheet
- Git y github cheatsheet
- Ordenar este doc + el readme (crear otro para las cheatsheets?)
- IA checklist + cheatsheet

---

<br>

## Checklists

<br>

### SQL

<br>

- Tipos de datos (`SERIAL`, `INT`, `SMALLINT`, `TEXT`, `VARCHAR(50)`)
- Restricciones y valores por defecto (`UNIQUE`, `NOT NULL`, `DEFAULT 0`)

Definir y explicar:
- [ ] Qué es SQL?
- [ ] Qué cosas deben ser representadas como tablas en una base de datos?
- [ ] Ventajas de usar SQL
- [ ] Que significan/ qué son: `1:1`, `1:N`, y `N:N`?
- [ ] Cómo resolver `N:N`?
- [ ] Conceptos Primary Key y Foreign key 

Explicar + decir comando(s):
- [ ] Query para definir PK
- [ ] Query para definir FK
- [ ] SELECT ... FROM tabla
- [ ] INSERT INTO tabla (id, nombre, apellido) VALUES (....)
- [ ] UPDATE tabla SET ... WHERE ...
- [ ] DELETE FROM tabla
- [ ] DROP DATABASE mi_base y DROP TABLE tabla
- [ ] TRUNCATE TABLE tabla
- [ ] JOIN tabla ON ...
- [ ] LEFT JOIN tabla ON ...
- [ ] WHERE ...
- [ ] Consultas concatenadas
- [ ] Consultar tabla auxiliar
- [ ] Consultar múltiples tablas al mismo tiempo
- [ ] Cuándo usar AND, OR, NOT
- [ ] Cuándo usar <>, !=, <, >, >=, <=

<br>

---

<br>

### Docker

<br>

Definir y explicar:
- [ ] Imagen
- [ ] Dockerfile
- [ ] Contenedor
- [ ] Servicios/ dependencias
- [ ] Puerto
- [ ] Persistencia: Volumen vs bind mount
- [ ] Ventajas de usar una app hecha con docker para el usuario
- [ ] Ventajas de usar docker para el desarrollador

Definir, explicar + decir comando(s):
- [ ] Flujo de comandos de docker (sin tener un archivo docker-compose)
- [ ] Saber qué hace cada comando


<br>
<br>

---

<br>

### Bash

<br>

| Área | Contenido |
|---|---|
| Práctica | 1. Los comandos del apunte.<br>2. Orden y sintaxis correcta.<br>3. Qué hace cada comando.<br>4. Moverse entre directorios.<br>5. Mostrar características de archivos.<br>6. Pipelines y redirecciones , argumentos|
| Teoría | 1. Ventajas/desventajas de usar Bash. |

<br>
<br>

---

<br>

### Regex

<br>

Leer lo siguiente:

<br>

| Tema | Ejemplo | Qué devuelve |
|---|---|---|
| Qué es regex | `^[A-Z]$` | Regex busca patrones de texto. En este caso, devuelve una letra mayúscula.|
| Qué es Character Class | `[0-9]` | Esta es la forma tradicional de usar regex. En este caso, devuelve un dígito.  |
| Qué es Shorthand Character Class | `\d` | Otra forma de usar regex. No es necesario saber usarlo. En este caso, devuelve un dígito. |
| Buscar coincidencias en una línea | `hola como estas` | Ese texto pero puede estar entre otras cosas en esa misma línea. |
| Buscar coincidencias donde no haya nada más en esa línea | `^Hola$` | Línea entera que solo contenga `Hola`. |
| Consultar caracter desconocido -> con `.`| `hola.mundo` | Caracter desconocido entre `hola` y `mundo`. `.` representa cualquier caracter. |
| Usar `.` como literal -> con `\.`| `google\.com` | `google.com` |
| Qué es sed | `sed` modifica texto: `sed ´s/patrón/reemplazo/g'`. | Intercambia la parte del `patrón` por la parte del `reemplazo` (ambas escritas en regex) en todas sus ocurrencias (por la `g` de `global` del final, que según el caso se pone o no). |


<br>
<br>
Ahora, 
<br>

Decir comando(s):
- [ ] Consultar por una clase de caracteres (letras minusculas, letras mayusculas, letras mayusculas y minusculas, números, etc.).
- [ ] Concatenar patrones para consultar por distintas clases en distintas posiciones.
- [ ] Buscar cierto patrón o clase cierta cantidad de veces con `+`, `*`, `{5}`.
- [ ] Negación de una clase con `^`.
- [ ] Consultar texto desconocido entre algo
- [ ] Cómo usar sed


<br>






<br>
<br>

---

<br>

### Git y GitHub

<br>

Definir, explicar + decir comando(s):
  - [ ] commit
  - [ ] add
  - [ ] diff
  - [ ] log
  - [ ] merge
  - [ ] push (github)
  - [ ] pull (github)
  - [ ] clone
  - [ ] fetch
  - [ ] status
  - [ ] cambio de rama
  - [ ] conflicts
  - [ ] forks
  - [ ] stash
  - [ ] rebase

Definir y explicar:
  - [ ] Branches (como feature, main/ origin)
  - [ ] Release
  - [ ] Stage
  - [ ] Uso de git + beneficios
  - [ ] Uso de github + beneficios
  - [ ] Repositorio
  - [ ] Repositorio remoto vs local


<br>
<br>

---

<br>

### Ingeniería de Software y SDLC
No subestimar..

<br>

Definir y explicar:
- [ ] Etapas del SDLC + qué rol(es) participa(n) en cada etapa del SDLC
- [ ] es lineal el SDLC? + cuándo es malo retroceder en el SDLC?

<br>
<br>

---

<br>

### IA

<br>

Pendiente.

<br>
<br>

---
---
---

<br>

## Cheatsheet

<br>

### Ingenieria de Software y SDLC

<br>

| Etapa del SDLC | Qué sucede | Roles que suelen participar |
|---|---|---|
| Análisis de requerimientos (funcionales y no funcionales) | Se define qué necesita el cliente/usuario.<br>Requisitos funcionales: Qué debe hacer el sistema (“El usuario puede subir archivos”).<br>Requisitos no funcionales: seguridad, rendimiento, escalabilidad, velocidad, disponibilidad, usabilidad (“La subida debe tardar menos de 2 segundos”) . | Product Manager, Project Manager, Software Architect, UX Designer |
| Diseño | Se diseña la arquitectura, interfaz y estructura del sistema. | Software Architect, UI Designer, UX Designer, DBA |
| Desarrollo | Se programa el sistema. | Frontend Developer, Backend Developer, Full Stack Developer |
| Testing / QA | Se prueban funcionalidades y errores. | QA / Tester, Developers |
| Despliegue | Se despliega el sistema a producción. | DevOps Engineer, Backend Developer |
| Mantenimiento | Se corrigen errores y agregan mejoras. | Developers, DevOps, QA |

- El SDLC es un proceso **no lineal** y pueden repetirse pasos, el problema es cuando sucede por causas evitables. Por esto, se debe desarrollar software que esté correctamente gestionado con Git, GitHub y Docker, y que utilice las tecnologías correspondientes según el proyecto, sin forzar el uso de herramientas que están diseñadas para otros casos. Así, se vuelve un sistema **funcional, escalable, seguro, eficiente, y modular** y se evitan problemas que requieren retroceder en el SDLC por tener un código difícil de mantener, modificar y/o expandir.

<br>



---

<br>

### Regex

<br>

| Tema | Ejemplo | Qué devuelve |
|---|---|---|
| Consultar por una clase de caracteres (letras minusculas, letras mayusculas, letras mayusculas y minusculas, números, etc.) | `[A-Za-z]` | Una letra. |
| Concatenar patrones para consultar por distintas clases en distintas posiciones | `[A-Za-z][0-9]` | Una letra seguida de un número. |
| Buscar cierto patrón o clase cierta cantidad de veces con `+`, `*`, `{5}` | `[0-9]+` / `[0-9]*` / `[0-9]{5}` | Uno o más números / cero o más / exactamente 5. |
| Negación de una clase con `^` | `[^0-9]` | Cualquier carácter que no sea numérico. |
| Consultar texto desconocido entre algo | `hola.*mundo` | Texto entre `hola` y `mundo`. |
| Cómo usar sed | `echo "abc123" ⎜ sed 's/[0-9]/X/g'` | `abcXXX` |

<br>
<br>

---

<br>


