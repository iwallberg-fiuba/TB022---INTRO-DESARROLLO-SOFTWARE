
> **Idea:** este archivo muestra a Bash resolviendo un problema real: recibir archivos, validarlos, transformarlos y dejar todo ordenado sin trabajo manual repetitivo.

## Keywords a saber

`parametros posicionales`, `validacion`, `case`, `grep`, `sed`, `recorrido de archivos`, `directorios`, `automatizacion`, `procesamiento de texto`, `script`, `acciones`, `errores`

> **Para estudiar:** cada keyword de este apunte tiene sentido dentro de un flujo de trabajo; no conviene estudiarlas como comandos aislados.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `parametros posicionales` | Valores que un script recibe por orden, como `$1` o `$2`. | Son la forma mas directa de volver reutilizable un script: en vez de hardcodear datos, los recibis al ejecutarlo. |
| `validacion` | Comprobacion de que una entrada o archivo cumple lo esperado. | Es clave porque automatizar sin validar puede propagar errores mas rapido en lugar de ahorrarte trabajo. |
| `case` | Estructura que elige una accion segun el valor recibido. | Sirve mucho cuando el script ofrece varias acciones posibles y queres una seleccion clara. |
| `grep` | Herramienta para buscar texto segun patrones. | En ejercicios practicos se usa para detectar si un archivo contiene o no cierta estructura. |
| `sed` | Herramienta para transformar texto con reglas de edicion. | Es util cuando no solo queres detectar algo, sino tambien modificarlo de forma automatica. |
| `recorrido de archivos` | Proceso de iterar por archivos dentro de una carpeta. | Aparece en cualquier automatizacion masiva, porque rara vez trabajas con un solo archivo aislado. |
| `directorios` | Carpetas que organizan archivos y subcarpetas. | En este ejercicio no son detalle administrativo: separan estados distintos del trabajo, como originales y procesados. |
| `automatizacion` | Ejecucion repetible de tareas sin hacerlas manualmente una por una. | Ese es el problema central del ejercicio: que una tarea aburrida, lenta o propensa a errores pase a ser sistematica. |
| `procesamiento de texto` | Lectura, filtro y transformacion de contenido textual. | Es la materia prima de Bash en muchos ejercicios: mas que interfaces graficas, trabaja muy bien sobre texto. |
| `script` | Archivo ejecutable con pasos automatizados escritos en shell. | Es un procedimiento guardado. La ventaja no es solo velocidad, sino tambien repetir siempre la misma logica. |
| `acciones` | Operaciones que el script sabe realizar segun el argumento recibido. | Pensarlas como "modos de uso" ayuda a disenar un script mas claro y menos confuso. |
| `errores` | Situaciones invalidas que el script debe detectar y manejar. | Un buen script no solo hace el caso feliz; tambien informa cuando algo falta, esta mal o no puede seguir. |

## Tabla comparativa rapida

| Pieza | Rol en el ejercicio |
| --- | --- |
| `parametros posicionales` | Definen accion y directorio de trabajo |
| `validacion` | Decide si un archivo sirve o debe descartarse |
| `procesamiento de texto` | Limpia o transforma el contenido |
| `automatizacion` | Evita hacer a mano las mismas tareas en cada entrega |

## Mapa mental rapido

El sentido del ejercicio se puede resumir asi:

```text
recibo archivos
-> reviso si cumplen reglas
-> tomo una accion segun el caso
-> transformo contenido si hace falta
-> dejo todo ordenado sin hacerlo a mano una y otra vez
```

Si ves ese flujo, ya no parece un ejercicio de comandos aislados, sino de resolucion de problema.

## Lo que mas se suele confundir

- `automatizar` no significa "hacer todo sin pensar": un script util valida entradas y corta a tiempo cuando algo esta mal.
- `case` no esta para decorar el script, sino para volver legible la eleccion entre distintas acciones posibles.
- `grep` y `sed` suelen aparecer juntos, pero no hacen lo mismo: uno detecta patrones y el otro transforma contenido.

## Material de referencia

- Repositorio: <https://github.com/RiedelNicolas/bash-exercise>
- Video de la clase: <https://youtu.be/dGo6IiAdvvs>

## Como leer este apunte

Este archivo conserva el ejercicio integrador original, pero lo reescribe como guia de interpretacion.

La idea es que no leas el enunciado solo como una lista de pasos, sino como un problema de automatizacion con Bash.

## 1. Situacion planteada

El escenario es el de una correccion masiva de entregas.

Hay muchos archivos `.txt` que llegaron a una carpeta, pero:

- algunos nombres son desordenados;
- no todos respetan el formato pedido;
- y revisar todo a mano no escala.

Por eso el ejercicio pide un script que:

- cree estructura de trabajo;
- valide archivos;
- genere una version procesada;
- y genere una variante "burlona".

## 2. Objetivo del script

Hay que escribir un archivo llamado:

```bash
gestionar_entregas.sh
```

Debe recibir dos parametros:

```bash
bash gestionar_entregas.sh <accion> <directorio>
```

Lectura:

- primer parametro: la accion;
- segundo parametro: el directorio base de trabajo.

## 3. Estructura de carpetas esperada

