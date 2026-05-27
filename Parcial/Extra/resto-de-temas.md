<br><br>

### Table of Contents

<br>

> [!NOTE]
> Usar modo `Full Screen`, disminuir / aumentar el `zoom` y abrir el `Outline` para una mejor lectura.

<br>

[Docker](#docker)
- [Conceptos clave](#conceptos-clave)
- [Ventajas](#ventajas)
- [Docker VS VMs](#docker-vs-vms)

<br>

[Regex y sed](#regex-y-sed)

<br>

[Ingeniería de Software y SDLC](#ingeniería-de-software-y-sdlc)
- [Conceptos clave](#conceptos)
- [Requerimientos](#requerimientos)
- [Sobre DevOps y CI/CD](#sobre-devops-y-cicd)

<br>

[Inteligencia Artificial](#inteligencia-artificial)
- [Agentes](#agentes)
- [Arquitectura](#arquitectura)
- [Optimización](#optimización)

<br>

---

<br>

## Docker

<br>

### Conceptos clave

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


<br><br><br>

### Ventajas

<br>

| Beneficiado | Ventajas |
| --- | --- |
| Usuario (SUECA) | **S**imple instalación.<br>**U**X más estable.<br>**E**ntorno consistente.<br>**C**ompatibilidad entre máquinas/sistemas.<br>**A**ctualizaciones y migraciones más fáciles. |
| Desarrollador (MAPTEC) | **M**ismo entorno en distintas máquinas.<br>**A**islamiento de dependencias.<br>**P**ortabilidad y reproducibilidad.<br>**T**esting y deployment más simples.<br>**E**scalabilidad y mantenimiento más simples.<br>**C**I/CD y colaboración/trabajo en equipo. |


<br><br><br>

### Docker vs VMs

<br>

| Tecnología | Flujo                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Docker** | Sistema Host  <br>↓<br> Kernel del host *(o kernel Linux en WSL2/VM)*  <br>↓<br> Docker Engine  <br>↓<br> Contenedores     |
| **VM**     | Hardware  <br>↓<br> Hypervisor  <br>↓<br> Máquinas Virtuales  <br>↓<br> Sistema Operativo invitado  <br>↓<br> Aplicaciones |


<br><br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Regex y sed

<br><br>

| Tema | Ejemplo | Qué devuelve |
| --- | --- | --- |
| Regex | `^[A-Z]$` | busca patrones de texto. En este caso, devuelve una letra mayúscula. |
| Character Class | `[0-9]` | Esta es la forma tradicional de usar regex. En este caso, devuelve un dígito. |
| Shorthand Character Class | `\d` | Otra forma de usar regex. No es necesario saber usarlo. En este caso, devuelve un dígito. |
| Buscar matches en una línea | `hola como estas` | Ese texto, aunque puede estar entre otras cosas en esa misma línea. |
| Buscar matches donde no haya nada más en esa línea | `^Hola$` | Línea entera que solo contenga `Hola`. |
| Carácter desconocido `.` | `hola.mundo` | Carácter desconocido entre `hola` y `mundo`. `.` representa cualquier carácter. |
| Usar `.` como literal `\.` | `google\.com` | `google.com` |
| Cuantificadores | `[0-9]+`, `[0-9]*`, `[0-9]{5}` | Uno o más / cero o más / exactamente 5. |
| Negación de clase | `[^0-9]` | Cualquier carácter que no sea un número. |
| Qué es `sed` | `sed 's/patrón/reemplazo/g'` | Reemplaza el patrón por el reemplazo en todas sus ocurrencias. Si sacas la `g`, lo hace solo en la primera. |



<br><br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Ingeniería de Software y SDLC

<br><br>

### Conceptos

| Tema | Información |
| --- | --- |
| Ingeniería de Software | Incluye todo el SDLC (Software Development Life Cycle), no es solo programar. |
| SDLC | Requerimientos (Func. y No Func.) → Diseño → Desarrollo → Testing → Despliegue → Mantenimiento |
| Roles | **Analista:** define necesidades y requerimientos.<br>**Arquitecto:** diseña estructura y tecnologías.<br>**Desarrollador:** implementa funcionalidades.<br>**QA/Tester:** verifica calidad y detecta errores.<br>**DevOps:** CI/CD. |
| Cuándo es malo retroceder en el SDLC | Cuando ocurre por errores evitables, mala planificación o deuda técnica (problemas generados por elegir soluciones rápidas pero ineficientes cuando se desarrolló el código). | 


<br><br><br>

### Requerimientos

| Requerimientos | Información |
| --- | --- |
| Funcionales (`BREGAM`) | Definen **qué hace** el sistema. Suelen expresarse con verbos: **B**uscar, **R**egistrar, **E**nviar, **G**enerar, **A**ctualizar, **M**ostrar. |
| No Funcionales (`SEMECA`) | Definen **cómo debe funcionar** el sistema. Ejemplos: **S**eguro, **E**scalable, **M**antenible, **E**ficiente, **C**onfiable, **A**ccesible. |


<br><br><br>

### Sobre DevOps y CI/CD
- CI (Continuous Integration): integra cambios de código automáticamente, ejecutando tests, validaciones y builds.
- CD (Continuous Delivery / Deployment): automatiza preparación y/o despliegue de la aplicación luego de pasar tests.
- Objetivo de CI/CD: Reducir errores manuales, acelerar desarrollo y hacer deployments más seguros, rápidos y frecuentes.
- Flujo típico CI/CD: `git push` → tests automáticos → build → deployment automático 

<br>
<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Inteligencia Artificial

<br><br>

### Agentes

<br>

| Término                        | Qué es                                                                                       | Ejemplo                                                           |
| ------------------------------ | -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **LLM (Large Language Model)** | Modelo de IA entrenado con enormes cantidades de texto. Predice texto y sigue instrucciones. | ChatGPT, Claude                                                   |
| **Reasoning Model**            | Modelo optimizado para razonar paso a paso antes de responder.                               | o3, GPT-5 Reasoning                                               |
| **Coding Agent**               | Agente basado en un LLM que además puede usar herramientas y actuar sobre un entorno.        | Codex, Claude Code                                                |
| **Subagents**                  | Agentes auxiliares especializados en subtareas concretas.                                    | AutoGen usando agentes separados para frontend, backend y testing |

<br><br><br>

### Arquitectura

<br>

| Término               | Qué es                                                                                | Ejemplo                                              |
| --------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **Agent Harness**     | Sistema/capa que coordina herramientas, memoria, contexto e instrucciones del agente. | OpenAI Codex Harness                                 |
| **Coding Harness**    | Entorno específico para programación y automatización de tareas de desarrollo.        | OpenAI Codex Harness                                 |
| **Tool Access**       | Capacidad del agente para usar herramientas externas.                                 | Claude Code usando terminal, Codex editando archivos |
| **Live Repo Context** | Acceso al estado actual y real de un repositorio mientras el agente trabaja.          | Cursor leyendo archivos y commits en tiempo real     |


<br><br><br>

### Optimización

<br>

| Término               | Qué es                                                                               | Ejemplo                                                        |
| --------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| **Context Reduction** | Técnicas para resumir o filtrar información y evitar saturar el contexto del modelo. | Claude resumiendo archivos largos antes de enviarlos al modelo |
| **Cache Reuse**       | Reutilización de resultados o contexto previo para ahorrar tiempo y recursos.        | Reusar respuestas o análisis ya generados                      |


<br><br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br>


