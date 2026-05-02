
> **Idea:** Bash sirve cuando queres pasar de escribir comandos aislados a pensar en flujo, automatizacion y control del sistema desde texto.

## Keywords a saber

`shell`, `terminal`, `stdin`, `stdout`, `stderr`, `pipes`, `redireccion`, `variables`, `scripts`, `chmod`, `if`, `for`, `while`, `case`, `shebang`

> **Para estudiar:** intenta ubicar cada keyword en una de estas tres categorias: `interfaz`, `flujo de datos` o `logica del script`.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `shell` | Interprete de comandos que recibe ordenes y ejecuta programas. | Es el "traductor operativo" entre lo que escribis y lo que el sistema hace. |
| `terminal` | Ventana o interfaz donde interactuas con el shell. | No ejecuta por si sola la logica del comando: muestra y transporta la interaccion. |
| `stdin` | Entrada estandar que un programa recibe por defecto. | Muchas veces viene del teclado, pero tambien puede venir de un archivo o de otro comando. |
| `stdout` | Salida estandar normal que un programa emite por defecto. | Es el canal pensado para resultados correctos y reutilizables. Por eso despues se puede encadenar con pipes. |
| `stderr` | Salida estandar reservada para errores. | Separar errores de salida normal permite automatizar mejor sin mezclar mensajes utiles con fallos. |
| `pipes` | Mecanismo para pasar la salida de un comando como entrada de otro. | Es una de las ideas mas potentes de Bash: construir procesos chicos que colaboran entre si. |
| `redireccion` | Desvio de entrada o salida hacia archivos u otros destinos. | Te deja decidir de donde lee un comando y a donde manda lo que produce. |
| `variables` | Nombres que guardan valores reutilizables dentro del shell o script. | Evitan repetir datos y vuelven mas flexible un script, porque cambias el valor una vez y afecta varios lugares. |
| `scripts` | Archivos con secuencias de comandos para automatizar tareas. | Son la forma de pasar de "ejecutar cosas a mano" a "dejar un procedimiento guardado y repetible". |
| `chmod` | Comando para cambiar permisos de un archivo o directorio. | En Bash aparece mucho porque un script necesita permiso de ejecucion para correrse comodamente. |
| `if` | Estructura condicional que ejecuta algo segun una condicion. | Sirve para que el script no haga siempre lo mismo, sino que reaccione al contexto. |
| `for` | Bucle que recorre elementos o repite una accion controlada. | Es util cuando ya sabes sobre que conjunto queres iterar. |
| `while` | Bucle que repite mientras una condicion sea verdadera. | Es mejor cuando no sabes cuantas veces va a repetirse algo y dependes de una condicion. |
| `case` | Estructura para elegir acciones segun varios patrones posibles. | Suele ser mas legible que encadenar muchos `if` cuando lo que cambia es una opcion o comando elegido. |
| `shebang` | Primera linea que indica con que interprete debe ejecutarse un script. | Le dice al sistema que shell o lenguaje debe usar para interpretar el archivo al ejecutarlo. |

## Tabla comparativa rapida

| Concepto | Funcion principal | Ejemplo |
| --- | --- | --- |
| `terminal` | Mostrar la interfaz de trabajo | Windows Terminal |
| `shell` | Interpretar lo escrito | Bash |
| `comando` | Ejecutar una accion concreta | `ls` |

## Mapa mental rapido

La mejor forma de entender Bash es esta:

```text
la terminal muestra
-> el shell interpreta
-> los comandos producen salida
-> esa salida se puede redirigir o encadenar
-> y cuando eso se vuelve repetitivo, se guarda en un script
```

Si entendes ese flujo, Bash deja de ser una lista de simbolos raros.

## Lo que mas se suele confundir

- `terminal`, `shell` y `comando` no son lo mismo: la terminal muestra, el shell interpreta y el comando hace una accion concreta.
- `stdout` y `stderr` pueden verse iguales en pantalla, pero no cumplen la misma funcion: uno transporta resultados y el otro errores.
- un `script` no es solo un archivo con comandos pegados; es una forma de dejar un procedimiento repetible, legible y reutilizable.

## Como leer este apunte

Este archivo toma el contenido del apunte largo original, pero lo reordena para que se entienda desde cero.

La idea no es memorizar una lista de comandos sueltos, sino entender:

- que es Bash;
- como se relaciona con la terminal y el sistema operativo;
- como se navega y se trabaja con archivos;
- como se encadenan comandos;
- y como se escriben scripts simples.

