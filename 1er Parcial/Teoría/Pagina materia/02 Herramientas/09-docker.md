
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


