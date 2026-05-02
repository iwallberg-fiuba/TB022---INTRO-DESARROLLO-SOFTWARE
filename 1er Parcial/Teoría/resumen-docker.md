# Apunte largo - Docker

## Fuentes trabajadas

- `slides.html`
- `Mastering_Custom_Docker_Images.pptx`
- `Docker_Data_Architecture.pptx`

## Idea global del tema

Docker aparece en el material como una respuesta practica a un problema de entornos: misma app, distinto resultado segun la maquina. La propuesta no es solo "correr cosas en contenedores", sino estandarizar:

- dependencias,
- forma de construccion,
- forma de despliegue,
- persistencia,
- networking,
- permisos,
- y colaboracion entre integrantes del equipo.

El mensaje de fondo de los materiales es que Docker no es solo una herramienta de comandos, sino una manera de describir y reproducir entornos.

## 1. El problema que Docker resuelve

### El clasico "en mi maquina funciona"

El material lo presenta como un problema estructural del desarrollo:

- distintos sistemas operativos,
- distintas versiones de librerias,
- distintas variables de entorno,
- distintas dependencias del sistema,
- diferencias entre entorno local y produccion.

### La promesa de Docker

- Empaquetar la app con lo que necesita.
- Poder ejecutarla igual en laptop, servidor o nube.
- Reducir el costo de onboarding.
- Hacer reproducible el entorno de testing y desarrollo.

### Donde se usa segun el material

- Desarrollo local.
- Onboarding de nuevos integrantes.
- Testing.
- CI/CD.
- Produccion.
- Microservicios.
- Base de datos para pruebas reproducibles.

## 2. Contenedores vs virtualizacion

### Virtualizacion tradicional

La VM abstrae a nivel hardware:

- cada VM tiene sistema operativo completo,
- el aislamiento es fuerte,
- el costo en recursos es alto,
- el arranque es mas lento,
- el tamano tipico es grande.

### Contenedores

El contenedor abstrae a nivel sistema operativo:

- comparte el kernel del host,
- incluye solo aplicacion y dependencias necesarias,
- arranca como proceso, no como un boot de SO completo,
- es mucho mas liviano,
- tiene aislamiento logico.

### Comparacion del material

- VM: gigabytes, minutos, kernel propio, hipervisor.
- Contenedor: megabytes, segundos, kernel compartido, namespaces y cgroups.

### Detalle importante

Los materiales remarcan que no son excluyentes:

- una arquitectura real puede correr contenedores dentro de VMs,
- combinando portabilidad de Docker con aislamiento de infraestructura.

## 3. Conceptos base: imagen, contenedor, puerto, volumen

### Imagen

La imagen es la receta.

- Es inmutable.
- Es de solo lectura.
- Es estatica.
- Contiene sistema base, dependencias y codigo o artefactos.
- Puede instanciarse muchas veces.

### Contenedor

El contenedor es la instancia viva de una imagen.

- Es un proceso aislado en ejecucion.
- Tiene una capa volatil de lectura/escritura.
- Todo cambio hecho solo ahi desaparece al destruirlo.

### Puerto

- Es un punto logico de comunicacion.
- El servicio escucha adentro del contenedor.
- Para hacerlo visible desde afuera, Docker publica o mapea puertos.

### Volumen

- Es la pieza que desacopla datos del ciclo de vida efimero del contenedor.
- Permite persistencia real.

## 4. El sistema de capas

Los slides de "Mastering Custom Docker Images" lo explican con bastante claridad:

- las imagenes se construyen en capas apiladas,
- cada instruccion del Dockerfile como `RUN`, `COPY` o `ADD` crea una nueva capa,
- esas capas son de solo lectura e inmutables una vez creadas,
- el contenedor agrega por arriba una capa de lectura/escritura volatil.

### Consecuencia operativa importante

Si haces un cambio en tiempo de ejecucion dentro del contenedor:

- el cambio vive en la capa volatil,
- desaparece cuando el contenedor se destruye,
- no modifica la imagen original.

### Cache de capas

Docker reutiliza capas ya construidas para compilar mas rapido. Eso explica por que:

- el orden del Dockerfile importa,
- cambios en una instruccion pueden invalidar cache de las de abajo,
- conviene estabilizar primero capas costosas y cambiantes por separado.

## 5. Flujo basico de trabajo con Docker

### Construccion

1. Tenes un directorio local con codigo.
2. Escribis un `Dockerfile`.
3. Ejecutas `docker build -t mi-app:1.0 .`
4. Docker toma el contexto y procesa linea por linea.
5. Genera una imagen.

