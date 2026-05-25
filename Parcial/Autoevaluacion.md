

Disminuir zoom para ver mejor el contenido.

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

[SQL](./Extra/SQL.md)

<br><br>

### Docker

<br>

| Tema | Información |
| --- | --- |
| Imagen | Plantilla inmutable que contiene la app, dependencias, configuraciones y comandos necesarios para crear contenedores. Nota: no se dice "ejecutar una imagen", se dice “levantar/iniciar/crear un contenedor desde una imagen”.|
| Contenedor | Instancia en ejecución de una imagen. Tiene procesos, red, puertos y sistema de archivos aislado. |
| Dockerfile | Archivo con instrucciones para construir una imagen (contiene `FROM`, `COPY`, `RUN`, `CMD`, etc.). |
| Servicios / dependencias | Cada servicio (frontend, backend, base de datos, etc.) suele ejecutarse en un contenedor distinto. Algunos servicios dependen de otros para funcionar. Se comunican mediante una red virtual creada por Docker. |
| Puerto | Permite acceder desde tu máquina al programa que corre dentro del contenedor. <br>Relación `host:contenedor`. <br>Ejemplo: `3000:3000` → puerto `3000` de tu PC conectado al `3000` del contenedor. |
| Persistencia | **Volumen:** administrado por Docker, ideal para datos persistentes.<br>**Bind mount:** carpeta real del host, útil para desarrollo y sincronización inmediata de archivos. |
| Flujo Comandos Docker | `docker build` → construye una imagen desde una Dockerfile.<br>`docker run` → crea e inicia un contenedor a partir de una imagen.<br>`docker ps` → muestra contenedores en ejecución.<br>`docker logs` → muestra logs/salida del contenedor.<br>`docker stop` → detiene un contenedor.<br>`docker rm` → elimina un contenedor detenido. |

| Beneficiado | Ventajas |
| --- | --- |
| Usuario (SUECA) | **S**imple instalación.<br>**U**X más estable.<br>**E**ntorno consistente.<br>**C**ompatibilidad entre máquinas/sistemas.<br>**A**ctualizaciones y migraciones más fáciles. |
| Desarrollador (MAPTEC) | **M**ismo entorno en distintas máquinas.<br>**A**islamiento de dependencias.<br>**P**ortabilidad y reproducibilidad.<br>**T**esting y deployment más simples.<br>**E**scalabilidad y mantenimiento más simples.<br>**C**I/CD y colaboración/trabajo en equipo. |

| de qué | Componentes |
| --- | --- |
| Docker | Sistema Host → Kernel del host (o kernel Linux dentro de WSL2/VM si el host es Windows/macOS) → Docker Engine (gestiona imágenes, redes y contenedores) → Contenedores (procesos aislados que comparten el kernel). |
| Virtual Machine (VM) | Hardware → Hypervisor (software de virtualización) → Máquinas Virtuales → Sistema Operativo invitado completo con su propio kernel → Aplicaciones.                                   |



<br><br>

### Linux y Bash

<br>

`Pending`  

<br><br>

### Regex y sed

<br>

| Tema | Ejemplo | Qué devuelve |
| --- | --- | --- |
| Regex | `^[A-Z]$` | busca patrones de texto. En este caso, devuelve una letra mayúscula. |
| Character Class | `[0-9]` | Esta es la forma tradicional de usar regex. En este caso, devuelve un dígito. |
| Shorthand Character Class | `\d` | Otra forma de usar regex. No es necesario saber usarlo. En este caso, devuelve un dígito. |
| Buscar matches en una línea | `hola como estas` | Ese texto, aunque puede estar entre otras cosas en esa misma línea. |
| Buscar matches donde no haya nada más en esa línea | `^Hola$` | Línea entera que solo contenga `Hola`. |
| Carácter desconocido `.` | `hola.mundo` | Carácter desconocido entre `hola` y `mundo`. `.` representa cualquier carácter. |
| Usar `.` como literal con `\.` | `google\.com` | `google.com` |
| Cuantificadores | `[0-9]+`, `[0-9]*`, `[0-9]{5}` | Uno o más / cero o más / exactamente 5. |
| Negación de clase | `[^0-9]` | Cualquier carácter que no sea un número. |
| Qué es `sed` | `sed 's/patrón/reemplazo/g'` | Reemplaza el patrón por el reemplazo en todas sus ocurrencias. Si sacas la `g`, lo hace solo en la primera. |

