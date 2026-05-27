
<br><br>

### Table of Contents

<br>

Bases
- [Conceptos Claves](#conceptos-claves) 
- [Ventajas de uso](#ventajas-de-uso)
- [CRUD](#crud)
- [Tipos de datos](#tipos-de-datos)
- [Restricciones de datos](#restricciones-de-datos)


<br>

Convenciones
- [Sobre Queries](#sobre-queries)
- [Sobre Configs](#sobre-configs)

<br>

Queries - `Pending`
- [en SELECT](#en-select)
- [Después de FROM](#después-de-from)
- [en WHERE](#en-where)
    - [Subqueries](#subqueries) 
- [Después de WHERE](#después-de-where)

<br>

Queries - Flujos `Pending`
- para cada tipo de relacion

<br>

Extras - `Pending`
- [Flujo de Conexión con Docker](#flujo-de-conexión-con-docker)
- [Ejecución de Queries](#ejecución-de-queries)

<br>

No entran en el Parcial
- Unión/ consultas concatenadas
- Funciones de agregación: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

<br><br>

---

<br>

## Bases

<br>

### Conceptos Claves

<br>

`Pending`
Tema filas, columnas, entidades, relaciones, atributos y en q tablas pone, cliente, motor, uso de docker


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

<br><br>

[Volver a Table of Contents](#table-of-contents)

<br>

---

<br>

## Convenciones

<br>

### Sobre Queries

<br>

- Definir aliases en `FROM` sin usar `AS`.
  - Ejemplo: `FROM usuarios u`
- Usar `DISTINCT` cuando sea necesario evitar filas repetidas.
  - No usarlo siempre por defecto, porque puede ocultar errores en la consulta.
- No usar `WHERE` como reemplazo de `JOIN`.
  - Si se usa mal, puede generar un `CROSS JOIN` no deseado: todas las combinaciones posibles entre dos tablas, sin respetar relaciones.

<br><br>

### Sobre Configs

<br>

- Usar PostgreSQL como motor / Data Base Management System (DBMS).
  - Para el TP, PostgreSQL debe levantarse como un contenedor a partir de una imagen Docker.
- Usar DBeaver como cliente gráfico para conectarse a PostgreSQL, ver tablas y ejecutar consultas.

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

### Después de FROM
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

<br>

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





