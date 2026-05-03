
> **Idea:** este tema se entiende de verdad cuando separas con claridad patron, herramienta de busqueda y herramienta de transformacion.

## Keywords a saber

`regex`, `grupo`, `coleccion`, `cuantificadores`, `anclajes`, `grep`, `sed`, `clases de caracteres`, `rangos`, `\w`, `\s`, `^`, `$`, `reemplazo`

> **Para estudiar:** si una expresion te abruma, desarmala por piezas: que caracteres permite, cuantas veces, y en que posicion.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `regex` | Patron formal para describir formas de texto. | No entiende "significado humano"; reconoce estructuras textuales repetibles. |
| `grupo` | Parte de una regex encerrada para agrupar o capturar contenido. | Sirve para tratar varias piezas como una unidad y, en muchos casos, reutilizar lo encontrado. |
| `coleccion` | Conjunto de caracteres posibles dentro de una expresion, como `[abc]`. | Expresa "aca puede aparecer uno de estos", en lugar de fijar un unico caracter. |
| `cuantificadores` | Operadores que indican cuantas veces puede repetirse algo. | Son los que vuelven flexible el patron: una vez, muchas, opcional, etc. |
| `anclajes` | Marcas que fijan posicion, como inicio o fin de linea. | Sirven para evitar coincidencias parciales cuando queres controlar exactamente donde aparece algo. |
| `grep` | Herramienta para buscar lineas que coincidan con un patron. | `grep` no inventa el patron; lo aplica. La logica vive en la regex, la busqueda la hace la herramienta. |
| `sed` | Herramienta para editar y reemplazar texto por linea. | Mientras `grep` filtra, `sed` transforma. Esa diferencia conviene tenerla clarisima. |
| `clases de caracteres` | Atajos para tipos de caracteres, como digitos o espacios. | Ahorran escribir colecciones largas y hacen mas expresiva la regex. |
| `rangos` | Forma compacta de indicar intervalos, como `[a-z]`. | Son una manera corta de listar muchos caracteres posibles sin escribirlos uno por uno. |
| `\w` | Atajo habitual para caracter alfanumerico o guion bajo. | Es comodo, pero puede variar segun el motor de regex que uses. |
| `\s` | Atajo habitual para espacio en blanco. | Tambien depende del dialecto y puede incluir espacios, tabs o saltos segun el caso. |
| `^` | Anclaje de inicio de linea o cadena. | Ayuda a decir "esto tiene que empezar asi", no solo "contener algo parecido". |
| `$` | Anclaje de fin de linea o cadena. | Completa la idea anterior: fija donde debe terminar la coincidencia. |
| `reemplazo` | Sustitucion de una coincidencia por otro texto. | Es lo que convierte una deteccion en una transformacion concreta del contenido. |

## Tabla comparativa rapida

| Elemento | Rol | Ejemplo |
| --- | --- | --- |
| `regex` | Define el patron | `^[A-Z].*` |
| `grep` | Busca coincidencias | `grep 'error' archivo.txt` |
| `sed` | Reemplaza o transforma | `sed 's/foo/bar/' archivo.txt` |

## Mapa mental rapido

La forma correcta de pensar este tema es:

```text
regex define la forma del texto
-> grep usa esa forma para encontrar
-> sed usa esa forma para cambiar
```

Si se mezclan esas tres capas, el tema se vuelve confuso. Si se separan, se vuelve bastante mas claro.

## Lo que mas se suele confundir

- una `regex` no es una herramienta, sino una forma de describir patrones.
- `grep` usa patrones para encontrar; `sed` usa patrones para cambiar.
- que una cadena "matchee" una regex no significa necesariamente que sea semanticamente correcta; puede tener la forma esperada y aun asi ser invalida en el mundo real.

## Como leer este apunte

Este archivo toma el resumen de `Slides` y lo vuelve un apunte de estudio mas completo, pensado para alguien que esta viendo el tema por primera vez.

La idea principal es separar tres cosas que suelen mezclarse:

- regex: el patron;
- `grep`: la herramienta para buscar;
- `sed`: la herramienta para transformar texto.

## 1. Que es una expresion regular

Una expresion regular, o regex, es una forma de describir patrones de texto.

No describe significado profundo. Describe forma.

Eso quiere decir que una regex sirve para responder preguntas como:

- esta cadena tiene formato de mail?
- esta fecha tiene pinta correcta?
- esta linea contiene cierta estructura?

Pero no necesariamente puede garantizar que el contenido sea semanticamente valido.

Ejemplos:

