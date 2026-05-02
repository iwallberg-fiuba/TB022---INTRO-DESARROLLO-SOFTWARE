
> **Idea:** SQL no es solo pedir datos; es una forma estructurada de definir, consultar y relacionar informacion persistente.

## Keywords a saber

`base de datos`, `tabla`, `SELECT`, `WHERE`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`, `GROUP BY`, `ORDER BY`, `PRIMARY KEY`, `FOREIGN KEY`

> **Para estudiar:** separa mentalmente las operaciones que `leen`, las que `escriben` y las que `relacionan`.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `base de datos` | Conjunto organizado de datos y objetos relacionados. | Conviene pensarla como el "espacio de informacion" completo de una aplicacion, no solo como una tabla suelta. |
| `tabla` | Estructura de filas y columnas donde se almacenan datos. | Es la unidad visible mas comun del modelo relacional: una tabla suele representar una entidad o tema. |
| `SELECT` | Consulta para recuperar datos. | Es la operacion de lectura por excelencia. No cambia la informacion; la observa y la organiza. |
| `WHERE` | Clausula que filtra filas segun una condicion. | Define que parte de la tabla te interesa, evitando traer todo sin criterio. |
| `INSERT` | Instruccion para agregar nuevas filas. | Se usa cuando incorporas informacion nueva al sistema. |
| `UPDATE` | Instruccion para modificar filas existentes. | Es potente pero riesgosa: sin filtro correcto, podes cambiar mas datos de los que querias. |
| `DELETE` | Instruccion para borrar filas. | Conviene usarla con cuidado porque quita datos; en muchos sistemas reales eso puede ser irreversible. |
| `JOIN` | Operacion para combinar datos de varias tablas relacionadas. | Es una de las ideas mas importantes de SQL relacional: los datos ganan valor cuando se conectan, no cuando quedan aislados. |
| `GROUP BY` | Clausula para agrupar filas antes de aplicar agregaciones. | Sirve cuando no queres ver registros uno por uno, sino resumenes por categoria. |
| `ORDER BY` | Clausula para ordenar el resultado de una consulta. | No cambia el contenido de la consulta, pero si la forma en que lo lees o presentas. |
| `PRIMARY KEY` | Clave principal que identifica de forma unica cada fila. | Su funcion central es evitar ambiguedad: cada fila debe poder distinguirse sin duda. |
| `FOREIGN KEY` | Clave que referencia la clave principal de otra tabla. | Es el mecanismo que formaliza la relacion entre tablas y evita conexiones "inventadas". |

## Tabla comparativa rapida

| Instruccion | Para que sirve | Tipo de accion |
| --- | --- | --- |
| `SELECT` | leer datos | consulta |
| `INSERT` | agregar datos | escritura |
| `UPDATE` | cambiar datos | escritura |
| `DELETE` | borrar datos | escritura |

## Mapa mental rapido

La progresion del tema es esta:

```text
primero defino donde viven los datos
-> despues agrego o modifico registros
-> luego consulto con filtros y orden
-> y cuando hace falta, relaciono tablas entre si
```

Eso muestra que SQL no es solo "hacer selects", sino administrar informacion con estructura.

## Lo que mas se suele confundir

- una `base de datos` no es una sola `tabla`; la tabla es solo una pieza dentro de una estructura mas amplia.
- `WHERE` y `ORDER BY` no cumplen el mismo rol: uno filtra que filas entran y el otro ordena como se muestran.
- `PRIMARY KEY` y `FOREIGN KEY` tampoco son equivalentes: una identifica filas dentro de la tabla y la otra crea relaciones con otra tabla.

## Como leer este apunte

Este archivo conserva el recorrido del material largo, pero ordena mejor los conceptos para que se vea la diferencia entre:

- base de datos;
- tabla;
- consulta;
- manipulacion de estructura;
- manipulacion de datos.

## 1. Idea general

SQL significa `Structured Query Language`.

Se usa para trabajar con bases de datos relacionales.

Con SQL podes:

- crear bases y tablas;
- insertar datos;
- actualizarlos;
- borrarlos;
- consultarlos;
- relacionar varias tablas.

## 2. Conceptos base

### Base de datos

Es el conjunto organizado que contiene tablas y otros objetos.

### Tabla

Es una estructura de filas y columnas dentro de una base de datos.

### Fila o registro

Representa una instancia concreta de datos.

### Columna

Representa un atributo o tipo de dato dentro de la tabla.

### Consulta

Es una instruccion SQL que recupera o manipula datos.

## 3. Crear base de datos y tablas

### Crear base de datos

```sql
CREATE DATABASE mi_base_de_datos;
```

### Crear tabla

```sql
CREATE TABLE empleados (
  id INT PRIMARY KEY,
  nombre VARCHAR(50),
  departamento VARCHAR(50),
  salario DECIMAL(10, 2)
);
```

Lectura:

- `id`: entero y clave primaria;
- `nombre`: texto variable;
- `departamento`: texto variable;
- `salario`: numero decimal.

## 4. Insertar datos

### Un registro

```sql
INSERT INTO empleados (id, nombre, departamento, salario)
VALUES (1, 'Juan Perez', 'Recursos Humanos', 3000.00);
```

### Varios registros

```sql
INSERT INTO empleados (id, nombre, departamento, salario)
VALUES
  (2, 'Ana Gomez', 'Finanzas', 3500.00),
  (3, 'Luis Martinez', 'IT', 4000.00),
  (4, 'Maria Lopez', 'Marketing', 3200.00);
