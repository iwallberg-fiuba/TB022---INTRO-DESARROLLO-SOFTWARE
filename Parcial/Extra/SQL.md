

INICIO

Acuerdos:
- Definir aliases en `FROM` (omite el paso de usar `AS`).
- Poner `DISTINCT`
- Nunca usar `WHERE` como reemplazo de `JOIN` porque puede generar un `CROSS JOIN` accidental (se generan todas las combinaciones posibles entre dos tablas sin considerar relaciones).


No entran:
- Unión/ consultas concatenadas
- Funciones de agregación: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

Lo más difícil (opinión):
- Queries con múltiples JOINs.
- Diseñar las bases de datos para relaciones `N:N` con atributos propios.
- Hacer queries dirigidas a esos atributos propios de `N:N`.

Table of Contents:


---

DEFINICIONES BASES

| Concepto | Definición |
|---|---|
| SQL | Lenguaje utilizado para definir, consultar y modificar datos en bases de datos relacionales. |
| Base de datos | Conjunto organizado de información almacenada. |
| Base de datos relacional | Base de datos que organiza información en tablas relacionadas entre sí mediante claves (`PK` y `FK`). |
| Tablas | Estructuras que almacenan datos organizados en filas y columnas. Representan entidades como usuarios, productos o pedidos. |
| Columnas (describen) | Definen qué información guarda cierta tabla. Ejemplo: `id`, `nombre`, `precio`. |
| Filas (representan) | Cada registro concreto de la tabla; representan entidades reales. Ejemplo: `(Mouse, 100)`, `(Teclado, 200)`. |
| Primary Key (`PK`) | Columna que identifica de forma única cada fila de una tabla. No se repite ni puede ser `NULL`. |
| Foreign Key (`FK`) | Columna que referencia la `PK` de otra tabla para relacionarlas. |
| Query | Consulta SQL utilizada para pedir, modificar o eliminar información. |
| Ventajas de usar SQL | Permite consultar grandes cantidades de datos, relacionar tablas, filtrar información y mantener datos organizados y consistentes. |
| Alias | Permiten escribir consultas más cortas y legibles: `usuarios u`, `cursos c`, `usuarios_cursos uc`. Después se usan como `u.nombre`, `c.nombre`, etc. |
| CRUD (Create, Read, Update, Delete) | `CREATE TABLE ...` crea tablas, `INSERT INTO ... VALUES ...` agrega datos, `SELECT ... FROM ...` consulta datos, `UPDATE ... SET ... WHERE ...` modifica datos, `DELETE FROM ... WHERE ...` elimina filas específicas, `TRUNCATE TABLE ...` elimina todas las filas manteniendo la estructura, `DROP TABLE ...` elimina completamente la tabla (estructura + datos). |
| Motor de base de datos relacional (DBMS) (ej: PostgreSQL) | Guarda, organiza y consulta datos usando SQL. Corre como un servidor. |
| Cliente para administar BdDs (ej: DBeaver) | Permite conectarse a PostgreSQL, SQLite, MySQL, etc., y ejecutar queries, dependiendo del cliente, gráficamente o no. |

---

QUERIES

1. Usadas en `SELECT`:

- Estas son las únicas que trabajan con COLUMNAS además de `CREATE TABLE` y las funciones de agregación.

| Elemento                         | Qué hace                                                                      | Ejemplo / pista                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `SELECT *`                       | Selecciona todas las columnas de una tabla.                                   | `SELECT * FROM usuarios`                                                             |
| `SELECT 1` (SUBQUERIES)          | Devuelve el valor constante 1 por cada fila encontrada. Se usa cuando solo importa saber si existen filas, no sus datos. | `SELECT 1 FROM usuarios`                  |
| `CASE ... WHEN ... THEN ... END` | Permite hacer condiciones dentro de una consulta SQL, similar a un `if/else`. | Útil para crear columnas calculadas o mostrar distintos valores según una condición. |

```sql
CASE
    WHEN condicion THEN resultado
    WHEN otra_condicion THEN resultado
    ELSE resultado
END
```

2. Usadas después de `FROM`

Los JOIN permiten combinar tablas **horizontalmente** entre columnas.

| Elemento              | Qué hace                                                                          | Resultado                                |
| --------------------- | --------------------------------------------------------------------------------- | ---------------------------------------- |
| `INNER JOIN` o `JOIN` | Devuelve solo las filas que tienen coincidencia en ambas tablas.                  | Solo aparecen matches.                   |
| `LEFT JOIN`           | Devuelve todas las filas de la tabla izquierda y las coincidencias de la derecha. | Si no hay coincidencia, aparecen `NULL`. |

Entonces: 
- `JOIN` cuando se quieren obtener los matches
- `LEFT JOIN` cuando queres incluir valores nulos/ sin matches.



3. Usadas en `WHERE`