- una regex puede validar que algo parezca una fecha;
- no necesariamente puede garantizar que esa fecha exista en el calendario.

## 2. Para que se usan las regex

Se usan para:

- buscar patrones;
- validar formatos;
- extraer partes de un texto;
- reemplazar fragmentos;
- limpiar datos;
- filtrar lineas;
- trabajar con archivos desde terminal.

En la practica, aparecen mucho junto con:

- `grep`
- `sed`
- editores de texto
- scripts Bash

## 3. Idea mental correcta

Conviene pensar una regex como una descripcion formal de una forma textual.

No "entiende" el contenido. Lo compara contra una estructura.

Ejemplo:

```text
algo@dominio.com
```

Una regex puede chequear si una cadena tiene esa forma general, pero no si el dominio realmente existe.

## 4. Variantes o dialectos

No todas las herramientas usan exactamente la misma variante de regex.

Aparecen familias como:

- POSIX;
- PCRE;
- otras variantes segun la herramienta.

La idea importante no es memorizar dialectos, sino entender que:

- el nucleo conceptual se mantiene;
- pero algunos detalles de sintaxis pueden cambiar.

## 5. Bloques fundamentales

## 5.1 Alternativa u OR

Sintaxis:

```text
A|B
```

Significa:

- coincide con `A`;
- o coincide con `B`.

Se usa cuando hay opciones posibles.

## 5.2 Grupos

Los grupos se escriben con parentesis:

```text
(...)
```

Sirven para:

- agrupar partes de una expresion;
- controlar el alcance de `|`;
- controlar el alcance de cuantificadores;
- ordenar mejor la regex.

Ejemplo conceptual:

```text
ab|cd
```

no significa lo mismo que:

```text
(ab|cd)
```

## 5.3 Comodin `.`

El punto:

```text
.
```

coincide con cualquier caracter.

Eso lo hace muy potente, pero tambien peligroso si lo usas demasiado libremente, porque puede volver el patron demasiado permisivo.

## 5.4 Colecciones o clases de caracteres

Sintaxis:

```text
[abc]
```

Significa:

- coincide con un unico caracter;
- y ese caracter puede ser `a`, `b` o `c`.

La coleccion trabaja caracter por caracter.

## 5.5 Rangos

Dentro de colecciones se pueden usar rangos:

```text
[a-z]
[A-Z]
[0-9]
```

Eso evita escribir uno por uno todos los caracteres posibles.

## 6. Diferencia entre grupo y coleccion

Esta diferencia es clave.

### Grupo

- agrupa subexpresiones;
- puede contener secuencias completas;
- sirve para estructurar el patron.

### Coleccion

- describe un conjunto de caracteres posibles;
- siempre actua sobre un solo caracter por vez.

Regla mental:

```text
grupo = estructura
coleccion = inventario de caracteres
```

## 7. Tokens utiles

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

- letras;
- numeros;
- guion bajo.

### `\W`

No caracter de palabra.

### `\b`

Limite de palabra.

Sirve para ubicar el borde entre una palabra y lo que no es palabra.

### `\B`

No limite de palabra.

### `^`

Fuera de una coleccion:

- inicio de linea.

Dentro de una coleccion:

- negacion del conjunto.

### `$`

Fin de linea.

### `\`

Escape.

Sirve para indicar que un simbolo especial debe tratarse literalmente, o para usar secuencias como `\w`, `\s`, etc.

## 8. Cuantificadores

Los cuantificadores indican cuantas veces puede aparecer el patron anterior.

### `*`

Cero o mas veces.

### `+`

Una o mas veces.

### `?`

Cero o una vez.

Idea clave:

- cuantifican lo inmediatamente anterior;
- si queres ampliar su alcance, necesitas usar grupos.

Ejemplo:

```text
ab+
```

significa:

- `a`
- seguido por una o mas `b`

No significa repetir `ab` completo. Para eso haria falta:

```text
(ab)+
```

## 9. Anclajes

### `^`

Inicio de linea.

### `$`

Fin de linea.

## Para que sirven

Sirven para evitar coincidencias parciales cuando queres validar una linea entera.

Sin anclajes, una regex puede coincidir "por dentro" de una cadena mas larga.

Con anclajes, exigis forma total.

## 10. `grep`

## 10.1 Que es

`grep` es una herramienta de linea de comandos para buscar patrones dentro de archivos o salidas de otros comandos.

Forma general:

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

Muestra solo los nombres de archivos donde aparece el patron.

## 10.3 Ejemplos de uso