## 1. Que es Bash

Bash significa `Bourne Again Shell`.

Es un shell, es decir, un programa que:

- recibe comandos escritos por el usuario;
- los interpreta;
- decide que programa ejecutar;
- y muestra el resultado.

Tambien es un lenguaje de scripting, porque permite escribir archivos con secuencias de comandos y estructuras de control.

## 2. Bash, shell y terminal

Al principio se suelen mezclar tres ideas distintas:

- terminal: la ventana o entorno donde escribis;
- shell: el interprete que entiende lo que escribis;
- comando: la instruccion concreta que queres ejecutar.

Ejemplo:

```text
Windows Terminal -> Bash -> ls
```

La terminal muestra la interfaz. Bash interpreta. `ls` es el comando.

## 3. Como funciona una orden

Cuando escribis algo en la terminal, el flujo conceptual es este:

1. escribis un comando;
2. Bash lo lee;
3. analiza si es un builtin, una expansion o un programa externo;
4. ejecuta la accion;
5. devuelve salida o error.

Ejemplo:

```bash
mkdir nueva_carpeta
```

Bash interpreta que queres crear un directorio y le pide al sistema que lo haga.

## 4. Entrada, salida y error

En Bash aparecen tres flujos estandar:

- `stdin`: entrada estandar;
- `stdout`: salida estandar;
- `stderr`: salida de error.

Por defecto:

- `stdin` suele venir del teclado;
- `stdout` se muestra en pantalla;
- `stderr` tambien se muestra en pantalla.

Esto es importante porque despues se puede redirigir cada flujo a archivos o a otros comandos.

## 5. Anatomia del prompt

Un prompt tipico puede verse asi:

```text
usuario@maquina:~/proyecto$
```

Lectura:

- `usuario`: quien esta usando la sesion;
- `maquina`: nombre del equipo;
- `~/proyecto`: directorio actual;
- `$`: usuario comun.

Si aparece `#`, normalmente estas trabajando como `root`.

## 6. Navegacion basica

Los primeros comandos responden tres preguntas:

- donde estoy;
- que hay aca;
- como me muevo.

```bash
pwd
ls
ls -la
cd Documentos
cd ..
cd ~
cd /
cd -
```

Que hace cada uno:

- `pwd`: muestra el directorio actual;
- `ls`: lista contenido;
- `ls -la`: lista con detalles y archivos ocultos;
- `cd ruta`: cambia de directorio;
- `cd ..`: sube al directorio padre;
- `cd ~`: va al home;
- `cd /`: va a la raiz;
- `cd -`: vuelve al directorio anterior.

## 7. Rutas absolutas y relativas

Una ruta absoluta empieza desde la raiz:

```text
/home/usuario/proyecto/main.py
```

Una ruta relativa depende de donde estas parado:

```text
src/main.py
../notas.txt
./script.sh
```

Significados utiles:

- `.` = directorio actual;
- `..` = directorio padre;
- `~` = home del usuario.

## 8. Sistema de archivos

En sistemas Unix-like todo cuelga de un arbol con raiz `/`.

```text
/
|-- home/
|-- etc/
|-- var/
|-- tmp/
|-- usr/
`-- bin/
```

No hace falta memorizar todo de una vez. Lo importante es entender que:

- los usuarios suelen trabajar dentro de `home`;
- `etc` guarda configuraciones;
- `tmp` se usa para temporales;
- `bin` y otras carpetas del sistema contienen programas.

## 9. Comandos para archivos y carpetas

```bash
mkdir proyecto
touch notas.txt
cp origen.txt destino.txt
mv viejo.txt nuevo.txt
rm archivo.txt
rm -r carpeta
rmdir carpeta_vacia
cat archivo.txt
less archivo_largo.txt
head -n 5 archivo.txt
tail -n 10 archivo.txt
```

Idea general:

- `mkdir`: crea carpetas;
- `touch`: crea archivos vacios o actualiza fecha;
- `cp`: copia;
- `mv`: mueve o renombra;
- `rm`: borra;
- `rmdir`: borra carpetas vacias;
- `cat`: muestra contenido;
- `less`: permite leer por pagina;
- `head`: muestra el comienzo;
- `tail`: muestra el final.

`rm -r` hay que usarlo con cuidado: no manda nada a una papelera.

## 10. Wildcards

Los wildcards sirven para seleccionar varios archivos con un patron.

```bash
ls *.txt
rm *.log
cp foto_*.jpg backup/
ls archivo?.txt
ls [a-z]*.md
```

Significados:

- `*`: cualquier cantidad de caracteres;
- `?`: un caracter;
- `[abc]`: uno entre varios;
- `[a-z]`: rango.

## 11. Variables

En Bash una variable se define sin espacios alrededor del `=`.

```bash
nombre="Jose"
edad=30
```

Para leer su valor se usa `$`:

```bash
echo "Mi nombre es $nombre y tengo $edad anios."
```

Regla importante:

```bash
nombre = "Jose"
```

eso esta mal en Bash, porque los espacios rompen la asignacion.

### Variables de entorno

Algunas variables ya existen en la sesion:

- `$HOME`
- `$PATH`
- `$USER`
- `$PWD`

Ejemplo:

```bash
echo "Estoy en $PWD y mi home es $HOME"
```

### Variables especiales

En scripts aparecen variables muy utiles:

- `$0`: nombre del script;
- `$1`, `$2`, ...: parametros recibidos;
- `$#`: cantidad de parametros;
- `$?`: codigo de salida del ultimo comando;
- `$$`: PID del proceso actual;
- `$@`: todos los parametros.