Se utilizan para filtrar resultados.
* Comparaciones: Operadores como `<`, `>`, `<=`, `>=`, `=`, `!=` o `<>` comparan valores.
* Comparaciones especiales: Expresiones como `BETWEEN`, `LIKE`, `IN` o `IS NULL` simplifican filtros frecuentes.
* Operadores lógicos: Operadores como `AND`, `OR` y `NOT` permiten combinar o negar condiciones.
* Subqueries: Consultas dentro de otras consultas. Pueden usarse para filtrar, comparar valores o verificar existencia de filas (`EXISTS`).


Comparaciones
| Elemento          | Qué hace                                 | Ejemplo              |
| ----------------- | ---------------------------------------- | -------------------- |
| `=`               | Verifica igualdad.                       | `pais = 'Argentina'` |
| `!=` o `<>`       | Verifica desigualdad.                    | `edad != 18`         |
| `>` `<` `>=` `<=` | Comparan valores numéricos, fechas, etc. | `edad >= 18`         |

Comparaciones especiales
| Elemento  | Qué hace                                                | Ejemplo                          |
| --------- | ------------------------------------------------------- | -------------------------------- |
| `BETWEEN` | Verifica si un valor está dentro de un rango inclusive. | `edad BETWEEN 18 AND 30`         |
| `LIKE`    | Busca patrones en texto.                                | `nombre LIKE 'A%'`               |
| `IN`      | Verifica si un valor pertenece a una lista.             | `pais IN ('Argentina', 'Chile')` |
| `IS NULL` | Verifica si un valor es `NULL`.                         | `telefono IS NULL`               |

Operadores lógicos
| Elemento | Qué hace                               | Ejemplo                                |
| -------- | -------------------------------------- | -------------------------------------- |
| `AND`    | Todas las condiciones deben cumplirse. | `edad > 18 AND pais = 'Argentina'`     |
| `OR`     | Al menos una condición debe cumplirse. | `pais = 'Argentina' OR pais = 'Chile'` |
| `NOT`    | Niega una condición.                   | `NOT edad > 18`                        |

Subqueries
| Elemento              | Qué hace                                             | Ejemplo                          |
| --------------------- | ---------------------------------------------------- | -------------------------------- |
| `EXISTS` + `SELECT 1` | Verifica si una subquery devuelve al menos una fila. | `EXISTS ( SELECT 1 FROM pedidos p WHERE p.usuario_id = u.id )` |





4. Usadas después de `SELECT`, `FROM` y `WHERE`

| Elemento   | Qué hace                                                     | Ejemplo              |
| ---------- | ------------------------------------------------------------ | -------------------- |
| `ORDER BY` | Ordena resultados. Por defecto es ascendente.                | `ORDER BY edad`      |
| `ORDER BY` + `DESC` | Cambia el orden a descendente.                      | `ORDER BY nota DESC` |
| `LIMIT`    | Limita la cantidad de filas devueltas.                       | `LIMIT 5`            |





---

ENTENDER

1. JOIN y su relación con PKs y FKs

Un JOIN permite combinar información de varias tablas relacionadas. 
Generalmente se une una PK (Primary Key) con una FK (Foreign Key) (La FK apunta a la PK de otra tabla).

Idea mental:
usuarios.id = pedidos.usuario_id
 PK                    FK

Cómo pensar los joins:
1. Elegir tabla principal.
2. Ver qué tablas están relacionadas.
3. Traducir cada relación a:
    tabla1.pk = tabla2.fk

Ejemplo:
```sql
SELECT u.nombre, p.total
FROM usuarios u
JOIN pedidos p
ON u.id = p.usuario_id;
```


2. Múltiples JOINs

Se usan cuando necesitás información de más de dos tablas.
Cada JOIN agrega otra tabla relacionada.

Idea mental:

usuarios
   ↓
pedidos
   ↓
productos

Cada flecha representa una relación.

Ejemplo:
```sql
SELECT u.nombre, pr.nombre
FROM usuarios u
JOIN pedidos p
ON u.id = p.usuario_id
JOIN productos pr
ON p.producto_id = pr.id;
```

Cómo pensarlo:
1. “Estoy en usuarios”.
2. “Desde usuarios llego a pedidos”.
3. “Desde pedidos llego a productos”.




3. Subqueries

Una subquery es una consulta dentro de otra consulta.
La query interna se ejecuta primero y su resultado es usado por la externa.

Se usan para filtrar, comparar valores, verificar existencia, reutilizar resultados.