```

## 5. Modificar y borrar datos

### Actualizar

```sql
UPDATE empleados
SET salario = 3200.00
WHERE id = 2;
```

### Borrar un registro

```sql
DELETE FROM empleados
WHERE id = 1;
```

En `UPDATE` y `DELETE`, la clausula `WHERE` es critica.

Sin `WHERE`, podrias afectar toda la tabla.

## 6. Cambiar estructura

### Agregar columna

```sql
ALTER TABLE empleados
ADD fecha_contratacion DATE;
```

### Eliminar columna

```sql
ALTER TABLE empleados
DROP COLUMN fecha_contratacion;
```

## 7. Eliminar tabla o base

### Borrar tabla

```sql
DROP TABLE empleados;
```

Si hay relaciones con otras tablas, puede aparecer el uso de `CASCADE`.

```sql
DROP TABLE empleados CASCADE;
```

### Borrar todos los datos pero no la tabla

```sql
TRUNCATE TABLE empleados;
```

### Borrar base de datos

```sql
DROP DATABASE mi_base_de_datos;
```

## 8. Consultas basicas con SELECT

### Todas las columnas

```sql
SELECT * FROM empleados;
```

### Algunas columnas

```sql
SELECT nombre, salario
FROM empleados;
```

`SELECT *` sirve para explorar rapido, pero en consultas reales suele ser mejor pedir solo las columnas necesarias.

## 9. Filtrado con WHERE

### Igualdad

```sql
SELECT *
FROM empleados
WHERE departamento = 'IT';
```

### Comparacion numerica

```sql
SELECT *
FROM empleados
WHERE salario > 3000.00;
```

### Patrones con LIKE

```sql
SELECT *
FROM empleados
WHERE nombre LIKE 'A%';
```

`%` funciona como comodin de varios caracteres.

## 10. Ordenar resultados

### Descendente

```sql
SELECT *
FROM empleados
ORDER BY salario DESC;
```

### Ascendente

```sql
SELECT *
FROM empleados
ORDER BY nombre ASC;
```

### Filtrar y ordenar juntos

```sql
SELECT *
FROM empleados
WHERE departamento = 'Recursos Humanos'
ORDER BY fecha_contratacion DESC;
```

## 11. Agrupar resultados

### Contar por grupo

```sql
SELECT departamento, COUNT(*) AS total_empleados
FROM empleados
GROUP BY departamento;
```

### Promediar por grupo

```sql
SELECT departamento, AVG(salario) AS salario_promedio
FROM empleados
GROUP BY departamento;
```

`GROUP BY` sirve cuando queres resumir datos por categoria.

## 12. Funciones de agregacion

Las mas comunes:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

Ejemplo:

```sql
SELECT COUNT(*) AS total_empleados
FROM empleados;
```

## 13. Relaciones entre tablas

Las bases relacionales toman fuerza cuando varias tablas se vinculan entre si.

Ejemplo mental:

- una tabla `empleados`;
- una tabla `departamentos`.

Cada empleado pertenece a un departamento.

## 14. Joins

Un `JOIN` combina datos de varias tablas segun una relacion.

### INNER JOIN

```sql
SELECT e.nombre, d.nombre AS departamento
FROM empleados e
INNER JOIN departamentos d
  ON e.departamento = d.id;
```

La idea general es:

- tomar una tabla;
- unirla con otra;
- decir con que condicion se relacionan.

## 15. Subconsultas

Una subconsulta es una consulta dentro de otra consulta.

Ejemplo:

```sql
SELECT nombre, salario
FROM empleados
WHERE salario > (
  SELECT AVG(salario)
  FROM empleados
);
```

Lectura:

- primero se calcula el salario promedio;
- despues se filtran solo los empleados que lo superan.

## 16. Primary Key y Foreign Key

### Primary Key

Identifica de forma unica cada fila.

Ejemplo:

```sql
CREATE TABLE empleados (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(50)
);
```

### Foreign Key

Conecta una columna con la clave primaria de otra tabla.

Ejemplo:

```sql
CREATE TABLE empleados (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(50),
  depto_id INT,
  FOREIGN KEY (depto_id) REFERENCES departamentos(id)
);
```

Eso obliga a que `depto_id` apunte a un departamento existente.

## 17. Diferencias que suelen confundir

### DELETE vs TRUNCATE vs DROP

- `DELETE`: borra filas;
- `TRUNCATE`: vacia la tabla pero conserva su estructura;
- `DROP`: elimina la tabla completa.

### Base de datos vs tabla

- base de datos: contiene tablas;
- tabla: contiene filas y columnas.

### WHERE vs ORDER BY vs GROUP BY

- `WHERE`: filtra;
- `ORDER BY`: ordena;
- `GROUP BY`: agrupa para resumir.

## 18. Resumen final

Las ideas mas importantes del tema son:

- SQL manipula bases de datos relacionales;
- una tabla organiza datos en filas y columnas;
- `CREATE`, `INSERT`, `UPDATE`, `DELETE` y `SELECT` son la base;
- `WHERE` filtra;
- `ORDER BY` ordena;
- `GROUP BY` resume por grupos;
- `JOIN` conecta tablas;
- `PRIMARY KEY` identifica;
- `FOREIGN KEY` relaciona.