## 12. Expansiones

Bash reemplaza ciertas partes antes de ejecutar el comando final.

### Expansion de variables

```bash
echo "$HOME"
```

### Sustitucion de comandos

```bash
echo "Hoy es $(date)"
```

Eso ejecuta `date` y reemplaza la expresion por su salida.

### Historial con `!`

Algunas expansiones usan el historial:

- `!!`: repite el ultimo comando;
- `!ls`: busca el ultimo comando que empezo con `ls`.

Esto es comodo, pero conviene usarlo con cuidado porque ejecuta de verdad.

### Evitar expansiones

Las comillas simples bloquean expansion:

```bash
echo 'El valor de $HOME no se expande aca'
```

El backslash tambien puede escapar caracteres:

```bash
echo \$HOME
```

## 13. Redireccion

Una de las ideas mas importantes de Bash es que la salida de un comando se puede redirigir.

### Salida a archivo

```bash
echo "Hola" > saludo.txt
echo "Otra linea" >> saludo.txt
```

- `>` sobrescribe;
- `>>` agrega al final.

### Entrada desde archivo

```bash
wc -w < archivo.txt
```

Eso toma el contenido del archivo como entrada del comando.

### Errores

Tambien se puede redirigir error:

```bash
comando 2> errores.txt
```

## 14. Pipes

El operador `|` conecta la salida de un comando con la entrada del siguiente.

```bash
cat archivo.txt | grep "hola"
ls -l | grep ".txt"
cat archivo.txt | wc -l
cat archivo.txt | sort
```

La idea del pipe es central en Unix:

```text
salida de un programa -> entrada de otro programa
```

En vez de escribir programas gigantes, se combinan herramientas pequenas.

## 15. `grep`

`grep` busca lineas que coinciden con un patron.

```bash
grep "hola" ejemplo.txt
grep "hola" archivo1 | grep "busqueda2"
grep -l "palabra" ./*
```

Sirve para:

- buscar texto en archivos;
- filtrar salida de otros comandos;
- detectar lineas relevantes.

## 16. `cat` y usos frecuentes

`cat` sirve para mostrar o concatenar archivos.

```bash
cat archivo.txt
cat archivo1.txt archivo2.txt > combinado.txt
cat archivo_original.txt > copia_archivo.txt
```

Tambien se puede usar para escribir interactivamente:

```bash
cat > notas.txt
```

Luego escribis lineas y cerras con `Ctrl+D`.

## 17. Permisos

Cada archivo tiene permisos para:

- owner;
- group;
- others.

Y cada permiso puede ser:

- `r`: read;
- `w`: write;
- `x`: execute.

Ejemplo:

```text
-rwxr-xr--
```

Lectura:

- owner: `rwx`
- group: `r-x`
- others: `r--`

### `chmod`

```bash
chmod +x script.sh
chmod 755 script.sh
chmod 644 archivo.txt
```

### `chown`

```bash
sudo chown usuario archivo.txt
```

En un script, dar permiso de ejecucion es habitual:

```bash
chmod +x mi_script.sh
```

## 18. Bash como lenguaje de scripting

Un script es un archivo de texto con comandos Bash.

Suele empezar con:

```bash
#!/bin/bash
```

Eso se llama shebang y le dice al sistema con que interprete ejecutar el archivo.

Ejemplo minimo:

```bash
#!/bin/bash
echo "Hola desde un script"
```

Para ejecutarlo:

