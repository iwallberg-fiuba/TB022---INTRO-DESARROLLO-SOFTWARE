
> **Idea:** Docker importa porque convierte un entorno tecnico en algo describible, reproducible y portable entre maquinas.

## Keywords a saber

`imagen`, `contenedor`, `Dockerfile`, `Docker Engine`, `Docker Hub`, `docker run`, `docker build`, `puertos`, `volumenes`, `compose`, `.env`, `multi-stage build`

> **Para estudiar:** pensa cada keyword como una parte del flujo `describir -> construir -> ejecutar -> conectar -> persistir`.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `imagen` | Plantilla inmutable con el entorno necesario para una aplicacion. | Se parece mas a una receta congelada que a una maquina viva. Define que se necesita, pero no esta "corriendo". |
| `contenedor` | Instancia en ejecucion de una imagen. | Es la imagen puesta en marcha. Si la imagen es el molde, el contenedor es el caso concreto ejecutandose. |
| `Dockerfile` | Archivo que describe como construir una imagen Docker. | Es importante porque vuelve reproducible el entorno: no dependes de recordar pasos manuales. |
| `Docker Engine` | Motor que construye, ejecuta y administra contenedores. | Es la pieza de software que hace posible todo el flujo Docker en tu maquina. |
| `Docker Hub` | Registro publico donde se comparten imagenes Docker. | Cumple un rol parecido al de un repositorio de paquetes, pero para imagenes enteras. |
| `docker run` | Comando para crear y arrancar un contenedor desde una imagen. | Es el paso donde la definicion abstracta se convierte en un proceso real. |
| `docker build` | Comando para construir una imagen a partir de un `Dockerfile`. | Sirve para transformar instrucciones declaradas en una imagen utilizable. |
| `puertos` | Canales de red que se exponen o mapean entre host y contenedor. | Importan porque un contenedor puede estar corriendo perfecto y aun asi ser inaccesible desde afuera si los puertos no estan bien mapeados. |
| `volumenes` | Mecanismo para persistir o compartir datos fuera del contenedor. | Resuelven un problema central: los contenedores son descartables, pero muchos datos no deben desaparecer con ellos. |
| `compose` | Herramienta para definir y levantar varios servicios juntos. | Se vuelve clave cuando una app deja de ser un solo proceso y pasa a incluir base, backend, cache, etc. |
| `.env` | Archivo de variables de entorno usado para configuracion. | Ayuda a separar configuracion de codigo, algo muy util al cambiar entre entornos. |
| `multi-stage build` | Tecnica para construir imagenes finales mas chicas y limpias. | Permite usar etapas pesadas para compilar y despues entregar una imagen final mas liviana y segura. |

## Tabla comparativa rapida

| Concepto | Que es | Analogia util |
| --- | --- | --- |
| `imagen` | definicion del entorno | receta |
| `contenedor` | ejecucion concreta de esa definicion | plato servido |
| `Dockerfile` | instrucciones para crear la imagen | receta escrita |

## Mapa mental rapido

La logica del tema es esta:

```text
describo un entorno en un Dockerfile
-> construyo una imagen
-> ejecuto esa imagen como contenedor
-> conecto puertos y volumenes segun necesidad
-> y si hay varios servicios, los coordino con compose
```

Asi Docker se entiende como flujo, no como lista de comandos.

## Lo que mas se suele confundir

- `imagen` y `contenedor` no son lo mismo: la imagen define el entorno y el contenedor es la ejecucion concreta.
- un contenedor no es exactamente lo mismo que una maquina virtual; ambos aislan, pero lo hacen con mecanismos y costos distintos.
- exponer `puertos` y usar `volumenes` no son extras secundarios; suelen ser la diferencia entre un contenedor inutil y uno realmente aprovechable.

## Como leer este apunte

Este archivo conserva los temas del material largo, pero los reordena para explicar primero que problema resuelve Docker y despues como se organiza la herramienta.

## 1. Idea general

Docker es una plataforma para empaquetar y ejecutar aplicaciones dentro de contenedores.

La promesa principal es:

```text
si funciona en un entorno, deberia funcionar igual en otro
```

Eso no significa magia absoluta, pero si mucha mas reproducibilidad que instalar cosas manualmente en cada maquina.

## 2. Que problema resuelve

En desarrollo aparecen seguido estos problemas:

- en mi maquina funciona y en la tuya no;
- una app depende de versiones especificas;
- dos proyectos piden dependencias incompatibles;
- configurar un entorno nuevo lleva demasiado tiempo.

Docker ayuda porque encapsula:

- codigo;
- runtime;
- librerias;
- configuraciones base;
- parte del sistema necesario para correr la app.

