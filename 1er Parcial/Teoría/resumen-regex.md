# Apunte largo - Regex, grep y sed

## Fuente trabajada

- `Intro a Regex.pdf`

## Idea global del tema

Las expresiones regulares son una forma de describir patrones de texto. No describen significado profundo, sino forma textual. El material las presenta como una herramienta transversal para:

- buscar,
- validar,
- reemplazar,
- parsear,
- limpiar datos,
- y trabajar con archivos desde terminal.

## 1. Motivacion intuitiva del tema

Las primeras diapositivas plantean preguntas del tipo:

- cuales cadenas podrian ser nombres validos?
- cuales podrian pertenecer a una familia?
- cuales fechas tienen forma correcta?
- cuales mails tienen forma valida?

### Mensaje pedagogico

Regex sirve para decidir si un texto coincide o no con una estructura determinada.

## 2. Para que se usan las regex

- busqueda de patrones,
- reemplazo de fragmentos,
- validacion de formatos,
- parseo y extraccion de partes,
- limpieza de datos,
- debugging,
- refactorizaciones,
- busqueda avanzada en archivos y logs.

## 3. Variantes o dialectos

El material menciona que hay variantes:

- POSIX,
- PCRE,
- y otras.

### Idea importante

No todas las herramientas soportan exactamente lo mismo, pero el nucleo conceptual se mantiene.

## 4. Concepto mental correcto

Regex no "entiende" el contenido. Lo compara con una forma.

### Ejemplos

- Una regex puede validar que algo tenga pinta de mail.
- No puede garantizar por si sola que ese dominio exista.
- Una regex puede verificar que algo tenga estructura de fecha.
- No necesariamente que sea una fecha calendariamente real.

## 5. Bloques fundamentales

## 5.1 OR o alternativa

### Sintaxis

```text
A|B
```

### Significado

Coincide con A o con B.

### Uso conceptual

Cuando hay opciones mutuamente posibles.

## 5.2 Grupos

Se usan para:

- agrupar partes,
- controlar el alcance de `|`,
- controlar el alcance de cuantificadores,
- organizar la regex mentalmente.

### Ejemplo conceptual

No es lo mismo:

- `ab|cd`
- que `(ab|cd)`

El agrupamiento importa.

## 5.3 Comodin

### `.` 

Coincide con cualquier caracter.

### Cuidado

Si se usa sin control, puede volver la regex demasiado permisiva.

## 5.4 Colecciones o clases de caracteres

### Sintaxis general

```text
[abc]
```

Coincide con un caracter que sea `a`, `b` o `c`.

### Idea central

La coleccion elige un caracter dentro de un conjunto.

## 5.5 Rangos

Se usan dentro de colecciones:

- `[a-z]`
- `[A-Z]`
- `[0-9]`

## 6. Diferencia entre grupo y coleccion

Esta es una distincion muy preguntable.

### Grupo

- agrupa subexpresiones,
- puede contener secuencias completas,
- sirve para organizar alternativas o repeticiones.

### Coleccion

- describe un conjunto de caracteres posibles,
- siempre trabaja caracter por caracter.

### Regla mental

- grupo = estructura,
- coleccion = inventario de caracteres permitidos.

## 7. Tokens importantes

### `.` 

Cualquier caracter.

### `\n`

Nueva linea.

### `\t`

Tabulacion.

### `\s`

Cualquier espacio en blanco.

### `\S`

Cualquier caracter que no sea espacio en blanco.

### `\w`

Caracter de palabra:

- letras,
- numeros,
- guion bajo.

### `\W`

No caracter de palabra.

### `\b`

Limite de palabra.

Sirve para encontrar el borde entre caracter de palabra y no-palabra.

### `\B`

No limite de palabra.

### `^`

#### Fuera de coleccion

Inicio de linea.

#### Dentro de coleccion

Niega el conjunto.

### `$`

Fin de linea.

### `\`

Escape o barra invertida literal, segun el caso.

## 8. Cuantificadores

Los cuantificadores dicen cuantas veces puede aparecer el patron anterior.

### `*`

Cero o mas.

### `+`

Uno o mas.

### `?`

Cero o uno.

### Idea clave

Siempre cuantifican lo inmediatamente anterior, salvo que uses grupos para ampliar el alcance.

## 9. Anclajes

### `^`

Principio de linea.

### `$`

Fin de linea.

### Para que sirven

Evitan coincidencias parciales cuando queres validar una linea completa.

### Ejemplo mental

Sin anclajes, una cadena puede matchear "por dentro".
Con anclajes, exigis forma total.

## 10. `grep`

## 10.1 Que es

Herramienta de linea de comandos para buscar patrones dentro de archivos.

### Forma general

```bash
grep [opciones] [patron] [archivo]
```

## 10.2 Opciones importantes

### `-i`

Ignora mayusculas y minusculas.

### `-n`

Muestra numero de linea.

### `-w`

Coincide solo con palabras completas.

### `-v`

Muestra lineas que no contienen el patron.

### `-r`

Busca recursivamente en subdirectorios.

### `-c`

