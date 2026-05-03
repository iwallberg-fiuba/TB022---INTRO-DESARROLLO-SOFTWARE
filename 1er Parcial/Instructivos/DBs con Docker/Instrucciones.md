Gracias a Docker, no es necesario instalar Postgree ni múltiples versiones de la app.  
  
**Cómo hacer una Base de Datos con Docker?**  
  
1. Abrir app `VS Code`
2. Crear el archivo `docker-compose.yml` con la siguiente información:

```yml
services:
  db:
    image: postgres:17
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: nombre_db
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./schema.sql:/docker-entrypoint-initdb.d/schema.sql
      - ./data.sql:/docker-entrypoint-initdb.d/data.sql
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

3. Dentro de la carpeta en donde está `docker-compose.yml`, crear los siguientes archivos:
  - `schema.sql` con el código ya escrito para crear las tablas
  - `data.sql` con el código ya escrito para insertar los datos iniciales de las tablas
  - Carpeta `updates_unicas` vacía como placeholder para cuando se deseen insertar o borrar datos (INSERT, DELETE)
  - Carpeta `updates_reejecutables` vacía como placeholder para cuando se deseen actualizar datos (UPDATE)
  - `queries.sql` vacío como placeholder para cuando se deseen hacer queries (SELECT)


4. Abrir `Docker`
5. Dentro de la carpeta donde está `docker-compose.yml`: `click derecho` > `Abrir en Terminal` y correr los siguientes comandos:
   1. `docker compose up -d`  
      `-d` de `detach` para que Docker no muestre logs en la Terminal, que el proceso pueda correr en segundo plano y que la Terminal no esté bloqueada.
   2. `docker ps`  
      Para ver los contenedores que están corriendo.
   3. `docker exec -it nombre_contenedor psql -U postgres -d nombre_db`
      Para ver la BD (sin modificar nada).
     
6. SI SE DESEA CAMBIAR ALGO: INYECCIONES. CUIDADO.
  Todas las inyecciones SQL están pensadas para ejecutarse una sola vez, ya que sus cambios son persistentes en la base de datos; sin embargo, no se deben borrar los archivos que las contienen, porque funcionan como un historial (logs) de qué cambios se aplicaron y en qué orden. Por eso, es importante mantenerlos versionados y no modificarlos una vez usados, sino crear nuevos scripts para cada cambio.  
  1. Cambios seguros de ejecutar varias veces:
    - Queries (no modifican nada, solo muestran algo): `docker exec -i nombre_contenedor psql -U postgres -d nombre_db < queries.sql`
    - Actualizar usuario específico, agregar columna si no existe, insertar dato en columna con propiedad UNIQUE. Se inyectan en la BD usando: `docker exec -i nombre_contenedor psql -U postgres -d nombre_db < updates_reejecutables/nombre_update.sql`. EJEMPLO:
    
  ```sql
  -- Actualizar usuario específico
  UPDATE usuarios
  SET edad = 24
  WHERE id = 2;

  -- Agregar columna si no existe
  ALTER TABLE usuarios
  ADD COLUMN IF NOT EXISTS email VARCHAR(50);

  -- Insertar dato en columna con propiedad UNIQUE
  INSERT INTO usuarios (nombre, edad)
  VALUES ('Luis', 25)
  ON CONFLICT (nombre) DO NOTHING;
  ```
  

  2. Cambios que pueden duplicar o borrar datos.
    - Insertar dato en columna que no tiene la propiedad UNIQUE, borrar, borrar sólo si cumple X condición. Se inyectan en la BD usando: `docker exec -i nombre_contenedor psql -U postgres -d nombre_db < updates_unicas/nombre_update.sql`

  ```sql
  -- Insertar dato en columna que no tiene la propiedad UNIQUE
  INSERT INTO usuarios (nombre, edad)
  VALUES ('Luis', 25);

  -- Borrar sólo si cumple condición
  DELETE FROM usuarios
  WHERE nombre = 'Temp';
  ```
  

5. Cuando se desea apagar Docker (sin perder nada): `docker compose down`

6. Cuando se desea reiniciar Docker, repito pasos a partir del 4°.

---

COMANDOS ADICIONALES:  
De uso según necesidad. 
Se ejecutarían en psql (si se usan inyecciones no resultan necesarios).
- `\q` - salir de psql y volver a la Terminal
- `\l` - ver bases de datos
- `\dt`- ver tablas
- `\conninfo`- ver conexión actual

---

OTROS:  
PRECAUCION: Estos comandos eliminan datos y vuelven a ejecutar `schema.sql` y `data.sql` porque vuelven a correr el archivo `docker-compose.yml`.
1. `docker compose down -v`
2. `docker compose up -d`