### Ejecucion

1. Elegis una imagen.
2. La instancias con `docker run`.
3. El proceso arranca dentro del contenedor.
4. Si hace falta, publicas puertos y montas volumenes.

## 6. Comandos fundamentales de Docker CLI

### Imagenes

- `docker pull nginx`
- `docker images`
- `docker rmi python:3.12`
- `docker build -t nombre .`

### Contenedores

- `docker run ...`
- `docker ps`
- `docker ps -a`
- `docker logs <id>`
- `docker exec -it <id> sh`
- `docker stop <id>`
- `docker start <id>`
- `docker rm <id>`

### Volumenes

- `docker volume ls`
- `docker volume inspect <nombre>`
- `docker volume rm <nombre>`
- `docker volume prune`

## 7. `docker run` y lectura del comando

Uno de los slides explica este ejemplo:

```bash
docker run -d --name mi-bd -v datos-api:/var/lib/mysql mysql:8.0
```

### Como leerlo

- `docker run`: crea e inicia un contenedor.
- `-d`: modo detached, en segundo plano.
- `--name mi-bd`: nombre humano del contenedor.
- `-v datos-api:/var/lib/mysql`: monta persistencia.
- `mysql:8.0`: imagen base a usar.

### Lectura del `-v`

- `datos-api`: origen persistente.
- `:`: puente de mapeo.
- `/var/lib/mysql`: destino dentro del contenedor.

El material lo presenta casi como un cordon umbilical entre contenedor volatil y almacenamiento persistente.

## 8. Puertos y exposicion de servicios

### Idea conceptual

Los servicios escuchan en puertos internos del contenedor. Docker aisla la red, por lo que desde afuera no ves esos puertos a menos que los publiques.

### Sintaxis clave

```bash
docker run -p 8080:80 nginx
```

### Interpretacion

- `8080` = puerto del host.
- `80` = puerto del contenedor.

Si visitas `localhost:8080`, el trafico termina llegando al proceso que escucha en el `80` del contenedor.

### Error conceptual comun

Creer que `EXPOSE 8080` publica un puerto.

No. `EXPOSE` solo documenta. La publicacion real ocurre con:

- `-p`,
- `--publish`,
- o configuracion equivalente en Compose.

## 9. Persistencia: el problema central del estado

El deck `Docker_Data_Architecture.pptx` enfatiza esto como el gran punto de arquitectura de datos en Docker.

### La trampa de la efimeridad

Por defecto:

- el contenedor vive en un filesystem de union,
- la capa de escritura se pierde al destruir el contenedor,
- si una base de datos escribe ahi, los datos mueren con el contenedor.

### Mensaje arquitectonico

Los contenedores son ganado, no mascotas:

- no se "curan" a mano,
- se reemplazan,
- por eso el estado importante tiene que vivir afuera.

## 10. Estrategias de almacenamiento

El material compara tres estrategias.

### A. Volumen Docker

#### Que es

- Gestionado por el daemon Docker.
- Generalmente ubicado bajo `/var/lib/docker/volumes/`.

#### Propiedades

- Persistencia alta.
- Portabilidad muy alta.
- Aislamiento fuerte respecto de otros procesos del host.

#### Casos ideales

- Bases de datos.
- Archivos de usuarios.
- Datos que deben sobrevivir recreaciones de contenedor.

#### Mensaje del material

Es la estrategia recomendada.

### B. Bind mount

#### Que es

- Montaje directo de una ruta especifica del host dentro del contenedor.

#### Propiedades

- Persistencia alta.
- Portabilidad baja, porque depende de la estructura del host.

#### Casos ideales

- Desarrollo local.
- Inyeccion de codigo fuente.
- Editar desde el host y ver cambios dentro del contenedor.

### C. Tmpfs

#### Que es

- Montaje en RAM del host.

#### Propiedades

- Persistencia nula.
- Volatil.
- Muy rapido.

#### Casos ideales

- caches rapidos,
- credenciales temporales,
- datos descartables en Linux.

## 11. Matriz comparativa para memorizar

### Volumen Docker

- Gestionado por: daemon Docker.
- Persistencia: alta.
- Portabilidad: muy alta.
- Caso ideal: base de datos y datos de usuario.

### Bind mount

- Gestionado por: usuario y filesystem del host.
- Persistencia: alta.
- Portabilidad: baja.
- Caso ideal: desarrollo local.

### Tmpfs

- Gestionado por: RAM del host.
- Persistencia: nula.
- Portabilidad: no aplica como almacenamiento persistente.
- Caso ideal: caches temporales.

