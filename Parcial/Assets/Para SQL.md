
### Table of Contents

- [Relación `1:1`](#relación-11)
- [Relación `1:N`](#relación-1n)
- [Relación `N:N`](#relación-nn)
- [Ej 1 - Múltiples `N:N`](#ej-1---múltiples-nn)
- [Ej 2 - Múltiples `N:N`](#ej-2---múltiples-nn)

<br>

---

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