Cuenta lineas coincidentes.

### `-l`

Muestra solo nombres de archivos donde aparece el patron.

## 10.3 Buscar en multiples archivos

El material da varios ejemplos:

```bash
grep "ejemplo" archivo1.txt archivo2.txt archivo3.csv
grep "ejemplo" *
grep "ejemplo" *.log
grep "ejemplo" ruta/a/directorio/*
grep -r "ejemplo" .
grep -r "ejemplo" ./ruta/a/directorio/
```

### Idea importante

`grep` no es solo "buscar en un archivo"; puede escalar a conjuntos de archivos y arboles enteros de directorios.

## 10.4 Casos practicos del material

- Buscar notas de una persona en `notas.csv`.
- Buscar notas de una persona en todos los archivos de un directorio.
- Buscar alumnos con nota mayor o igual a `85.2`.
- Encontrar codigos postales argentinos mal formados.
- Buscar alumnos entre 25 y 29 años.

### Lectura didactica

Esto muestra que regex + grep no sirve solo para texto suelto, sino para explotar datos semiestructurados.

## 11. `sed`

## 11.1 Que es

Herramienta para procesar y manipular texto. El material la enfoca principalmente como herramienta de busqueda y reemplazo.

### Forma general

```bash
sed [script] [archivo]
```

### Reemplazo clasico

```bash
sed 's/patron/reemplazo/' archivo
```

## 11.2 Opciones y operaciones vistas

### `-i`

Modifica el archivo en lugar de solo imprimir resultado.

### `-e`

Concatena operaciones.

### `-r`

Usa expresiones regulares extendidas.

### `Nd`

Elimina la linea numero N.

### `/patron/d`

Elimina lineas que matchean.

### `/patron/p`

Imprime lineas coincidentes.

### `s/patron/reemplazo/g`

Reemplaza todas las coincidencias en la linea.

### `s/patron/reemplazo/I`

Ignora mayusculas/minusculas al reemplazar.

## 11.3 Advertencia conceptual

Si no usas `-i`, muchas veces `sed` no modifica el archivo: imprime el resultado transformado a salida estandar.

## 12. Ejercicios del material

### Ejercicio 1

Sustituir todas las vocales de `cancion.txt` por `a`.

### Ejercicio 2

Transformar a `55` las notas desaprobadas (`nota < 55`).

### Ejercicio 3

Adaptar la regex cuando las notas menores a `10` tienen un solo digito.

### Ejercicio 4

Intercambiar notas entre dos personas en un solo comando.

### Que enseñan estos ejercicios

- que una regex naive puede fallar con formatos reales,
- que los bordes del problema importan,
- que reemplazar bien exige pensar tanto en patron como en estructura de datos.

## 13. Como pensar una regex

### Paso 1

Definir exactamente que forma queres aceptar.

### Paso 2

Identificar partes fijas y partes variables.

### Paso 3

Elegir:

- colecciones,
- rangos,
- grupos,
- cuantificadores,
- anclajes.

### Paso 4

Probar contra ejemplos validos e invalidos.

### Paso 5

Ajustar casos borde.

## 14. Errores comunes

### Error 1

Usar `.` cuando deberia usarse una clase mas restringida.

### Error 2

Olvidar anclajes `^` y `$` al validar linea completa.

### Error 3

Confundir grupo con coleccion.

### Error 4

Creer que una regex valida semantica real y no solo forma.

### Error 5

Olvidar que `*`, `+` y `?` aplican a lo inmediatamente anterior.

### Error 6

Modificar archivos con `sed -i` sin probar antes la version no destructiva.

## 15. Diferencias practicas entre regex, grep y sed

### Regex

Es el lenguaje o sistema de patrones.

### grep

Usa regex para buscar.

### sed

Usa regex principalmente para transformar o filtrar texto.

### Regla de memoria

- regex = patron,
- grep = encontrar,
- sed = transformar.

## 16. Posibles preguntas de parcial

1. Que es una expresion regular?
2. Para que sirve una regex?
3. Que diferencia hay entre grupo y coleccion?
4. Que hace el comodin `.`?
5. Que significan `\w`, `\W`, `\s`, `\S`, `\b`, `\B`?
6. Diferencia entre `^` dentro y fuera de una coleccion.
7. Que hacen `*`, `+` y `?`?
8. Para que sirven los anclajes?
9. Que es `grep` y para que sirve?
10. Explica `-i`, `-n`, `-w`, `-v`, `-r`, `-c`, `-l`.
11. Que es `sed` y para que se usa en el material?
12. Que hace `sed 's/patron/reemplazo/g'`?
13. Que efecto tiene `-i` en `sed`?
14. Por que regex no garantiza significado semantico?

## 17. Memorizacion rapida

- Regex describe forma textual.
- Grupo = estructura. Coleccion = conjunto de caracteres.
- `.` cualquier caracter.
- `\s` espacio. `\w` caracter de palabra.
- `^` inicio. `$` final.
- `*` cero o mas. `+` uno o mas. `?` cero o uno.
- `grep` busca.
- `sed` reemplaza y transforma.