Ejemplo subquery:
```sql
`SELECT nombre
FROM usuarios u
WHERE EXISTS (
    SELECT 1
    FROM pedidos p
    WHERE p.usuario_id = u.id
);
```


---


# Diseñar Bases de Datos

## Cómo pensar el diseño de una base de datos

1. Pensar qué entidades existen.
   - Ejemplo: usuarios, pedidos, productos, cursos.

2. Pensar qué información necesita guardar cada entidad.
   - Ejemplo:
     - usuarios → nombre, mail, edad.
     - productos → nombre, precio, stock.

3. Pensar cuáles son las relaciones entre las entidades.
   - Ejemplo:
     - un usuario puede tener muchos pedidos.
     - un pedido puede tener muchos productos.

4. Pensar cómo se representa cada relación.

| Relación | Qué significa | Cómo suele representarse |
|---|---|---|
| `1:1` | Una fila se relaciona con una sola fila. | FK única (`UNIQUE`). |
| `1:N` | Una fila se relaciona con muchas filas. | FK en la tabla “muchos”. |
| `N:N` | Muchas filas se relacionan con muchas filas. | Tabla intermedia con dos FKs. |


5. Pensar si la relación necesita atributos propios.
   - Ejemplo:
     - `usuarios_cursos`
       - fecha_inscripcion
       - nota
       - estado

6. Elegir tipos de datos adecuados.

| Tipo          | Uso común                  |
| ------------- | -------------------------- |
| `SERIAL`      | IDs autoincrementales.     |
| `INT`         | Números enteros.           |
| `SMALLINT`    | Enteros pequeños.          |
| `TEXT`        | Texto largo.               |
| `VARCHAR(50)` | Texto con longitud máxima. |
| `DATE`        | Fechas.                    |
| `TIMESTAMP`   | Fecha y hora.              |
| `BOOLEAN`     | `TRUE` o `FALSE`.          |



7. Agregar restricciones para mantener consistencia.

| Restricción   | Qué hace                  |
| ------------- | ------------------------- |
| `UNIQUE`      | Evita valores repetidos.  |
| `NOT NULL`    | Obliga a tener valor.     |
| `DEFAULT`     | Asigna valor por defecto. |


EJEMPLOS DE CADA CASO:


<br>

### Relación `1:1` 
<br>
Para cada Persona, hay un único pasaporte.
<br><br>

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
<img width="1599" height="436" alt="imagen" src="https://github.com/user-attachments/assets/afa29f14-e090-49ef-b00e-3d20dc3b6366" />

<br><br>

<br>

---

<br>

### Relación `1:N`
<br>
Para cada Usuario, hay 1 o más Compras.
<br><br>

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
<img width="1119" height="444" alt="imagen" src="https://github.com/user-attachments/assets/50b1fd73-5ee7-4a03-8e8a-ff5415f3aef5" />

<br><br>
<br>

---

<br>

### Relación `N:N`

<br>

- Para cada Alumno, hay 1 o más Materias `1:N`.
- Para cada Materia, hay 1 o más Alumnos `N:1`.

Entonces: <br>
Alumno ↔ Materia es una relación `N:N` → necesito una tabla auxiliar.

<br><br>

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
<img width="2006" height="384" alt="imagen" src="https://github.com/user-attachments/assets/d10e6bc2-920f-4661-96f9-f4ef4bb0081d" />

<br><br>
<br>

---

<br>

### Ej 1 - Múltiples `N:N`

<br>

Primera relación `N:N`:
- Para cada Alumno, hay 1 o más Materias `1:N`.
- Para cada Materia, hay 1 o más Alumnos `N:1`.

Entonces:  
Alumno ↔ Materia es `N:N` → necesito una tabla auxiliar: `alumno_materia`.

Segunda relación `N:N`:
- Para cada Profesor, hay 1 o más Materias `1:N`.
- Para cada Materia, hay 1 o más Profesores `N:1`.

Entonces:  <br>
Profesor ↔ Materia es `N:N` → necesito otra tabla auxiliar: `profesor_materia`.

<br><br>

```sql
CREATE TABLE alumnos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE profesores (
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

CREATE TABLE profesor_materia (
    profesor_id INT REFERENCES profesores(id),
    materia_id INT REFERENCES materias(id),
    PRIMARY KEY (profesor_id, materia_id)
);
```
<br>
<img width="1559" height="1031" alt="imagen" src="https://github.com/user-attachments/assets/f4e2ca9c-7fe0-4488-88af-02e349b2dfa3" />

<br><br>
<br>

---

<br>

### Ej 2 - Múltiples `N:N`

<br>

Primera relación `N:N`:
- Para cada Jugador, hay 1 o más Partidos `1:N`.
- Para cada Partido, hay 1 o más Jugadores `N:1`.

Entonces:  
Jugador ↔ Partido es `N:N` → necesito una tabla auxiliar: `jugadores_partidos`.

Además, esta relación tiene atributos propios:
- es_local
- goles_anotados
- asistencias_hechas

Entonces: <br>
la tabla auxiliar no solo conecta entidades, también guarda información específica de la participación del jugador en el partido.

Segunda relación `N:N`:
- Para cada Jugador, hay 1 o más Inscripciones `1:N`.
- Para cada Partido, hay 1 o más Inscripciones `N:1`.

Entonces:  <br>
Jugador ↔ Partido también tiene otra relación `N:N` distinta → necesito otra tabla auxiliar: `inscripciones`.

Además, esta relación tiene un atributo propio:
- fecha_inscripcion

Entonces: <br>
la inscripción también se modela como entidad/tabla auxiliar separada.

<br><br>

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
<img width="1409" height="1021" alt="imagen" src="https://github.com/user-attachments/assets/fc0df7d2-53de-4264-a943-09c67f936555" />

<br><br><br>