## 12. Topografia de montajes

El slide de topografia lo muestra de forma muy clara:

- host RAM -> contenedor `/app/cache` con `tmpfs`,
- host ruta del proyecto -> contenedor `/usr/src/app` con bind mount,
- volumen Docker -> contenedor `/var/lib/mysql`.

### Idea fuerte

No todo dato debe montarse igual. El tipo de storage depende del tipo de informacion.

## 13. Docker Compose

### Para que existe

Para definir aplicaciones multi-contenedor como infraestructura declarativa.

### Que permite

- declarar servicios,
- declarar puertos,
- declarar volumenes,
- declarar redes,
- levantar todo con un solo comando.

### Concepto importante del material

Declarar volumenes a nivel superior del archivo Compose permite:

- que persistan aunque el contenedor suba y baje,
- que varias replicas compartan el mismo estado fisico,
- separar infraestructura de almacenamiento del ciclo de vida puntual de cada servicio.

### Ejemplo conceptual del slide

Dos servicios `web-app-v1` y `web-app-v2` montan el mismo volumen `datos-api:/app/uploads`.

### Lectura arquitectonica

Eso muestra dos cosas:

- Compose orquesta estado compartido.
- El volumen no pertenece "a mano" a un solo contenedor; es un recurso declarativo del stack.

### Comandos de Compose

- `docker compose up -d`
- `docker compose ps`
- `docker compose logs -f`
- `docker compose down`
- `docker compose down -v`

### Cuidado con `down -v`

Ese comando tambien elimina volumenes. Para datos importantes hay que usarlo con criterio.

## 14. Networking entre contenedores

### Idea base

Docker crea una red aislada para los contenedores.

### Consecuencias

- los contenedores estan aislados por defecto,
- para exponer servicios al host se usa `-p`,
- en Compose los servicios se resuelven por nombre,
- Docker ofrece DNS interno automatico.

### Mensaje importante

No hace falta conectar servicios por IP fija. El nombre del servicio actua como identidad de red dentro del stack.

## 15. Dockerfile: la definicion del entorno

El Dockerfile aparece como un manifiesto:

- documenta como se arma la imagen,
- automatiza la construccion,
- vuelve reproducible el entorno,
- es infraestructura como codigo.

## 16. Instrucciones fundamentales del Dockerfile

### `FROM`

- Define la imagen base.
- Determina el tamaño inicial y buena parte de la seguridad.
- El slide la llama "los cimientos".

### `WORKDIR`

- Define el directorio de trabajo interno.
- Es mejor que andar usando `cd` en distintas instrucciones.
- Hace mas legible el Dockerfile.

### `USER`

- Baja privilegios.
- Muy importante para seguridad.
- Docker corre como root por defecto si no se cambia.

### `COPY`

- Copia archivos del host al contenedor o imagen.
- Es simple, transparente y predecible.
- El material recomienda preferirlo.

### `ADD`

- Puede hacer mas que `COPY`:
- extraer `.tar`,
- descargar desde URL,
- comportamientos adicionales.

Por eso el material recomienda usarlo con extrema cautela. No porque sea "malo", sino porque agrega magia y menos previsibilidad.

### `RUN`

- Ejecuta comandos en build time.
- Genera una nueva capa inmutable.
- Se usa para instalar dependencias, crear carpetas, ajustar permisos, etc.

### `ENV`

- Variables disponibles en tiempo de ejecucion del contenedor vivo.
- Ejemplo conceptual: credenciales, modo de la app, flags.

### `ARG`

- Variables solo de build time.
- Desaparecen una vez compilada la imagen.
- Utiles para inyectar versiones o parametros de construccion.

### `EXPOSE`

- Documenta el puerto interno.
- No publica automaticamente al host.

### `CMD`

- Define el comando por defecto al iniciar el contenedor.

## 17. `COPY` vs `ADD`

### `COPY`

- hace una transferencia directa,
- es mas explicito,
- menos sorpresas,
- preferido en la mayoria de casos.

### `ADD`

- agrega comportamientos especiales,
- puede descomprimir o descargar,
- por eso se reserva para casos donde realmente hace falta.

### Regla de estudio

Si te preguntan cual usar por defecto:

- `COPY`.

Si te preguntan cuando `ADD`:

- cuando queres especificamente sus capacidades extra y sos consciente del costo de complejidad.

## 18. Buenas practicas de imagenes segun los slides

### 1. Usar imagenes base oficiales y minimalistas