<br><br>

### Git y GitHub

<br>

`Pending`  

<br><br>

### Ingeniería de Software y SDLC

<br>

| Tema | Información |
| --- | --- |
| Ingeniería de Software | Incluye todo el SDLC (Software Development Life Cycle), no es solo programar. |
| SDLC | Requerimientos (Func. y No Func.) → Diseño → Desarrollo → Testing → Despliegue → Mantenimiento |
| Req. Funcionales (`BREGAM`) | Definen **qué hace** el sistema. Suelen expresarse con verbos: **B**uscar, **R**egistrar, **E**nviar, **G**enerar, **A**ctualizar, **M**ostrar. |
| Req. No Funcionales (`SEMECA`) | Definen **cómo debe funcionar** el sistema. Ejemplos: **S**eguro, **E**scalable, **M**antenible, **E**ficiente, **C**onfiable, **A**ccesible. |
| Roles comunes | **Analista:** define necesidades y requerimientos.<br>**Arquitecto:** diseña estructura y tecnologías.<br>**Desarrollador:** implementa funcionalidades.<br>**QA/Tester:** verifica calidad y detecta errores.<br>**DevOps:** CI/CD. |
| Cuándo es malo retroceder en el SDLC | Cuando ocurre por errores evitables, mala planificación o deuda técnica (problemas generados por elegir soluciones rápidas pero ineficientes cuando se desarrolló el código). | 

<br>
Sobre DevOps y CI/CD:
- CI (Continuous Integration): integra cambios de código automáticamente, ejecutando tests, validaciones y builds.
- CD (Continuous Delivery / Deployment): automatiza preparación y/o despliegue de la aplicación luego de pasar tests.
- Objetivo de CI/CD: Reducir errores manuales, acelerar desarrollo y hacer deployments más seguros, rápidos y frecuentes.
- Flujo típico CI/CD: `git push` → tests automáticos → build → deployment automático 


<br><br>

### Inteligencia Artificial

<br>

| Término | Qué es | Ejemplo |
| --- | --- | --- |
| LLM (Large Language Model) | Modelo de IA entrenado con grandes cantidades de texto. Predice texto y sigue instrucciones. | ChatGPT, Claude |
| Coding Agent | Agente basado en un LLM que además puede usar herramientas y actuar sobre un entorno. | Codex, Claude Code |
| Agent Harness | Sistema/capa que coordina herramientas, memoria, contexto e instrucciones del agente. | OpenAI Codex Harness |
| Coding Harness | Entorno específico para programación y automatización de tareas de desarrollo. | OpenAI Codex Harness |
| Reasoning Model | Modelo optimizado para razonar paso a paso antes de responder. | o3, GPT-5 Reasoning |
| Live Repo Context | Acceso al estado actual y real de un repositorio mientras el agente trabaja. | Codex y Cursor leyendo archivos y commits en tiempo real. |
| Context Reduction | Técnicas para resumir o filtrar información y evitar saturar el contexto del modelo. | Claude resumiendo automáticamente archivos largos antes de enviarlos al modelo. |
| Cache Reuse | Reutilización de resultados o contexto previo para ahorrar tiempo y recursos. | Reusar respuestas con otros agentes. |
| Tool Access | Capacidad del agente para usar herramientas externas. | Claude Code usando terminal, Codex editando archivos. |
| Subagents | Agentes auxiliares especializados en subtareas específicas. | AutoGen usando múltiples agentes para frontend, backend y testing al mismo tiempo. |

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