```bash
chmod +x script.sh
./script.sh
```

Tambien se puede correr asi:

```bash
bash script.sh
```

## 19. Leer datos del usuario

Para pedir input se usa `read`.

```bash
echo "Ingresa tu nombre:"
read nombre
echo "Hola, $nombre"
```

La idea es:

- mostrar un mensaje;
- guardar lo escrito por el usuario;
- reutilizarlo despues.

## 20. Condicionales

### `if`

```bash
if [ "$edad" -ge 18 ]; then
  echo "Es mayor de edad"
else
  echo "Es menor de edad"
fi
```

En Bash, la sintaxis importa mucho:

- los espacios dentro de `[` y `]` importan;
- `then` abre el bloque;
- `fi` lo cierra.

### Comparaciones numericas

- `-eq`: igual
- `-ne`: distinto
- `-gt`: mayor que
- `-lt`: menor que
- `-ge`: mayor o igual
- `-le`: menor o igual

### Comparaciones de cadenas

- `=` o `==`: igualdad
- `!=`: desigualdad
- `-z`: cadena vacia
- `-n`: cadena no vacia

## 21. Bucles

### `for`

```bash
for archivo in *.txt; do
  echo "$archivo"
done
```

Recorre una secuencia de elementos.

### `while`

```bash
contador=1

while [ "$contador" -le 5 ]; do
  echo "$contador"
  contador=$((contador + 1))
done
```

Se ejecuta mientras la condicion sea verdadera.

### `case`

```bash
case "$opcion" in
  iniciar)
    echo "Inicio"
    ;;
  salir)
    echo "Salida"
    ;;
  *)
    echo "Opcion invalida"
    ;;
esac
```

Es util cuando una variable puede tomar varias opciones discretas.

## 22. Operaciones aritmeticas

```bash
numero=5
resultado=$((numero + 3))
echo "$resultado"
```

Tambien existen comparaciones y expresiones dentro de `(( ))`.

## 23. Arrays

Bash tiene arrays simples.

```bash
frutas=("manzana" "pera" "uva")
echo "${frutas[0]}"
echo "${frutas[@]}"
```

No es un sistema de estructuras tan rico como en otros lenguajes, pero alcanza para muchos scripts sencillos.

## 24. Funciones

```bash
saludar() {
  echo "Hola, $1"
}

saludar "Ana"
```

Sirven para:

- evitar repetir codigo;
- separar tareas;
- hacer el script mas legible.

## 25. Codigos de salida

En Unix los programas suelen devolver:

- `0` si salio bien;
- otro numero si hubo error.

Se puede consultar con:

```bash
echo $?
```

Esto es importante cuando un script decide que hacer segun si otro comando funciono o no.

## 26. Idea mental correcta sobre Bash

Bash no se estudia solo como "lenguaje". Tambien se estudia como entorno de trabajo.

Hay que pensar en Bash como una combinacion de:

- comandos del sistema;
- expansion de texto;
- redireccion;
- composicion mediante pipes;
- y automatizacion con scripts.

## 27. Errores tipicos de principiante

- olvidar que en Bash la sintaxis de espacios importa;
- usar variables con espacios alrededor del `=`;
- confundir terminal con shell;
- olvidar comillas en cadenas con espacios;
- usar `rm -r` sin revisar bien la ruta;
- escribir bloques `if` o `for` sin `fi` o `done`;
- creer que `stdout` y `stderr` son lo mismo.

## 28. Resumen final

Las ideas mas importantes del tema son:

- Bash es shell y lenguaje de scripting;
- la terminal no es lo mismo que el shell;
- los comandos se pueden encadenar con pipes;
- la salida se puede redirigir;
- las variables usan expansion con `$`;
- los scripts pueden recibir parametros;
- `if`, `for`, `while` y `case` permiten controlar el flujo;
- permisos, rutas y archivos forman parte del trabajo normal.

## 29. Mini ejemplo integrador

```bash
#!/bin/bash

if [ "$#" -lt 1 ]; then
  echo "Uso: $0 <archivo>"
  exit 1
fi

archivo="$1"

if [ ! -f "$archivo" ]; then
  echo "Error: no existe el archivo $archivo"
  exit 1
fi

echo "Primeras 5 lineas:"
head -n 5 "$archivo"
echo "Cantidad de lineas con hola:"
grep -c "hola" "$archivo"
```

Este ejemplo junta varias ideas:

- parametros;
- validacion;
- condicionales;
- uso de comandos del sistema;
- y salida util para el usuario.