## 3. Contenedor, imagen y Dockerfile

### Imagen

Una imagen es una plantilla inmutable que define el entorno.

Pensa la imagen como una receta ya armada.

### Contenedor

Un contenedor es una instancia en ejecucion de una imagen.

Pensa el contenedor como la receta ya "cocinada" y corriendo.

### Dockerfile

Es el archivo de texto que describe como construir una imagen.

Ejemplo:

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

Lectura:

1. parte de una imagen base;
2. define directorio de trabajo;
3. copia archivos;
4. instala dependencias;
5. define el comando de arranque.

## 4. Componentes principales

### Docker Engine

Es el motor que crea y ejecuta contenedores.

### Docker Hub

Es un registro de imagenes donde podes:

- descargar imagenes ya preparadas;
- subir imagenes propias;
- compartirlas.

### Volumenes

Persisten datos fuera del contenedor.

### Redes

Permiten que contenedores se comuniquen entre si o con el host.

## 5. Por que se usa Docker

- portabilidad entre entornos;
- aislamiento de dependencias;
- reproduccion consistente;
- despliegue mas sencillo;
- mejor integracion con CI/CD;
- menor costo de recursos que una maquina virtual completa.

## 6. Docker no es una maquina virtual

Esta diferencia es muy importante.

Una maquina virtual suele incluir:

- sistema operativo completo;
- kernel propio;
- mas costo de recursos.

Un contenedor:

- comparte el kernel del host;
- es mucho mas liviano;
- esta pensado para aislar procesos, no para emular una computadora entera.

## 7. Ciclo basico de trabajo

### Descargar una imagen

```bash
docker pull ubuntu
```

### Ejecutar un contenedor

```bash
docker run -it ubuntu
```

### Ver contenedores

```bash
docker ps
docker ps -a
```

### Construir una imagen propia

```bash
docker build -t mi-app .
```

### Ejecutar una imagen propia

```bash
docker run mi-app
```

## 8. Puertos

Muchas apps dentro de un contenedor escuchan en un puerto interno.

Si queres acceder desde fuera, tenes que mapear puertos.

Ejemplo:

```bash
docker run -p 8080:3000 mi-app
```

Lectura:

- `3000`: puerto interno del contenedor;
- `8080`: puerto expuesto en tu maquina.

## 9. Volumenes y bind mounts

### Volumen

Es almacenamiento gestionado por Docker, ideal para persistencia.

### Bind mount

Monta una carpeta del host dentro del contenedor.

Muy util en desarrollo porque deja editar codigo local y verlo dentro del contenedor.

Ejemplo conceptual:

```text
host ./proyecto -> contenedor /app
```

## 10. Variables de entorno

Sirven para desacoplar configuracion del codigo.

Ejemplos tipicos:

- puertos;
- usuarios;
- contrasenas;
- modos de entorno;
- claves de API.

Ejemplo:

```bash
docker run -e FLASK_ENV=development mi-app
```

## 11. Docker Compose

Compose sirve para definir y levantar varios servicios como una sola aplicacion.

Es util cuando tu sistema tiene, por ejemplo:

- backend;
- base de datos;
- cache;
- frontend.

En vez de levantar todo a mano, lo declaras en un archivo YAML.

### Ejemplo minimo

```yaml
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
    environment:
      - FLASK_ENV=development

  redis:
    image: redis:alpine
```

### Que expresa este archivo

- `web` se construye desde el proyecto local;
- expone puerto;
- monta codigo local;
- define variables;
- `redis` usa una imagen externa.

## 12. Comandos de Compose

```bash
docker compose up
docker compose up -d
docker compose down
docker compose build
docker compose logs
docker compose ps
docker compose exec web bash
```

Nota: hoy suele usarse `docker compose` en vez de `docker-compose`, aunque vas a encontrar ambos formatos en muchos apuntes.

## 13. Redes personalizadas

Docker puede crear redes virtuales para que los contenedores se hablen por nombre de servicio.

Ejemplo:

```yaml
networks:
  mynetwork:
    driver: bridge
```

Eso es util para aplicaciones de multiples servicios.

## 14. Archivos `.env`

Compose puede leer variables desde un archivo `.env`.

Ejemplo:

```env
MYSQL_ROOT_PASSWORD=clave123
PORT=3306
```

Y despues:

```yaml
services:
  db:
    image: mysql
    ports:
      - "${PORT}:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
```

La ventaja es que cambias configuracion sin tocar el YAML principal.

## 15. Multi-stage builds

Permiten construir en etapas y dejar la imagen final mas liviana.

Ejemplo:

```dockerfile
FROM node:20 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```

La idea es:

- usar una etapa pesada para construir;
- y una final mas chica para ejecutar.

## 16. Cosas que conviene no confundir

### Imagen vs contenedor

- imagen: definicion;
- contenedor: instancia en ejecucion.

### Persistencia

Si el contenedor se borra, sus cambios internos pueden perderse.

Si los datos importan, conviene usar volumenes.

### Docker y seguridad

Docker ayuda a aislar, pero no convierte automaticamente una aplicacion en segura.

## 17. Resumen final

Ideas que conviene retener:

- Docker empaqueta entornos;
- la imagen define, el contenedor ejecuta;
- el Dockerfile construye la imagen;
- Compose organiza varios servicios;
- puertos exponen apps;
- volumenes guardan datos;
- `.env` desacopla configuracion;
- multi-stage builds ayudan a optimizar.

----
Apunte de @milagrosarganin

# 🐳 Docker

## ❓ ¿Qué es?


> Es un contenedor que engloba todo lo que necesitamos para correr una app en cualquier compu. Instala/guarda todas las dependencias en un contenedor y, al correr eso, solucionamos el problema de *"solo anda en mi computadora"*.

---

##  Conceptos Fundamentales

### 🖥️ Host
**Es tu compu o el servidor donde estás trabajando.**
- El host es donde está el SO y ahí se instala Docker.

### ⚙️ Servicio
**Programa/app que está corriendo.**

### 📦 Contenedores vs Virtualización
- Antes se usaban VMs para aislar apps, eso pesaba varios GB y hacía más lenta la PC.
- Con Docker **no** se instala un SO completo, porque comparte núcleo con el SO del host. Están diseñados para crearse y destruirse fácilmente.

### 💡 Notas Clave
- *Docker recibe indicaciones por medio de la terminal.*
- *Docker une contenedores por sus nombres a través de redes virtuales en vez de hacerlo con IPs complicadas.*

---

## 🖼️ Imágenes y Dockerfile (La Receta)

### 🖼️ Imágenes
- Un archivo de **solo lectura**.
- Contiene el SO, el código y las librerías.
- <span class="important">NO</span> se puede modificar.
- Si se quiere cambiar algo, se crea una nueva.

### 📄 Dockerfile
> Es la **"receta"** para crear la imagen. Un Dockerfile es simplemente un archivo de texto con instrucciones secuenciales.

#### 📜 Instrucciones Vitales del Dockerfile
- **`FROM`**: Es la imagen base sobre la que se construye, usualmente un SO (ej. `ubuntu:latest`).
- **`WORKDIR` (El Escritorio)**: Establece el directorio de trabajo interno del contenedor. Es como hacer `cd`. Todo lo que hagas después (copiar, ejecutar) sucederá en esa carpeta.
  - *Ejemplo: `WORKDIR /app`*
- **`COPY` (La Transferencia)**: Toma archivos de tu computadora (Host) y los pega dentro del contenedor.
  - *Ejemplo: `COPY . .` (Copia todo desde tu carpeta actual a la carpeta de trabajo del contenedor).*
- **`ADD`**: Similar a `COPY`, pero con más funcionalidades como descomprimir archivos `.tar` automáticamente. Generalmente se prefiere `COPY` por ser más explícito.
- **`RUN` (El Constructor)**: Ejecuta comandos de consola **mientras la imagen se está construyendo**. Se usa para instalar dependencias.
  - *Ejemplo: `RUN apt-get update && apt-get install -y python`*
- **`ENV` (Las Variables)**: Define variables de entorno que estarán disponibles cuando el contenedor esté vivo. Útil para pasar configuraciones sin escribirlas en el código.
  - *Ejemplo: `ENV PORT=8080`*
- **`CMD` (El Botón de Encendido)**: Es el comando por defecto que se va a ejecutar **cuando el contenedor arranque** (no cuando se construya).
  - *Ejemplo: `CMD ["python", "app.py"]`*

### 📝 Ejemplo Práctico de Creación

Los Dockerfile siempre empiezan con `FROM` y casi siempre terminan con `CMD`.

1.  **Crear el `Dockerfile`**:
    ```dockerfile
    # Empezá con un sistema Ubuntu básico
    FROM ubuntu:24.04
    
    # Cuando el contenedor arranque, ejecutá la terminal de linux
    CMD ["bash"]
    ```

