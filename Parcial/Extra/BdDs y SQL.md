
<br><br>

### Table of Contents

<br>

Bases
- [Conceptos Claves](#conceptos-claves) Tema filas, columnas, entidades, relaciones, atributos y en q tablas pone, cliente, motor, uso de docker
- [Ventajas de uso](#ventajas-de-uso)
- [CRUD](#crud) CRUD BdDs y tablas
- [Tipos de datos](#tipos-de-datos)
- [Restricciones de datos](#restricciones-de-datos)


<br>

Convenciones
- [Sobre Queries](#sobre-queries)
- [Sobre Configs](#sobre-configs) cliente, motor, docker

<br>

Queries
- [en SELECT](#en-select)
- [Después de FROM](#después-de-from)
- [en WHERE](#en-where)
    - [Subqueries](#subqueries) 
- [Después de WHERE](#después-de-where)

<br>

Queries - Flujos
- para cada tipo de relacion

<br>

Extras - `Pending`
- [Flujo de Conexión con Docker](#placeholder)
- [Ejecucución de Queries](#placeholder)

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

<br><br>

### Ventajas de uso

<br>

`Pending`

<br><br>

### CRUD

<br>

`Pending`

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

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Convenciones


### Sobre Queries

`Pending`


### Sobre Configs

`Pending`



<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Queries

<br>

### en SELECT
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

<br><br>

### Dspués de FROM
Los JOIN permiten combinar tablas **horizontalmente** entre columnas.

| Elemento              | Qué hace                                                                          | Resultado                                |
| --------------------- | --------------------------------------------------------------------------------- | ---------------------------------------- |
| `INNER JOIN` o `JOIN` | Devuelve solo las filas que tienen coincidencia en ambas tablas.                  | Solo aparecen matches.                   |
| `LEFT JOIN`           | Devuelve todas las filas de la tabla izquierda y las coincidencias de la derecha. | Si no hay coincidencia, aparecen `NULL`. |

Entonces: 
- `JOIN` cuando se quieren obtener los matches
- `LEFT JOIN` cuando queres incluir valores nulos/ sin matches.

<br><br>

 ### en WHERE

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

#### Subqueries

| Elemento              | Qué hace                                             | Ejemplo                          |
| --------------------- | ---------------------------------------------------- | -------------------------------- |
| `EXISTS` + `SELECT 1` | Verifica si una subquery devuelve al menos una fila. | `EXISTS ( SELECT 1 FROM pedidos p WHERE p.usuario_id = u.id )` |


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

`Pending`


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

<br>

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

<br><br>