El trabajo gira alrededor de un directorio base, por ejemplo `entregas`.

Dentro de ese directorio deben existir estas carpetas:

```text
entregas/
|-- originales/
|-- procesadas/
`-- burlas/
```

Cada carpeta cumple un rol distinto:

- `originales/`: archivos tal como llegaron;
- `procesadas/`: archivos ya validados y sin encabezado;
- `burlas/`: archivos transformados con el reemplazo de vocales.

## 4. Accion `inicializar`

Ejemplo:

```bash
bash gestionar_entregas.sh inicializar entregas
```

Que se espera:

1. crear el directorio base si no existe;
2. crear las carpetas internas necesarias;
3. informar para cada carpeta si fue creada o si ya existia.

Punto importante:

- la accion debe ser idempotente;
- o sea, correrla dos veces no deberia romper nada.

## 5. Accion `procesar`

Ejemplo:

```bash
bash gestionar_entregas.sh procesar entregas
```

Esta es la accion principal del ejercicio.

Debe recorrer todos los `.txt` dentro de:

```text
entregas/originales/
```

Para cada archivo hay que hacer tres cosas.

### 5.1 Validar encabezado

La primera linea debe tener este formato:

```text
Alumno: Apellido, Nombre - Padron: NNNNNN
```

Donde `NNNNNN` es un numero de exactamente 6 digitos.

Ejemplo valido:

```text
Alumno: Garcia, Juan - Padron: 104560
```

Que implica validar:

- que la primera linea exista;
- que empiece con `Alumno:`;
- que incluya apellido y nombre en ese orden;
- que tenga la parte `Padron:`;
- que el padron tenga exactamente 6 digitos.

Si no cumple:

- se informa error;
- se saltea el archivo;
- no se genera version procesada.

### 5.2 Extraer el padron

Del encabezado hay que sacar el numero de padron.

Ese numero define el nombre del archivo de salida:

```text
entregas/procesadas/104560.txt
```

Esto importa porque el corrector no deberia depender del nombre original del archivo.

### 5.3 Quitar el encabezado

El archivo procesado no debe incluir la primera linea con los datos del alumno.

O sea:

- se usa el archivo original como fuente;
- se toma todo menos la primera linea;
- se guarda eso en `procesadas/`.

## 6. Accion `burlarme`

Ejemplo:

```bash
bash gestionar_entregas.sh burlarme entregas
```

Debe recorrer todos los `.txt` dentro de:

```text
entregas/procesadas/
```

y generar una copia en:

```text
entregas/burlas/
```

La transformacion es:

- `a`, `e`, `o`, `u` se reemplazan por `i`;
- `A`, `E`, `O`, `U` se reemplazan por `I`.

Ejemplo:

```text
La funcion recibe como parametro una lista de enteros.
```

se transforma en:

```text
Li fincion ricibi cimi pirimitri ini listi di intiris.
```

Observacion importante:

- el enunciado no menciona reemplazar la `i`;
- por eso la `i` se deja como esta.

## 7. Accion invalida

Si la accion no es:

- `inicializar`
- `procesar`
- `burlarme`

entonces el script debe informar error y mostrar opciones validas.

Esto normalmente se resuelve bien con `case`.

## 8. Validaciones generales

### Faltan parametros

Si no llegan exactamente los dos parametros necesarios, el script debe mostrar:

```text
Uso: bash gestionar_entregas.sh <accion> <directorio>
```

### Directorio inexistente

Si la accion no es `inicializar` y el directorio base no existe, hay que mostrar error.

Eso evita intentar procesar rutas que no estan preparadas.

## 9. Que conocimientos de Bash pone en juego

Este ejercicio mezcla varias cosas de la materia:

- parametros posicionales como `$1` y `$2`;
- validaciones con `if`;
- multiples casos con `case`;
- recorrido de archivos;
- lectura de lineas;
- expresiones regulares o herramientas como `grep` y `sed`;
- redireccion de salida;
- creacion de carpetas y archivos.

O sea: no es un ejercicio de un solo comando, sino de composicion.

## 10. Una forma sana de pensar la resolucion

Conviene dividir mentalmente el problema en partes:

1. validar argumentos;
2. decidir accion;
3. preparar rutas;
4. recorrer archivos;
5. validar encabezado;
6. transformar contenido;
7. guardar resultados;
8. informar errores o acciones realizadas.

Si intentas escribir todo lineal y sin separar responsabilidades, el script se vuelve confuso enseguida.

## 11. Errores tipicos al resolverlo

- asumir que cualquier primer renglon sirve;
- usar el nombre original del archivo en vez del padron;
- olvidarse de saltear archivos invalidos;
- procesar todo el archivo sin quitar la primera linea;
- no contemplar mayusculas en `burlarme`;
- no validar cantidad de parametros;
- no manejar accion invalida.

## 12. Idea final

Este ejercicio no busca solo que "ande", sino que muestre que entendes como Bash sirve para automatizar una tarea real:

- organiza archivos;
- valida formato;
- transforma texto;
- y responde distinto segun la accion pedida.

Una buena solucion deberia ser:

- correcta;
- clara;
- y suficientemente ordenada como para que otro corrector la entienda rapido.


