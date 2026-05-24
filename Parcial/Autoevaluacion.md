
### Table of Contents

* [Recordatorios](#recordatorios)
  * [Bases de Datos y SQL](#bases-de-datos-y-sql)
  * [Docker](#docker)
  * [Linux y Bash](#linux-y-bash)
  * [Regex y sed](#regex-y-sed)
  * [Git y GitHub](#git-y-github)
  * [Ingeniería de Software y SDLC](#ingeniería-de-software-y-sdlc)
  * [Inteligencia Artificial](#inteligencia-artificial)
* [Preguntas de autoevaluación](#preguntas-de-autoevaluación)
  * [Requerimientos de las respuestas](#requerimientos-de-las-respuestas)
  * [Bases de Datos y SQL](#bases-de-datos-y-sql-1)
  * [Docker](#docker-1)
  * [Linux y Bash](#linux-y-bash-1)
  * [Regex y sed](#regex-y-sed-1)
  * [Git y GitHub](#git-y-github-1)
  * [Ingeniería de Software y SDLC](#ingeniería-de-software-y-sdlc-1)
  * [Inteligencia Artificial](#inteligencia-artificial-1)
 
<br><br>

---

<br>

## Recordatorios

<br>

### Bases de Datos y SQL

<br>


| Tema | Información |
| --- | --- |
| Qué es SQL | Lenguaje para definir, consultar y modificar datos en bases relacionales. |
| Alias | Se usan para escribir menos y entender mejor la consulta: `usuarios u`, `cursos c`, `usuarios_cursos uc`. Después usás `u.nombre`, `c.nombre`, etc. |
| Tipos de datos | `SERIAL`, `INT`, `SMALLINT`, `TEXT`, `VARCHAR(50)`. |
| Restricciones | `UNIQUE`, `NOT NULL`, `DEFAULT 0`. |
| JOINs | `JOIN` cruza coincidencias; `LEFT JOIN` conserva todas las filas de la izquierda, incluyendo repeticiones. |
| Filtros `WHERE` | `WHERE` + comparadores (`=`, `<>`, `!=`, `<`, `>`, `>=`, `<=`) + lógica (`AND`, `OR`, `NOT`). |
| Esqueletos útiles CRUD (Create, Read, Update, Delete) | `CREATE TABLE ...`, `SELECT ... FROM ...`, `INSERT INTO ... VALUES ...`, `UPDATE ... SET ... WHERE ...`. |
| `Primary Key (PK)` | Columna (o conjunto de columnas) con valores únicos que identifica cada fila de una tabla. Generalmente es una columna id. En tablas auxiliares N:N, la PK suele ser una tupla formada por las 2 FKs. |
| `Foreign Key (FK)` | Columna que guarda la PK de otra tabla para crear una relación entre ambas. |





<br><br>

### Docker

<br>

| Tema | Pista para orientarte |
| --- | --- |
| Imagen | Plantilla inmutable con app + dependencias + configuración base. |
| Contenedor | Instancia en ejecución de una imagen. No decir "ejecutar una imagen". |
| Dockerfile | Receta para construir una imagen: base, copia de archivos, dependencias, comandos. |
| Servicios/dependencias | La imagen define el entorno; los servicios múltiples suelen coordinarse aparte. |
| Puerto | Relación host:contenedor para exponer la app. |
| Persistencia | Volumen: administrado por Docker. Bind mount: carpeta real de tu máquina. |
| Flujo básico | `docker build` -> `docker run` -> `docker ps` -> `docker logs` -> `docker stop` / `docker rm`. |
| Qué mirar en una Dockerfile | `FROM`, `WORKDIR`, `COPY`, `RUN`, `EXPOSE`, `CMD`. |
| Ventaja para usuario | Instalación/uso más consistente. |
| Ventaja para dev | Mismo entorno en distintas máquinas. |

<br><br>

### Linux y Bash

<br>

| Área | Pistas |
| --- | --- |
| Navegación | `pwd`, `ls`, `cd`, rutas absolutas vs relativas. |
| Archivos | `touch`, `mkdir`, `cp`, `mv`, `rm`, `cat`, `less`. |
| Características | `ls -l`, permisos, tamaño, tipo de archivo. |
| Pipes y redirecciones | `|`, `>`, `>>`, `<` para conectar comandos o redirigir entrada/salida. |
| Argumentos | Pensar qué recibe el script/comando y en qué orden. |
| Bash | Sirve para automatizar tareas del sistema, manipular archivos y encadenar comandos. |
| Límite de Bash | Bueno para scripting; mala elección para apps web complejas. |

<br><br>

### Regex y sed

<br>

| Tema | Ejemplo | Qué devuelve |
| --- | --- | --- |
| Qué es regex | `^[A-Z]$` | Regex busca patrones de texto. En este caso, devuelve una letra mayúscula. |
| Qué es Character Class | `[0-9]` | Esta es la forma tradicional de usar regex. En este caso, devuelve un dígito. |
| Qué es Shorthand Character Class | `\d` | Otra forma de usar regex. No es necesario saber usarlo. En este caso, devuelve un dígito. |
| Buscar coincidencias en una línea | `hola como estas` | Ese texto, aunque puede estar entre otras cosas en esa misma línea. |
| Buscar coincidencias donde no haya nada más en esa línea | `^Hola$` | Línea entera que solo contenga `Hola`. |
| Consultar carácter desconocido con `.` | `hola.mundo` | Carácter desconocido entre `hola` y `mundo`. `.` representa cualquier carácter. |
| Usar `.` como literal con `\.` | `google\.com` | `google.com` |
| Cuantificadores | `[0-9]+`, `[0-9]*`, `[0-9]{5}` | Uno o más / cero o más / exactamente 5. |
| Negación de clase | `[^0-9]` | Cualquier carácter que no sea un número. |
| Qué es `sed` | `sed 's/patrón/reemplazo/g'` | Reemplaza el patrón por el reemplazo en todas sus ocurrencias. |

<br><br>

### Git y GitHub

<br>

| Tema | Pista para orientarte |
| --- | --- |
| Repositorio | Carpeta gestionada por Git; el historial vive en `.git`. |
| Stage | Área intermedia entre cambios hechos y commit. |
| `add` | Manda cambios al stage. Pensarlo como "preparar" archivos para el próximo commit. |
| Commit | Snapshot con mensaje claro. Atómico = un commit que agrupa un único cambio lógico, no varias cosas mezcladas. |
| Branch | Línea de trabajo independiente, por ejemplo `feature/...`, `main`, `development`. |
| Git vs GitHub | Git versiona cambios localmente; GitHub hospeda y comparte repositorios remotos. |
| `push` | Envía commits locales al remoto. |
| `pull` | Trae cambios del remoto al repositorio local. |
| `fetch` | Trae referencias/cambios remotos sin integrarlos todavía. |
| `merge` | Se hace parado en la rama que recibe los cambios. Pensarlo como "traer otra rama adentro de la actual". |
| Conflicts | Flujo mental: `status` -> editar archivo conflictivo -> `add` -> `commit` -> `push`. |
| `stash` | Guarda cambios sin commitearlos para limpiar temporalmente el working tree. |
| `rebase` | Reaplica commits sobre otra base; cambia el historial. |
| `diff`, `log`, `status` | Ver cambios, historial y estado del repo. |
| Cambio de rama | Primero mirar si hay cambios sin guardar/commitear; después `checkout` o `switch`. |
| Tags vs releases | Tag: marca en Git. Release: publicación/versionado en GitHub. |

<br><br>

### Ingeniería de Software y SDLC

<br>

| Tema | Info |
| --- | --- |
| Ingeniería de software | No es solo programar: incluye todo el SDLC. |
| Etapas del SDLC | Requerimientos (Func. y No Func.) -> diseño -> desarrollo -> testing -> despliegue -> mantenimiento. |
| Funcionales (verbos) | Qué hace. En general: Buscar `_`, Registrar `_`, Enviar `_`, Generar `_` , Actualizar `_`, Mostrar `_` (BREGAM) |
| No Funcionales (adjetivos) | Cómo lo hace. Que sea: Seguro, Escalable, Mantenible, Eficiente, Confiable, Accesible (SEMECA) |
| Roles | Analista, Arquitecto, Desarrollador, QA/ Tester, DevOps |
| Cuándo es malo retroceder | Cuando pasa por mala planificación, deuda técnica (hacer algo rápido pero sin planificar correctamente) y/o errores evitables (no cumplir los requerimientos funcionales y/o no funcionales, por ejemplo). |

<br><br>

### Inteligencia Artificial

<br>

| Término | Pista para orientarte |
| --- | --- |
| LLM | Modelo de lenguaje que predice texto y puede seguir instrucciones. |
| Coding Agent | Agente que usa un modelo para razonar y además operar sobre herramientas/código. |
| Agent Harness | Capa que coordina modelo, herramientas, contexto y ejecución del agente. |
| Coding Harness | Entorno/controlador específico para tareas de programación. |
| Reasoning Model | Modelo orientado a resolver tareas paso a paso con más capacidad de razonamiento. |
| Live Repo Context | Acceso al estado real y actual del repositorio mientras trabaja. |
| Context Reduction | Resumir/filtrar contexto para no saturar la ventana del modelo. |
| Cache Reuse | Reutilizar resultados o contexto previo para evitar repetir trabajo. |
| Tool Access | Posibilidad de usar shell, editor, buscador, navegador, etc. |
| Subagents | Agentes auxiliares para dividir trabajo o especializar subtareas. |

<br><br>

---

<br><br>

## Preguntas de autoevaluación

<br>

### Requerimientos de las respuestas

- Random picker: link al random picker con las preguntas.
- Preguntas teóricas: requieren contestar con definición y explicación del concepto.
- Preguntas con demostración: requieren contestar con explicación del concepto + comando(s).
- Preguntas de flujo: requieren contestar con breves explicaciones de cada paso y su comando asociado.


<br>

### Bases de Datos y SQL

Definir y explicar:

- [ ] Qué es SQL?
- [ ] Qué cosas deben ser representadas como tablas en una base de datos?
- [ ] Ventajas de usar SQL
- [ ] Qué significan/ qué son: `1:1`, `1:N`, y `N:N`?
- [ ] Cómo resolver `N:N`?
- [ ] Conceptos Primary Key y Foreign key

Definir y explicar (con comando(s)):

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

---

### Docker

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

---

### Linux y Bash

| Área | Contenido |
| --- | --- |
| Práctica | 1. Los comandos del apunte.<br>2. Orden y sintaxis correcta.<br>3. Qué hace cada comando.<br>4. Moverse entre directorios.<br>5. Mostrar características de archivos.<br>6. Pipelines, redirecciones y argumentos. |
| Teoría | 1. Ventajas/desventajas de usar Bash. |

---

### Regex y sed

Decir comando(s):

- [ ] Consultar por una clase de caracteres (letras minúsculas, letras mayúsculas, letras mayúsculas y minúsculas, números, etc.).
- [ ] Concatenar patrones para consultar por distintas clases en distintas posiciones.
- [ ] Buscar cierto patrón o clase cierta cantidad de veces con `+`, `*`, `{5}`.
- [ ] Negación de una clase con `^`.
- [ ] Consultar texto desconocido entre algo
- [ ] Ejemplo de cómo usar sed

---

### Git y GitHub

Definir, explicar + decir comando(s):

- [ ] commit (+ qué significa que sea atómico o que diga feat)
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

- [ ] Branches (incluyendo feature, main/ origin)
- [ ] Tags (git) y releases (github)
- [ ] Stage
- [ ] Uso de git + beneficios
- [ ] Uso de github + beneficios
- [ ] Repositorio
- [ ] Repositorio remoto vs local

---

### Ingeniería de Software y SDLC

Definir y explicar:

- [ ] Etapas del SDLC + qué rol(es) participa(n) en cada etapa del SDLC
- [ ] Es lineal el SDLC? + cuándo es malo retroceder en el SDLC?

---

### Inteligencia Artificial

Definir y explicar:

- [ ] LLM
- [ ] Coding Agent
- [ ] Agent Harness
- [ ] Coding Harness
- [ ] Reasoning Model
- [ ] Live Repo Context
- [ ] Context Reduction
- [ ] Cache Reuse
- [ ] Tool Access
- [ ] Subagents