2.  **🏗️ Construir la Imagen (Empaquetar los ingredientes)**
    Primero, le dices a Docker que lea tu archivo y cree la Imagen. Para eso usas el comando: `docker build -t mi-ubuntu-personalizado .`
    - `build`: Le dice a Docker que construya algo.
    - `-t mi-ubuntu-personalizado`: Le pone una "etiqueta" (nombre) a tu imagen para que la encuentres fácil.
    - `.` (el punto al final): Es súper importante. Le dice a Docker "busca el Dockerfile en esta carpeta actual".

3.  **🚀 Ejecutar el Contenedor (Servir el plato)**
    Ahora que tienes la Imagen, vas a crear un contenedor vivo a partir de ella con el comando: `docker run -it mi-ubuntu-personalizado`
    - `run`: Ejecuta un contenedor.
    - `-it`: Mantiene la terminal abierta e interactiva (necesario porque en tu Dockerfile pusimos que ejecute `bash`).

¡Y listo! Tu terminal cambiará y estarás "dentro" de un mini-sistema operativo Ubuntu.

---

## 💻 Comandos de la Terminal

### 🛠️ Manejo de Imágenes *(Las Plantillas)*
- `docker images`: Lista todas las imágenes que tienes descargadas en tu máquina.
- `docker pull <nombre_imagen>`: Descarga una imagen de internet sin ejecutarla *(ej. `docker pull ubuntu`)*.
- `docker rmi <id_imagen>`: Borra una imagen de tu computadora para liberar espacio.
- `docker build -t <nombre> .`: Construye una imagen propia a partir de un archivo `Dockerfile` en la carpeta actual.

### 📦 Manejo de Contenedores *(Las Cajas en ejecución)*
- `docker ps`: Lista los contenedores que están corriendo en este momento.
- `docker ps -a`: Lista todos los contenedores (los que están corriendo y los que están apagados/detenidos).
- `docker run <nombre_imagen>`: Crea y arranca un contenedor a partir de una imagen.
- `docker run -d <nombre_imagen>`: La `-d` *(detached)* hace que corra en segundo plano para que puedas seguir usando tu terminal.
- `docker stop <id_contenedor>`: Detiene un contenedor que está corriendo (lo apaga de forma segura).
- `docker start <id_contenedor>`: Vuelve a prender un contenedor que estaba detenido.
- `docker rm <id_contenedor>`: Borra un contenedor (tiene que estar detenido primero). **Ojo:** Esto no borra la imagen original.

### 🔍 Diagnóstico y Control
- `docker logs <id_contenedor>`: Te muestra qué está pasando dentro del contenedor *(útil si tu app tira un error y quieres leerlo)*.
- `docker exec -it <id_contenedor> /bin/bash`: "Te mete" dentro del contenedor. Es como abrir una terminal directamente adentro de esa caja para revisar archivos.

---

## 🔌 Puertos y Redes

- Un **puerto** es un punto lógico de comunicación. No se puede tener dos procesos en un mismo puerto del mismo host/contenedor.
- Docker aísla la red de los contenedores. Son como departamentos en un edificio (el host).

### 🔗 Mapeo de Puertos
Para que podamos ver una app web desde nuestra computadora, tenemos que hacer un **Mapeo de Puertos**: conectar un puerto de tu computadora (Host) a un puerto del contenedor.

- Para hacer esto, le agregamos el flag `-p` al comando `run`: `docker run -d -p 8080:80 mi-app-web`

#### ¿Qué significa `8080:80`?
- **El de la izquierda (8080)**: Es el puerto de tu computadora. Puedes elegir casi cualquier número libre.
- **El de la derecha (80)**: Es el puerto interno del contenedor donde la aplicación está escuchando (Nginx, por defecto, usa el 80).

Al ejecutar ese comando, puedes abrir el navegador en `localhost:8080` y verás tu página.

---

## 💾 Volúmenes y Persistencia de Datos

> En Docker los contenedores son **efímeros** (se pueden crear y destruir fácilmente). Si borramos un contenedor, se pierde toda la info que contenía. Para guardar datos importantes de forma permanente, usamos **Volúmenes** o **Bind Mounts**.

### 🗄️ Volúmenes Gestionados por Docker
- Son espacios de almacenamiento que Docker crea y administra de forma 100% aislada dentro de una parte protegida de tu sistema.
- **¿Cuándo usarlos?** Casi exclusivamente para Bases de Datos (como MySQL) o archivos críticos que genera la aplicación.
- **¿Por qué?** Porque no necesitas ver los archivos internos de la base de datos. Solo te interesa que estén seguros, que no se borren por accidente y que Docker los maneje de la forma más rápida y segura posible.

### 🔗 Bind Mounts (El Portal Mágico)
Un "Bind Mount" es un puente directo que conecta una carpeta específica de tu computadora con una ruta dentro del contenedor.

