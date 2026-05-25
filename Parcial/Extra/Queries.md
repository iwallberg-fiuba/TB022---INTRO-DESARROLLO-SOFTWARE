

INICIO

Acuerdos
- Definir aliases en SELECT, no es necesario poner `AS` en todos los casos.
- Poner `DISTINCT`
- Nunca usar `WHERE` como reemplazo de `JOIN` porque puede generar un `CROSS JOIN` accidental.

No entran
- Unión/ consultas concatenadas
- Funciones de agregación (`SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`)

Tipos de datos:
- 


DEFINICIONES

1. Usadas en `SELECT`:


| Elemento                         | Qué hace                                                                      | Ejemplo / pista                                                                      |
| -------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `SELECT *`                       | Selecciona todas las columnas de una tabla.                                   | `SELECT * FROM usuarios`                                                             |
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
| `RIGHT JOIN` (No se usa) | Devuelve todas las filas de la tabla derecha y las coincidencias de la izquierda. | Si no hay coincidencia, aparecen `NULL`. |
| `FULL JOIN` (No se usa) | Devuelve coincidencias y también las filas sin match de ambas tablas.             | Los faltantes aparecen como `NULL`.      |
| `CROSS JOIN` (No se usa) | Combina cada fila de una tabla con todas las filas de la otra.                    | Genera todas las combinaciones posibles. |



3. Usadas en `WHERE`

Se utilizan para filtrar resultados.

| Elemento  | Qué hace                                                | Ejemplo                                |
| --------- | ------------------------------------------------------- | -------------------------------------- |
| `BETWEEN` | Verifica si un valor está dentro de un rango inclusive. | `edad BETWEEN 18 AND 30`               |
| `LIKE`    | Busca patrones en texto.                                | `nombre LIKE 'A%'`                     |
| `IS NULL` | Verifica si un valor es `NULL`.                         | `telefono IS NULL`                     |
| `IN`      | Verifica si un valor pertenece a una lista.             | `pais IN ('Argentina', 'Chile')`       |
| `AND`     | Todas las condiciones deben cumplirse.                  | `edad > 18 AND pais = 'Argentina'`     |
| `OR`      | Al menos una condición debe cumplirse.                  | `pais = 'Argentina' OR pais = 'Chile'` |
| `NOT`     | Niega una condición.                                    | `NOT edad > 18`                        |
| `EXISTS` (SUBQUERIES)  | verifica si una subquery devuelve al menos una fila.    | `EXISTS ( subquery )`     |




4. Usadas después de `SELECT`, `FROM` y `WHERE`

| Elemento   | Qué hace                                                     | Ejemplo              |
| ---------- | ------------------------------------------------------------ | -------------------- |
| `ORDER BY` | Ordena resultados. Por defecto es ascendente.                | `ORDER BY edad`      |
| `ORDER BY` + `DESC` | Cambia el orden a descendente.                      | `ORDER BY nota DESC` |
| `LIMIT`    | Limita la cantidad de filas devueltas.                       | `LIMIT 5`            |
| `LIMIT` + `OFFSET` | Salta X cantidad de filas antes de devolver Y cantidad de resultados. | `LIMIT 5 OFFSET 10`  |


Cómo unir tablas? Cuándo usar múltiples joins? cuándo usar left join o join? cuando usar subqueries?



Múltiples `JOIN`s







