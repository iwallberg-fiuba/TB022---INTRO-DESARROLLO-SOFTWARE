
table of contents

---

<br>

## Parte 1: Checklist

<br>

### SQL

<br>

| Área | Contenido |
|---|---|
| Armado | 1. Crear/eliminar/modificar DBs, tablas y datos.<br>2. Reconocer qué tiene que ser una tabla.<br>3. Reconocer cuántas tablas auxiliares se necesitan. |
| Consultas / Queries | 1. Múltiples tablas al mismo tiempo.<br>2. Tablas auxiliares.<br>3. `SELECT`.<br>4. `INSERT`.<br>5. `UPDATE`.<br>6. `DELETE`. |
| Teoría | 1. `FOREIGN KEY` y `PRIMARY KEY`.<br>2. Tipos de datos ⇒ `SERIAL`, `INT`, `SMALLINT`, `TEXT`, `VARCHAR(50)`.<br>3. Restricciones y valores por defecto ⇒ `UNIQUE`, `NOT NULL`, `DEFAULT 0`.<br>4. Ventajas de usar SQL.<br>5. Saber tipos de relaciones ⇒ `1:1`, `1:N`, y `N:N` (ésta lleva a la tabla auxiliar). |

<br>

---

<br>

### Docker

<br>

| Área | Contenido |
|---|---|
| Práctica | 1. Saber ordenar los comandos del flujo completo de Docker (sin el archivo docker-compose).<br>2. Saber qué hace cada comando. |
| Teoría | 1. Imagen.<br>2. Contenedor.<br>3. Servicio.<br>4. Puerto.<br>5. Volumen y Persistencia.<br>6. Diferencia entre `Dockerfile` e imagen.<br>7. Diferencia entre volumen y bind mount.<br>8. Ventajas de usar Docker. |

<br>
<br>

---

<br>

### Bash

<br>

| Área | Contenido |
|---|---|
| Práctica | 1. Los comandos del apunte.<br>2. Orden y sintaxis correcta.<br>3. Qué hace cada comando.<br>4. Moverse entre directorios.<br>5. Mostrar características de archivos.<br>6. Pipelines y redirecciones |
| Teoría | 1. Ventajas/desventajas de usar Bash. |

<br>
<br>

---

<br>

### Regex

<br>

| Área | Contenido |
|---|---|
| Práctica | 1. Saber consultar cierta parte de una línea y no todas.<br>2. Saber `\.` para usar el `.` como literal y no como operador para buscar cualquier carácter.<br>3. Saber diferencia entre `.` y `\.`.<br>4. Saber anidar los regex ⇒ `[A-Za-z]` vs `[A-Za-z][0-9]`.<br>5. Saber cuándo usar `+`, `*` o `{5}`.<br>6. Saber abrir regex ⇒ `^` y terminarlo ⇒ `$`.<br>7. Saber usar `^` como negación ⇒ `[^0-9]`.<br>8. Saber buscar cierto texto ⇒ `hola como estas`. |
| Teoría | 1. Diferencia entre regex y `sed`.<br>2. Saber que existe Shorthand Character Class y Character Class (usar cualquiera de las dos es válido). |

<br>
<br>

---

<br>

### Git y GitHub

<br>

| Área | Contenido |
|---|---|
| Teoría y Práctica | 1. Branches (`feature`, `main`).<br>2. Release.<br>3. Commit.<br>4. Add.<br>5. Diff.<br>6. Hotfix.<br>7. Log.<br>8. Stage.<br>9. Merge.<br>10. Conflicts y cómo solucionarlos.<br>11. Push (GitHub).<br>12. Pull (GitHub).<br>13. Clone.<br>14. Fetch.<br>15. Status. |
| Teoría | 1. Qué es un repositorio.<br>2. Repositorio remoto vs local.<br>3. Ventajas de usar Git.<br>4. Ventajas de usar GitHub. |

<br>
<br>

---

<br>

### Ingeniería de Software y SDLC

<br>

| Área | Contenido |
|---|---|
| Roles | 1. Saber roles laborales del Ingeniero de Software y qué hacen. |
| SDLC | 1. Saber cuáles son las etapas del SDLC.<br>2. Saber qué sucede en cada etapa del SDLC.<br>3. Saber qué roles laborales del Ingeniero de Software intervienen en cada etapa.<br>4. Saber que no es un proceso lineal y que pueden repetirse pasos.<br>5. Saber cómo evitar tener que volver etapas atrás ⇒ armando un proyecto escalable, funcional, que cumpla con los requisitos, utilice las tecnologías adecuadas y esté correctamente gestionado con Git, GitHub y Docker. |

<br>
<br>

---

<br>

### IA

<br>

| Área | Contenido |
|---|---|
| Pendiente | Pendiente |

<br>
<br>

---

<br>

## Parte 2: Cheatsheet

<br>

### Ingenieria de Software y SDLC

<br>

| Etapa del SDLC | Qué sucede | Roles que suelen participar |
|---|---|---|
| Análisis de requisitos | Se define qué necesita el cliente/usuario. | Product Manager, Project Manager, Software Architect, UX Designer |
| Diseño | Se diseña la arquitectura, interfaz y estructura del sistema. | Software Architect, UI Designer, UX Designer, DBA |
| Desarrollo | Se programa el sistema. | Frontend Developer, Backend Developer, Full Stack Developer |
| Testing / QA | Se prueban funcionalidades y errores. | QA / Tester, Developers |
| Deployment | Se despliega el sistema a producción. | DevOps Engineer, Backend Developer |
| Mantenimiento | Se corrigen errores y agregan mejoras. | Developers, DevOps, QA |

<br>

#### Tipo de requisito
Unificarlo con la tabla de arriba.

<br>

| Tipo de requisito | Qué define | Ejemplos |
|---|---|---|
| Requisitos funcionales | Qué debe hacer el sistema. | Iniciar sesión, enviar mensajes, crear usuarios, realizar pagos. |
| Requisitos no funcionales | Cómo debe comportarse el sistema. | Seguridad, rendimiento, escalabilidad, velocidad, disponibilidad, usabilidad. |

<br>

Ejemplos:

* Funcional ⇒ “El usuario puede subir archivos.”
* No funcional ⇒ “La subida debe tardar menos de 2 segundos.”

<br>
<br>

---

<br>

### Regex y Sed

<br>

| Concepto | Regex | `sed` |
|---|---|---|
| Qué es | Un lenguaje de patrones para buscar texto. | Una herramienta/comando para editar texto automáticamente. |
| Qué hace | Encuentra texto que cumple un patrón. | Reemplaza, elimina o transforma texto. |
| Relación entre ambos | Define el patrón de búsqueda. | Usa regex para decidir qué modificar. |
| Ejemplo práctico | `[0-9]` encuentra números. | `sed 's/[0-9]/X/g'` ⇒ cambia números por `X`. (`s`: substitute, `g`: global ⇒ todas las coincidencias) |
| Resultado sobre `abc123` | Encuentra `123`. | Devuelve `abcXXX`. |
| También puede | Validar o filtrar texto. | Borrar líneas, editar archivos y transformar texto automáticamente. |

<br>
<br>

---

<br>


