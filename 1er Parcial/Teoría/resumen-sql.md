# Apunte largo - SQL

## Fuente trabajada

- `SQL  Intro al Desarrollo de Software.md`

## Idea global del tema

SQL es el lenguaje usado para trabajar con bases de datos relacionales. Sirve para definir tablas, insertar datos, consultarlos, actualizarlos, borrarlos y relacionar informacion entre tablas.

## 1. Conceptos base

### Base de datos

Conjunto organizado de datos.

### Tabla

Estructura con filas y columnas dentro de la base de datos.

### Consulta

Instruccion SQL para recuperar o manipular datos.

### Distincion clave

Una base de datos puede contener muchas tablas. Una tabla es una parte de la base de datos, no toda la base.

## 2. Crear y borrar base de datos

### Crear

```sql
CREATE DATABASE mi_base_de_datos;
```

### Eliminar

```sql
DROP DATABASE mi_base_de_datos;
```

## 3. Crear tablas

```sql
CREATE TABLE empleados (
  id INT PRIMARY KEY,
  nombre VARCHAR(50),
  departamento VARCHAR(50),
  salario DECIMAL(10, 2)
);
```

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
  (3, 'Luis Martinez', 'IT', 4000.00);
```

## 5. Actualizar y borrar datos

### Actualizar

```sql
UPDATE empleados
SET salario = 3200.00
WHERE id = 2;
```

### Borrar

```sql
DELETE FROM empleados
WHERE id = 1;
```

### Idea importante

`WHERE` evita afectar registros incorrectos.

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

## 7. Eliminar tabla o vaciarla

### Eliminar tabla

```sql
DROP TABLE empleados;
```

### Con cascada

```sql
DROP TABLE empleados CASCADE;
```

### Vaciar sin borrar estructura

```sql
TRUNCATE TABLE empleados;
```

## 8. `SELECT`

### Todo

```sql
SELECT * FROM empleados;
```

### Algunas columnas

```sql
SELECT nombre, salario FROM empleados;
```

## 9. Filtrado

```sql
SELECT * FROM empleados
WHERE departamento = 'IT';
```

### Operadores comunes

- `=`
- `>`
- `<`
- `>=`
- `<=`
- `<>`

### `LIKE`

```sql
SELECT * FROM empleados
WHERE nombre LIKE 'A%';
```

## 10. Ordenamiento

```sql
SELECT * FROM empleados
ORDER BY salario DESC;
```

## 11. Agrupamiento y agregacion

### `GROUP BY`

```sql
SELECT departamento, COUNT(*) AS total_empleados
FROM empleados
GROUP BY departamento;
```

### Funciones utiles

- `COUNT`
- `SUM`
- `AVG`
- `MIN`
- `MAX`

## 12. Consultas entre tablas

### `INNER JOIN`

```sql
SELECT empleados.nombre, departamentos.nombre AS departamento
FROM empleados
INNER JOIN departamentos
ON empleados.departamento = departamentos.id;
```

### Idea importante

`JOIN` es mas explicito y legible que mezclar tablas con `WHERE`.

## 13. Subconsultas

```sql
SELECT nombre, salario
FROM empleados
WHERE salario > (SELECT AVG(salario) FROM empleados);
```

## 14. Claves

### `PRIMARY KEY`

- identifica un registro de forma unica

### `FOREIGN KEY`

- referencia una clave de otra tabla
- permite modelar relaciones

## 15. Posibles preguntas de parcial

1. Que es SQL?
2. Diferencia entre base de datos y tabla.
3. Para que sirven `CREATE DATABASE` y `CREATE TABLE`?
4. Diferencia entre `INSERT`, `UPDATE` y `DELETE`.
5. Diferencia entre `DROP TABLE` y `TRUNCATE TABLE`.
6. Para que sirven `SELECT`, `WHERE`, `ORDER BY` y `GROUP BY`?
7. Que es un `JOIN`?
8. Que es una subconsulta?
9. Que son `PRIMARY KEY` y `FOREIGN KEY`?

## 16. Memorizacion rapida

- SQL trabaja con bases relacionales.
- Una base tiene tablas.
- `SELECT` consulta.
- `WHERE` filtra.
- `ORDER BY` ordena.
- `GROUP BY` agrupa.
- `JOIN` une tablas.
- `PRIMARY KEY` identifica.
- `FOREIGN KEY` relaciona.
