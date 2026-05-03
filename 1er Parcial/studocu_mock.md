### Distribucion

- Seccion 1: Opcion multiple, 20 preguntas
- Seccion 2: Respuesta breve, 6 preguntas
- Seccion 3: Respuesta larga, 3 preguntas

---

## Seccion 1 / 3 - Opcion multiple

Seleccione la unica opcion correcta para cada pregunta. Cada acierto suma 2 puntos.


### Pregunta 2

Cual de los siguientes comandos de Git se utiliza para registrar de forma definitiva los cambios almacenados en el area de preparacion (`staging area`)?

- A. `git add`
- B. `git push`
- C. `git commit`
- D. `git status`

### Pregunta 3

En la jerarquia de archivos de Linux, ?que simbolo representa al directorio padre del directorio actual?

- A. `..`
- B. `.`
- C. `root`
- D. `~`

### Pregunta 4

Que rol en el marco de trabajo Scrum es responsable de maximizar el valor del producto y gestionar el Product Backlog?

- A. `Scrum Master`
- B. `Development Team`
- C. `Stakeholder`
- D. `Product Owner`

### Pregunta 6

En SQL, ?cual es la diferencia principal entre `DROP` y `DELETE`?

- A. `DELETE` borra la tabla completa; `DROP` borra solo filas.
- B. `DROP` es para bases de datos NoSQL; `DELETE` es para SQL.
- C. Ambos comandos son identicos en su funcionalidad.
- D. `DROP` borra la estructura y los datos de la tabla; `DELETE` borra solo el contenido de las filas.


### Pregunta 8

Que comando de Bash permite filtrar lineas de un archivo que coincidan con un patron de texto especifico?

- A. `grep`
- B. `mkdir`
- C. `cat`
- D. `ls`

### Pregunta 9

?Cual es la funcion de una `Primary Key` en una tabla relacional?

- A. Almacenar archivos binarios pesados.
- B. Vincular la tabla con una API externa.
- C. Identificar de forma unica cada fila de la tabla.
- D. Permitir que la tabla tenga multiples nombres.

### Pregunta 11

?Que comando se utiliza en Git para descargar el historial de un repositorio remoto y fusionarlo automaticamente con la rama local actual?

- A. `git pull`
- B. `git checkout`
- C. `git fetch`
- D. `git remote add`

### Pregunta 12

En el contexto de Ingenieria de Software, ?cual es la etapa donde se definen las necesidades del cliente y el alcance del proyecto?

- A. Implementacion
- B. Pruebas (`Testing`)
- C. Mantenimiento
- D. Analisis de Requerimientos


### Pregunta 16

Que operador de Bash se utiliza para redirigir la salida de un comando y anadirla al final de un archivo sin sobrescribir el contenido existente?

- A. `||`
- B. `>`
- C. `>>`
- D. `&`

### Pregunta 17

Si desea eliminar todos los registros de una tabla llamada `Usuarios` pero mantener la estructura de la misma de la forma mas eficiente posible, ?que comando SQL deberia usar?

- A. `REMOVE * FROM Usuarios;`
- B. `DELETE FROM Usuarios;`
- C. `TRUNCATE TABLE Usuarios;`
- D. `DROP TABLE Usuarios;`

### Pregunta 18

?Que archivo se utiliza comunmente en Git para listar patrones de nombres de archivos y directorios que el sistema debe ignorar?

- A. `.gitconfig`
- B. `README.md`
- C. `.gitignore`
- D. `.gitattribute`

### Pregunta 20

En la Ingenieria de Software, ?que es un `Hotfix`?

- A. Un cambio en el color de la interfaz de usuario.
- B. Un proceso de documentacion de codigo.
- C. Una correccion urgente de un error critico en el entorno de produccion.
- D. Una nueva funcionalidad pedida por el cliente para el proximo ano.

---

## Seccion 2 / 3 - Respuesta breve

Responda de manera concisa a cada pregunta. Cada respuesta vale 5 puntos.

### Pregunta 21

Explique la diferencia entre una ruta absoluta y una ruta relativa en el sistema de archivos de Linux.

### Pregunta 22

Describa que sucede exactamente cuando un desarrollador ejecuta el comando `git pull`.

### Pregunta 23

?Cual es la funcion del objeto `request` en una aplicacion Flask?

### Pregunta 24

Diferencie entre una `Primary Key` y una `Foreign Key` en el diseno de una base de datos.


---

## Seccion 3 / 3 - Respuesta larga

Resuelva los siguientes ejercicios detallando su procedimiento. Cada ejercicio vale 10 puntos.

### Pregunta 27

Usted debe disenar una base de datos para una tienda de videojuegos. Se requiere almacenar informacion de **Videojuegos** (`ID`, `Titulo`, `Precio`, `ID_Categoria`) y **Categorias** (`ID`, `Nombre`).

Ademas, se necesita realizar una consulta para obtener una lista de todos los videojuegos cuyo precio sea mayor a `$60` y que pertenezcan a la categoria `Accion`.

1. Escriba la sentencia SQL para crear la tabla de **Videojuegos**, asegurandose de definir correctamente las claves primaria y foranea.
2. Escriba la consulta SQL solicitada en el caso para filtrar los videojuegos de `Accion` con precio superior a `$60`.

### Pregunta 28

En un servidor Linux, un desarrollador necesita limpiar un directorio de descargas. El objetivo es mover todos los archivos con extension `.log` a una carpeta llamada `backup`, pero solo si el archivo fue creado/modificado hoy. El desarrollador decide crear un script de Bash para automatizar esta tarea.

Disene un script de Bash, o describa los comandos necesarios con sus flags, que realice lo siguiente:

1. Cree el directorio `backup` si no existe.
2. Busque todos los archivos `.log` en el directorio actual.
3. Mueva dichos archivos al directorio `backup`.
4. Explique brevemente cada comando utilizado.

### Pregunta 29

Usted esta trabajando en una rama llamada `feature-login`. Al intentar fusionar sus cambios a la rama `main`, Git le informa que existe un conflicto en el archivo `auth.js` porque otro companero modifico la misma linea de codigo que usted.

Describa paso a paso el procedimiento tecnico y profesional que debe seguir para resolver este conflicto de forma segura, desde la deteccion hasta que los cambios queden integrados en el repositorio remoto.

---