```bash
grep "ejemplo" archivo1.txt archivo2.txt archivo3.csv
grep "ejemplo" *
grep "ejemplo" *.log
grep "ejemplo" ruta/a/directorio/*
grep -r "ejemplo" .
grep -r "ejemplo" ./ruta/a/directorio/
```

Esto muestra que `grep` no sirve solo para un archivo aislado. Tambien puede:

- recorrer varios archivos;
- aprovechar wildcards;
- explorar directorios enteros.

## 10.4 Casos practicos

El tema suele aplicarse a casos como:

- buscar notas de una persona en un CSV;
- encontrar alumnos entre ciertas edades;
- detectar datos mal formados;
- filtrar lineas en logs o reportes.

O sea: regex + `grep` no es solo teoria, sino una forma practica de explotar texto semiestructurado.

## 11. `sed`

## 11.1 Que es

`sed` es una herramienta para procesar y transformar texto.

En esta materia conviene pensarla sobre todo como:

- herramienta de busqueda y reemplazo;
- filtro de lineas;
- transformador de texto desde terminal.

Forma general:

```bash
sed [script] [archivo]
```

Reemplazo clasico:

```bash
sed 's/patron/reemplazo/' archivo
```

## 11.2 Operaciones utiles

### `-i`

Modifica el archivo directamente.

### `-e`

Permite concatenar operaciones.

### `-r`

Usa expresiones regulares extendidas.

### `Nd`

Elimina la linea numero `N`.

### `/patron/d`

Elimina lineas que coinciden con el patron.

### `/patron/p`

Imprime lineas coincidentes.

### `s/patron/reemplazo/g`

Reemplaza todas las coincidencias de la linea.

### `s/patron/reemplazo/I`

Ignora mayusculas y minusculas durante el reemplazo.

## 11.3 Advertencia importante

Si no usas `-i`, muchas veces `sed` no modifica el archivo: imprime el resultado transformado por salida estandar.

Eso es util para probar antes de hacer cambios destructivos.

## 12. Ejercicios tipicos del tema

Algunos ejercicios representativos son:

- sustituir todas las vocales de un archivo por otra letra;
- transformar notas desaprobadas a un valor minimo;
- adaptar una regex cuando cambia el formato de los datos;
- intercambiar valores entre dos personas en un solo comando.

## Que ensenian esos ejercicios

- que una regex ingenua puede fallar;
- que hay que pensar casos borde;
- que reemplazar bien depende tanto del patron como de la estructura de los datos.

## 13. Como pensar una regex

Una secuencia mental util es esta:

1. definir exactamente que forma queres aceptar;
2. separar partes fijas y variables;
3. elegir colecciones, grupos, cuantificadores y anclajes;
4. probar contra ejemplos validos e invalidos;
5. ajustar casos borde.

## 14. Errores comunes

- usar `.` cuando deberia usarse un patron mas restringido;
- olvidar `^` y `$` al validar una linea completa;
- confundir grupo con coleccion;
- creer que una regex valida significado real y no solo forma;
- olvidar que `*`, `+` y `?` aplican a lo inmediatamente anterior;
- usar `sed -i` sin probar antes la version no destructiva.

## 15. Diferencia entre regex, grep y sed

### Regex

Es el patron.

### `grep`

Usa regex para buscar.

### `sed`

Usa regex principalmente para transformar o filtrar texto.

Regla de memoria:

```text
regex = patron
grep = encontrar
sed = transformar
```

## 16. Preguntas de estudio posibles

1. Que es una expresion regular?
2. Para que sirve?
3. Que diferencia hay entre grupo y coleccion?
4. Que hace el comodin `.`?
5. Que significan `\w`, `\W`, `\s`, `\S`, `\b`, `\B`?
6. Que cambia con `^` dentro y fuera de una coleccion?
7. Que hacen `*`, `+` y `?`?
8. Para que sirven los anclajes?
9. Que es `grep`?
10. Que hacen `-i`, `-n`, `-w`, `-v`, `-r`, `-c`, `-l`?
11. Que es `sed`?
12. Que hace `sed 's/patron/reemplazo/g'`?
13. Que efecto tiene `-i`?
14. Por que regex no garantiza semantica real?

## 17. Resumen final

Las ideas mas importantes del tema son:

- regex describe forma textual;
- grupo no es lo mismo que coleccion;
- `.` coincide con cualquier caracter;
- `\s` representa espacio en blanco;
- `\w` representa caracter de palabra;
- `^` marca inicio y `$` marca final;
- `*`, `+` y `?` controlan cantidad;
- `grep` busca;
- `sed` transforma.