Ejemplo del material: Alpine.

#### Por que

- menor tamaño,
- menos superficie de ataque,
- builds mas rapidos,
- menos paquetes innecesarios.

### 2. Agrupar comandos en un solo `RUN`

El slide dice explicitamente que multiples comandos en un solo `RUN` minimizan capas inutiles.

#### Idea clave

- 1 `RUN` = 1 capa.

### 3. Usar `.dockerignore`

Para evitar copiar basura al contexto de construccion:

- `node_modules`,
- logs,
- archivos temporales,
- cualquier cosa innecesaria.

#### Por que importa

- menor contexto,
- build mas rapido,
- menos riesgo de incluir basura o secretos.

### 4. No limpiar caches en un `RUN` posterior

El slide remarca este error:

- instalar en una capa,
- limpiar en otra,
- creer que eso "borro" el peso.

No. El historial de capas conserva el contenido previo. Si queres limpiar, hacelo en la misma instruccion.

## 19. Seguridad y permisos

El slide de permisos y propiedad explica uno de los errores mas comunes.

### Problema tipico

- Host con usuario `UID 1000`.
- App dentro del contenedor corre con `UID 1001`.
- El proceso intenta escribir sobre un volumen cuyo propietario real en el host es otro.
- Resultado: `Permission denied`.

### Idea arquitectonica

Arquitecturas seguras quieren usuarios no-root, pero eso obliga a pensar permisos correctamente.

### Soluciones mencionadas

- igualar mapeo `UID/GID`,
- ejecutar `chown` en inicializacion si corresponde,
- configurar bien `USER` en Dockerfile,
- mapear permisos antes del arranque.

### Error comun

Resolver todo corriendo como root.

Eso puede "hacer que ande", pero empeora seguridad y esquiva el problema real.

## 20. Frases clave del material que conviene internalizar

- Los contenedores se reemplazan, no se reparan.
- La persistencia debe vivir fuera del contenedor.
- Las imagenes son inmutables; el contenedor es efimero.
- `EXPOSE` no publica puertos.
- Un volumen Docker es la opcion mas portable para datos persistentes.
- `COPY` es la opcion segura por defecto.
- `USER` no es decorativo: es seguridad.

## 21. Confusiones frecuentes para examen

### Confusion 1

Pensar que imagen y contenedor son lo mismo.

No:

- imagen = receta,
- contenedor = instancia viva.

### Confusion 2

Pensar que destruir el contenedor destruye siempre los datos.

No, solo si los datos vivian en la capa volatil y no en volumen/bind/tmpfs segun el caso.

### Confusion 3

Pensar que `EXPOSE` publica un puerto.

No. Solo documenta.

### Confusion 4

Pensar que bind mount y volumen Docker son equivalentes.

No:

- bind mount acopla al host,
- volumen Docker es mas portable y gestionado por Docker.

### Confusion 5

Pensar que limpiar en otra capa reduce la imagen.

No. Las capas anteriores siguen en el historial.

## 22. Posibles preguntas de parcial

1. Explica por que Docker ayuda a resolver el problema "en mi maquina funciona".
2. Diferencia entre maquina virtual y contenedor.
3. Diferencia entre imagen y contenedor.
4. Que significa que una imagen sea inmutable.
5. Que problema resuelve un volumen.
6. Compara volumen Docker, bind mount y tmpfs.
7. Explica el significado de `-p 8080:80`.
8. Explica el significado de `-v datos-api:/var/lib/mysql`.
9. Que hace `EXPOSE` y que no hace.
10. Diferencia entre `COPY` y `ADD`.
11. Diferencia entre `ENV` y `ARG`.
12. Por que conviene usar `USER`?
13. Por que no conviene limpiar caches en una capa posterior?
14. Que ventaja aporta Docker Compose en aplicaciones multi-contenedor?
15. Como aparece el problema de permisos entre host y contenedor?

## 23. Memorizacion rapida

- Docker estandariza entornos.
- Imagen = receta inmutable.
- Contenedor = proceso aislado con capa volatil.
- VM = hardware virtualizado; contenedor = kernel compartido.
- `-p` publica puertos.
- `-v` persiste datos.
- Volumen Docker = recomendado para estado real.
- Bind mount = ideal para desarrollo.
- Tmpfs = RAM, volatil.
- `FROM`, `WORKDIR`, `USER`, `COPY`, `RUN`, `ENV`, `ARG`, `EXPOSE`, `CMD` son el nucleo del Dockerfile.
- `.dockerignore` y `USER` son buenas practicas clave.
