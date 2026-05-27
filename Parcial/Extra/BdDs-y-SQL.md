
<br><br>

### Table of Contents

<br>

> [!NOTE]
> Usar modo `Full Screen`, disminuir / aumentar el `zoom` y abrir el `Outline` para una mejor lectura.

<br>

[Bases](#bases)
- [Conceptos Claves](#conceptos-claves) 
- [Ventajas de uso](#ventajas-de-uso)

<br>

[Convenciones](#convenciones)
- [Sobre Queries](#sobre-queries)
- [Sobre Configs](#sobre-configs)

<br>

[Diseño](#diseño)
- [CRUD](#crud)
- [Tipos de datos](#tipos-de-datos)
- [Restricciones de datos](#restricciones-de-datos)
- [Tablas para 1:1](#tablas-para-11)
- [Tablas para 1:N](#tablas-para-1n)
- [Tablas para N:N](#tablas-para-nn)
- [N:N Avanzado](#nn-avanzado)

<br>

[Queries](#queries)
- [en SELECT](#en-select)
- [Después de FROM](#después-de-from)
- [en WHERE](#en-where)
- [Después de WHERE](#después-de-where)

<br>

[Queries - Flujos](#queries---flujos)
- [Para 1:1](#para-11) - `Pending.`
- [Para 1:N](#para-1n) - `Pending.`
- [Para N:N](#para-nn) - `Pending.`
- [Para N:N Avanzado](#para-nn-avanzado)

<br>

[Extras](#extras)
- [Flujo de Conexión con Docker](#flujo-de-conexión-con-docker) - `Pending.`
- [Ejecución de Queries](#ejecución-de-queries) - `Pending.`
- [Parcial](#parcial)

<br><br>

---

<br>

## Bases

<br>

### Conceptos Claves

<br>

| Concepto | Definición |
|---|---|
| SQL | Lenguaje utilizado para definir, consultar y modificar datos en bases de datos relacionales. |
| Base de datos | Conjunto organizado de información almacenada. Puede ser virtual o no. Puede ser un Excel, cualquier cosa. Dentro de las virtuales están las Relacionales (organizan información en tablas relacionadas entre sí mediante claves `PK` y `FK`) y las No Relacionales. |
| Entidades | Objeto o concepto que se quiere representar en la base de datos. Si una relación `N:N` se desea representar en una tabla auxiliar con atributos propios, se vuelve una entidad. |
| Relaciones | `1:1`, `1:N` y `N:N` (requiere tabla auxiliar). |
| Tablas | Estructuras que almacenan datos organizados en filas y columnas. Representan entidades y/o relaciones entre ellas. |
| Atributo | Característica de una entidad. Aquello que se establecerá como columna. |
| Columnas (describen) | Definen qué información guarda cierta tabla. Ejemplo: `id`, `nombre`, `precio`. |
| Filas (representan) | Cada registro concreto de la tabla; representan entidades reales. Ejemplo: `(Mouse, 100)`, `(Teclado, 200)`. |
| Primary Key (`PK`) | Columna que identifica de forma única cada fila de una tabla. No se repite ni puede ser `NULL`. |
| Foreign Key (`FK`) | Columna que referencia la `PK` de otra tabla para relacionarlas. |
| Query | Consulta SQL utilizada para pedir, modificar o eliminar información. |
| Alias | Permiten escribir consultas más cortas y legibles: `usuarios u` se va a poder usar como `u.nombre`. |
| Motor de BdDs Relacional (DBMS) (ej: PostgreSQL) | Guarda, organiza y consulta datos usando SQL. Corre como un servidor. |
| Cliente (ej: DBeaver) | Programa que permite conectarse a diferentes motores y ejecutar queries (gráficamente o no, dependiendo del cliente). |

<br><br>

### Ventajas de uso

<br>

| Letra | Ventaja         | Idea clave                                               |
| ----- | --------------- | -------------------------------------------------------- |
| **P** | Persistencia    | Los datos quedan guardados permanentemente.              |
| **R** | Relaciones      | Permite conectar tablas y datos relacionados.            |
| **I** | Integridad      | Evita errores e inconsistencias con restricciones.       |
| **S** | Selects rápidos | Facilita consultas y búsquedas eficientes.               |
| **M** | Multiusuario    | Varias personas/apps pueden usar la BDD al mismo tiempo. |


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Convenciones

<br>

### Sobre Queries

<br>

- Definir aliases en `FROM` sin usar `AS`. Ejemplo: `FROM usuarios u`
- Usar `DISTINCT` cuando sea necesario evitar filas repetidas. No usarlo siempre por defecto, porque puede ocultar errores en la consulta.
- No usar `WHERE` como reemplazo de `JOIN`. Si se usa mal, puede generar un `CROSS JOIN` no deseado: todas las combinaciones posibles entre dos tablas, sin respetar relaciones.

<br><br>

### Sobre Configs

<br>

- Usar PostgreSQL como motor / Data Base Management System (DBMS). Para el TP, PostgreSQL debe levantarse como un contenedor a partir de una imagen Docker.
- Usar DBeaver como cliente gráfico para conectarse a PostgreSQL, ver tablas y ejecutar consultas.

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Diseño

<br>

### CRUD

<br>

| CRUD | Formas | Qué hace | Base de Datos | Tablas / Datos |
|---|---|---|---|---|
| **CREATE** | CREATE (estructura), <br>INSERT (datos) | CREATE: Crear estructura.<br><br>INSERT: Insertar valores a una tabla. | `CREATE DATABASE tienda;` | `CREATE TABLE usuarios ( ... );`<br><br>`INSERT INTO usuarios (nombre) VALUES ('Ana');` |
| **READ** | SELECT | Leer / consultar información | N/A | `SELECT ... FROM ...` |
| **UPDATE** | ALTER (estructuras), <br>UPDATE (datos) | ALTER: Modifica una estructura existente.<br><br>UPDATE: Modifica datos existentes. | `ALTER DATABASE mi_bdd ...` | `ALTER TABLE usuarios ...`<br><br>`UPDATE usuarios SET nombre = 'Juan' WHERE id = 1;` |
| **DELETE** | DROP (estructura), <br>TRUNCATE (limpiar tabla), <br>DELETE (datos) | DROP: Elimina completamente una estructura.<br><br>TRUNCATE: Vacía todos los datos de una tabla.<br><br>DELETE: Elimina datos específicos. | `DROP DATABASE mi_bdd;` | `DROP TABLE usuarios;`<br><br>`TRUNCATE TABLE usuarios;`<br><br>`DELETE FROM usuarios WHERE id = 1;` |

<br><br>

### Tipos de datos

<br>

| Tipo          | Uso común                  |
| ------------- | -------------------------- |
| `SERIAL`      | IDs autoincrementales.     |
| `INT`         | Números enteros.           |
| `SMALLINT`    | Enteros pequeños.          |
| `VARCHAR(50)` | Texto con longitud máxima. |
| `DATE`        | Fechas.                    |
| `TIMESTAMP`   | Fecha y hora.              |
| `BOOLEAN`     | `TRUE` o `FALSE`.          |


<br><br>

### Restricciones de datos

<br>

| Restricción   | Qué hace                  |
| ------------- | ------------------------- |
| `UNIQUE`      | Evita valores repetidos.  |
| `NOT NULL`    | Obliga a tener valor.     |
| `DEFAULT` + valor | Asigna valor por defecto. |

<br><br><br>

### Tablas para 1:1 

<br>

```txt
Para cada Persona, hay un único pasaporte.
```

<br>

```sql
CREATE TABLE personas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE pasaportes (
    id SERIAL PRIMARY KEY,
    persona_id INT UNIQUE REFERENCES personas(id),
    numero VARCHAR(50)
);
```
<br>
<img width="700" alt="imagen" src="https://github.com/user-attachments/assets/afa29f14-e090-49ef-b00e-3d20dc3b6366" />

<br><br><br>

### Tablas para 1:N 

<br>

```txt
Para cada Usuario, hay 1 o más Compras.
```

<br>

```sql
CREATE TABLE usuarios (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE compras (
    id SERIAL PRIMARY KEY,
    usuario_id INT REFERENCES usuarios(id),
    fecha DATE
);
```
<br>
<img width="600" alt="imagen" src="https://github.com/user-attachments/assets/50b1fd73-5ee7-4a03-8e8a-ff5415f3aef5" />

<br><br><br>

### Tablas para N:N 

<br>

```txt
Para cada Alumno, hay 1 o más Materias `1:N`.
Para cada Materia, hay 1 o más Alumnos `N:1`.

Entonces: Alumno <--> Materia es una relación `N:N`-> necesito tabla auxiliar.
```

<br>

```sql
CREATE TABLE alumnos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE materias (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE alumno_materia (
    alumno_id INT REFERENCES alumnos(id),
    materia_id INT REFERENCES materias(id),
    PRIMARY KEY (alumno_id, materia_id)
);
```
<br>
<img width="800" alt="imagen" src="https://github.com/user-attachments/assets/d10e6bc2-920f-4661-96f9-f4ef4bb0081d" />

<br><br><br>

### N:N Avanzado

<br>

```txt
Primera relación `N:N`:
- Para cada Jugador, hay 1 o más Partidos `1:N`.
- Para cada Partido, hay 1 o más Jugadores `N:1`.

Entonces: Jugador ↔ Partido es `N:N` → necesito una tabla auxiliar: `jugadores_partidos`.

Además, esta relación tiene atributos propios:
- es_local
- goles_anotados
- asistencias_hechas

Entonces: la tabla auxiliar no solo conecta entidades, también guarda información específica de la participación del jugador en el partido.
```

<br>

```txt
Segunda relación `N:N`:
- Para cada Jugador, hay 1 o más Inscripciones `1:N`.
- Para cada Partido, hay 1 o más Inscripciones `N:1`.

Entonces: Jugador ↔ Partido también tiene otra relación `N:N` distinta → necesito otra tabla auxiliar: `inscripciones`.

Además, esta relación tiene un atributo propio:
- fecha_inscripcion

Entonces: la inscripción también se modela como entidad/tabla auxiliar separada.
```

<br>

```sql
CREATE TABLE jugadores (
    id SERIAL PRIMARY KEY,
    nombre_completo VARCHAR(100) NOT NULL,
    posicion_preferida VARCHAR(50),
    fecha_nacimiento DATE,
    nacionalidad VARCHAR(50),
    dni INT UNIQUE,
    email VARCHAR(255) UNIQUE NOT NULL,
    contrasenia VARCHAR(255) NOT NULL
);

CREATE TABLE partidos (
    id SERIAL PRIMARY KEY,
    fecha_hora TIMESTAMP NOT NULL,
    lugar TEXT NOT NULL,
    goles_local SMALLINT,
    goles_visitante SMALLINT,
    inscripcion_desde TIMESTAMP NOT NULL,
    inscripcion_hasta TIMESTAMP NOT NULL
);

CREATE TABLE jugadores_partidos (
    id_jugador INT NOT NULL REFERENCES jugadores(id),
    id_partido INT NOT NULL REFERENCES partidos(id),
    es_local BOOLEAN NOT NULL,
    goles_anotados SMALLINT NOT NULL,
    asistencias_hechas SMALLINT NOT NULL,
    PRIMARY KEY (id_jugador, id_partido)
);

CREATE TABLE inscripciones (
    id_jugador INT NOT NULL REFERENCES jugadores(id),
    id_partido INT NOT NULL REFERENCES partidos(id),
    fecha_inscripcion TIMESTAMP NOT NULL,
    PRIMARY KEY (id_jugador, id_partido)
);
```
<br>
<img width="700" alt="imagen" src="https://github.com/user-attachments/assets/fc0df7d2-53de-4264-a943-09c67f936555" />


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Queries

<br>

### en SELECT
* Estas son las únicas estructuras que trabajan directamente con columnas además de `CREATE TABLE` y las funciones de agregación.

<br>

```sql
SELECT * FROM usuarios;
```
* Selecciona todas las columnas de una tabla.

<br>

```sql
SELECT 1 FROM usuarios;
```
* Se usa para subqueries con `EXISTS`.
* Devuelve el valor constante `1` por cada fila encontrada.
* Se usa cuando solo importa verificar si existen filas, no obtener sus datos.

<br>

```sql
CASE
    WHEN condicion THEN resultado
    WHEN otra_condicion THEN resultado
    ELSE resultado
END
```
* Permite hacer condiciones dentro de una consulta SQL, similar a un `if/else`.
* Sirve para crear columnas calculadas o mostrar distintos valores según una condición.


<br><br>

### Después de FROM
Los JOIN permiten combinar tablas **horizontalmente** entre columnas.

| Elemento              | Qué hace                                                                          | Resultado                                                         |
| --------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `INNER JOIN` o `JOIN` | Devuelve solo las filas que tienen coincidencia en ambas tablas.                  | Solo aparecen los registros con match entre ambas tablas.         |
| `LEFT JOIN`           | Devuelve todas las filas de la tabla izquierda y las coincidencias de la derecha. | Si no hay match en la derecha, sus columnas aparecen como `NULL`. |


<br><br>

### en WHERE
Se utilizan para filtrar resultados.

| Tipo | Elementos | Qué hacen | Ejemplos |
| --- | --- | --- | --- |
| Comparaciones | `=` `!=` `<>` `<` `>` `<=` `>=` | Comparan valores. | `edad >= 18` |
| Comparaciones especiales | `BETWEEN ... AND ...` `LIKE 'A%'` `IN` `IS NULL` | Simplifican filtros frecuentes. | `edad BETWEEN 18 AND 30`<br>`nombre LIKE 'A%'`<br>`archivo LIKE '%.txt'`<br>`pais IN ('Argentina', 'Chile')`<br>`telefono IS NULL` |
| Operadores lógicos | `AND` `OR` `NOT` | Combinan o niegan condiciones. | `edad > 18 AND pais = 'Argentina'` |
| Subqueries | `EXISTS` `SELECT 1` | Consultas dentro de otras consultas para filtrar, comparar o verificar existencia. | `SELECT u.nombre FROM usuarios u WHERE EXISTS ( SELECT 1 FROM pedidos p WHERE p.usuario_id = u.id )` |


<br><br>

### Después de WHERE

| Elemento   | Qué hace                                                     | Ejemplo              |
| ---------- | ------------------------------------------------------------ | -------------------- |
| `ORDER BY` | Ordena resultados. Por defecto es ascendente.                | `ORDER BY edad`      |
| `ORDER BY` + `DESC` | Cambia el orden a descendente.                      | `ORDER BY nota DESC` |
| `LIMIT`    | Limita la cantidad de filas devueltas.                       | `LIMIT 5`            |


<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Queries - Flujos

<br>

### Para 1:1 

<br>

`Pending.`

<br><br>

### Para 1:N

<br>

`Pending.`

<br><br>

### Para N:N

<br>

`Pending.`

<br><br>

### Para N:N Avanzado

<br>

```txt
Goles hechos por partido (fecha) por cada jugador (nombre completo).
```

<br>

```sql
SELECT partidos.fecha_hora, jugadores.nombre_completo, jp.goles_anotados
FROM jugadores_partidos jp
JOIN jugadores ON jp.id_jugador = jugadores.id
JOIN partidos ON jp.id_partido = partidos.id
WHERE jp.goles_anotados != 0
-- `<>` es lo mismo que `!=`
-- En ese where se sacan los jugadores que no anotaron goles
ORDER BY 
    partidos.fecha_hora, 
    jp.goles_anotados DESC, 
    jp.asistencias_hechas DESC, 
    jugadores.nombre_completo;
```

<br>

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Extras
No necesario memorizar para parcial pero útil para TP.

<br>

### Flujo de Conexión con Docker

<br>

`Pending`

<br><br>

### Ejecución de Queries
Terminal Interactiva vs Archivo `.sql`

<br>

`Pending`

<br><br>

### Parcial

No entran en el Parcial:
- Unión/ consultas concatenadas
- Funciones de agregación: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br><br><br>