#### 🔄 ¿Cómo funciona la bidireccionalidad?
- No es una copia, es un **espejo en tiempo real**.
- Si modificas un archivo `index.html` en tu editor de código, el contenedor ve ese cambio al instante.
- Si un proceso dentro del contenedor crea un archivo nuevo en esa carpeta, el archivo aparecerá mágicamente en tu computadora.
- Tu computadora (el Host) **SIEMPRE** manda y tiene la prioridad. Si tu carpeta local y la imagen del contenedor tienen un archivo con el mismo nombre en la misma ruta, el tuyo "tapa" o "eclipsa" al del contenedor.

### 🏗️ ¿Cómo aplicar esto en la arquitectura de un proyecto?
- **Para el Frontend (HTML/CSS/JS): ¡Usa Bind Mounts!** Te permite desarrollar en vivo. Escribes código, guardas, recargas el navegador y ves los cambios al instante sin tener que reconstruir la imagen (`docker build`) cada vez.
- **Para la Base de Datos (SQL): ¡Usa Volúmenes Gestionados!** Garantizas que los registros de tu base de datos sobrevivan de forma segura sin importar cuántas veces apagues o destruyas el contenedor.

---

## 🐙 Docker Compose

- Es una herramienta que te permite definir, configurar y ejecutar múltiples contenedores (servicios) como si fueran una sola aplicación unificada.
- Es ideal para arquitecturas que requieren varios servicios interconectados (ej. una web y su base de datos).
- Todo esto se orquesta desde un único archivo llamado `docker-compose.yml`.

### 📄 ¿Qué es YAML (`.yml`)?
- Es un formato de archivo muy sencillo para configuraciones. Depende de la indentación (los espacios) para organizar la información, similar a Python.

### ⚙️ Ejemplo de `docker-compose.yml`
En la carpeta de tu proyecto, crearías un archivo `docker-compose.yml`:

```yaml
version: '3.8' # La versión del formato de Compose

services: # Aquí listamos todos nuestros contenedores
  # SERVICIO 1: Tu página web
  mi-pagina-web:
    build: . # Le dice a Compose: "Construye el Dockerfile que está en esta carpeta"
    ports:
      - "8080:80" # Mapeamos el puerto como te expliqué arriba
    volumes:
      # Esto es un BIND MOUNT para desarrollo en vivo
      - ./mi-codigo-web:/usr/share/nginx/html

  # SERVICIO 2: Tu base de datos SQL
  mi-base-de-datos:
    image: mysql:8.0 # En lugar de construir, le decimos que descargue la imagen oficial
    environment: # Las variables secretas para que arranque la base
      - MYSQL_ROOT_PASSWORD=mi_clave_secreta
      - MYSQL_DATABASE=proyecto_final
    volumes:
      # Esto es un VOLUMEN GESTIONADO para persistir los datos
      - datos-sql:/var/lib/mysql

volumes:
  # Aquí se declara formalmente el volumen gestionado por Docker
  datos-sql:
```

Con este archivo, te olvidas de comandos largos. Simplemente ejecutas:
- `docker-compose up`: Lee el archivo, construye, descarga y levanta todo.
- `docker-compose down`: Apaga y elimina los contenedores.

---

### 🤔 ¿Cuándo y para qué uso Docker realmente?

Docker brilla en situaciones donde necesitas **aislamiento, portabilidad y reproducibilidad**.

- **Para matar el "en mi máquina sí funciona"**: Empaquetas tu app con su propio entorno. Si el contenedor funciona en tu PC, funcionará exactamente igual en cualquier otro lado.
- **Para no ensuciar tu computadora**: ¿Quieres probar una nueva base de datos o una versión antigua de Python? Levantas un contenedor. Cuando terminas, lo borras y tu PC queda impecable.
- **Para trabajar en equipo**: Un desarrollador nuevo solo necesita ejecutar `docker-compose up` y en minutos tiene todo el entorno de trabajo listo, sin pasar días instalando y configurando.

```dockerfile
FROM ubuntu:24.04
...
CMD ["bash"]
```

```yml
services: 
  db:
    image: postgres:17
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: nuestra_db
    volumes:
      - ./.volumes/db:/var/lib/postgresql/data  
      #.: Significa "aquí mismo" (la carpeta clases).
      #/.volumens/postgres/data: Es la ruta hacia la carpeta donde quieres que se guarden los archivos binarios de la base de datos en tu computadora.
      #:/var/lib/postgresql/data/: Es la ruta interna del contenedor (esa NO la debes cambiar, es donde Postgres guarda todo por defecto).
    ports:
      - "5432:5432"
      ```