
> **Idea:** este apunte explica que pasa dentro de Bash antes de que un comando se ejecute, por eso es mas conceptual que una guia de comandos.

## Keywords a saber

`prompt`, `expansiones`, `wildcards`, `cat`, `grep`, `read`, `parametros`, `arrays`, `funciones`, `codigo de salida`, `expansion de variables`, `sustitucion de comandos`

> **Para estudiar:** si algo parece "magico" en Bash, casi siempre esta relacionado con expansiones, sustituciones o codigos de salida.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `prompt` | Texto que muestra el shell para indicar que espera un comando. | No es decoracion nomas: suele darte pistas sobre usuario, carpeta actual o contexto de trabajo. |
| `expansiones` | Transformaciones que Bash hace antes de ejecutar un comando. | Bash no siempre toma lo que escribis de forma literal; primero resuelve variables, patrones y sustituciones. |
| `wildcards` | Patrones como `*` o `?` para matchear nombres de archivos. | Son utiles para trabajar con muchos archivos a la vez sin escribir cada nombre manualmente. |
| `cat` | Comando para mostrar o concatenar contenido de archivos. | Aunque es simple, sirve mucho para inspeccionar rapido texto plano o encadenarlo con otros comandos. |
| `grep` | Comando para buscar lineas que coincidan con un patron. | Es una herramienta de filtrado: de mucha salida, se queda con la parte que cumple una condicion. |
| `read` | Builtin que lee entrada y la guarda en variables. | Permite que un script deje de ser totalmente fijo y empiece a interactuar con el usuario. |
| `parametros` | Valores que recibe un script o funcion al ejecutarse. | Hacen que un mismo script sirva para distintos casos sin tener que reescribirlo. |
| `arrays` | Estructuras que guardan varios valores bajo un mismo nombre. | Son utiles cuando una sola variable no alcanza porque queres trabajar con una lista ordenada de elementos. |
| `funciones` | Bloques reutilizables de comandos con nombre propio. | Ayudan a no repetir codigo y a separar tareas dentro de un script mas largo. |
| `codigo de salida` | Numero que indica si un comando termino bien o con error. | Bash toma muy en serio ese codigo porque lo usa para decidir si continua, falla o entra en otra rama logica. |
| `expansion de variables` | Reemplazo de una referencia como `$HOME` por su valor. | Lo que parece un texto corto en realidad puede convertirse en una ruta, numero o string completo antes de ejecutarse. |
| `sustitucion de comandos` | Reemplazo de `$(comando)` por la salida de ese comando. | Permite usar el resultado de un comando como si fuera un dato dentro de otro comando. |

## Tabla comparativa rapida

| Mecanismo | Sobre que opera | Ejemplo |
| --- | --- | --- |
| `wildcards` | Nombres de archivos | `*.txt` |
| `expansion de variables` | Valores guardados | `$HOME` |
| `sustitucion de comandos` | Salida de otro comando | `$(pwd)` |

## Mapa mental rapido

Este apunte muestra el "interior" de Bash:

```text
vos escribis algo
-> Bash lo expande e interpreta
-> decide con que valores reales trabajar
-> ejecuta el comando
-> y devuelve un codigo de salida para indicar como termino
```

Por eso este tema es mas profundo que aprender comandos sueltos: explica que pasa antes y despues de cada ejecucion.

## Lo que mas se suele confundir

- `wildcards` no son lo mismo que `regex`: las wildcards expanden nombres de archivos; las regex describen patrones textuales.
- `expansion de variables` y `sustitucion de comandos` tampoco son iguales: una reemplaza un valor guardado y la otra reemplaza la salida de un comando.
- en Bash, `0` como codigo de salida significa exito; muchos principiantes asumen al reves porque piensan en cero como "nada".

## Como leer este apunte

Este archivo unifica dos cosas:

- la profundidad y los temas amplios del material largo de la pagina;
- la claridad y las explicaciones puente del resumen de `Slides`.

La idea es que sirva tanto para estudiar teoria como para entender que hace cada comando cuando lo ves por primera vez.

## Indice

1. Que es Bash
2. Terminal, shell y prompt
3. Navegacion del sistema
4. Trabajo con archivos
5. Permisos
6. Entrada, salida y errores
7. Pipes y operadores de control
8. Variables
9. Scripts
10. Condicionales y comparaciones
11. Aritmetica
12. Arrays
13. Parentesis, llaves y corchetes
14. Loops y funciones
15. Input del usuario
16. Comandos utiles
17. Ejercicios practicos

## 1. Que es Bash

Bash significa `Bourne Again Shell`. Es un shell, o sea, un programa que interpreta los comandos que escribis y decide que ejecutar.

Conviene separar tres conceptos:

- terminal: la ventana o programa donde escribis;
- shell: el interprete que entiende el comando;
- comando: la instruccion puntual que queres ejecutar.

Ejemplo mental:

```text
Windows Terminal -> Bash -> ls
```

La terminal es el medio. Bash es quien interpreta. `ls` es el comando.

### Historia minima

- `1977`: aparece `sh` o Bourne Shell.
- `1978`: aparece `csh`.
- `1983`: aparece `ksh`.
- `1989`: el proyecto GNU crea `Bash`.

La gracia del nombre es doble:

- es un sucesor del Bourne Shell;
- y suena como "born again", es decir, "renacido".

### Por que se usa tanto

- es el shell clasico en Linux;
- permite automatizar tareas del sistema;
- funciona muy bien para scripts cortos;
- aparece todo el tiempo en servidores, Docker, deploys y herramientas de desarrollo.

### Bash como lenguaje

Bash es un lenguaje procedural o imperativo. Eso significa que le decis a la computadora que pasos ejecutar y en que orden.

En Bash aparecen:

- comandos en secuencia;
- variables;
- condicionales;
- loops;
- funciones;
- arrays.

Tambien tiene limites:

- no esta pensado para logica grande;
- el manejo de errores es mas rustico;
- no tiene estructuras tan ricas como Python;
- mantener scripts largos se vuelve incomodo.

Regla practica:

- Bash para automatizar comandos y glue code;
- Python u otro lenguaje cuando la logica empieza a crecer demasiado.

## 2. Terminal, shell y prompt

### Que muestra el prompt

Un prompt comun puede verse asi:

```text
usuario@computadora:~/carpeta$
```

Cada parte te dice algo:

- `usuario`: quien esta usando la sesion;
- `computadora`: nombre de la maquina;
- `~/carpeta`: directorio actual;
- `$`: usuario comun.

Si aparece `#`, generalmente estas como `root`.

### Atajos utiles

| Atajo | Funcion |
| --- | --- |
| `Tab` | Autocompleta |
| `Up` / `Down` | Recorre historial |
| `Ctrl + C` | Cancela el comando actual |
| `Ctrl + D` | EOF o cierre de sesion |
| `Ctrl + L` | Limpia pantalla |
| `Ctrl + A` | Va al inicio de la linea |
| `Ctrl + E` | Va al final de la linea |
| `Ctrl + U` | Borra hasta el inicio |
| `Ctrl + K` | Borra hasta el final |
| `Ctrl + R` | Busca en el historial |

### Ejemplo practico de autocompletado

```bash

> **Idea fuerza:** este apunte explica que pasa dentro de Bash antes de que un comando se ejecute, por eso es mas conceptual que una guia de comandos.
his[Tab]

> **Idea fuerza:** este apunte explica que pasa dentro de Bash antes de que un comando se ejecute, por eso es mas conceptual que una guia de comandos.
history

cd /ho[Tab]

> **Idea fuerza:** este apunte explica que pasa dentro de Bash antes de que un comando se ejecute, por eso es mas conceptual que una guia de comandos.
cd /home/
```

## 3. Navegacion del sistema

Linux organiza todo en un arbol que parte de `/`.

```text
/
|-- home/
|   `-- tu_usuario/
|       |-- Documentos/
|       |-- Descargas/
|       `-- ...
|-- etc/
|-- var/
|-- tmp/
|-- usr/
`-- bin/
```

### Rutas

- absoluta: empieza en `/`;
- relativa: depende de donde estas parado;
- `.`: directorio actual;
- `..`: directorio padre;
- `~`: home del usuario.

### Comandos de navegacion

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

### Que hace cada uno

- `pwd`: muestra donde estas;
- `ls`: lista contenido;
- `ls -la`: lista con detalles y ocultos;
- `cd ruta`: cambia de directorio;
- `cd -`: vuelve al directorio anterior.

### Ejemplo

```bash
pwd
/home/usuario/Documentos

ls -la

cd ~
mkdir practica_bash
cd practica_bash
pwd
```

## 4. Trabajo con archivos

### Crear

```bash
mkdir nueva_carpeta
mkdir -p carpeta/subcarpeta/otra
touch archivo.txt
touch archivo1.txt archivo2.txt
```

### Leer

```bash
cat archivo.txt
less archivo_largo.txt
head archivo.txt
head -n 5 archivo.txt
tail archivo.txt
tail -n 20 archivo.txt
tail -f /var/log/syslog
```

`less` sirve para archivos largos. Te moves con:

- `Space` o `f`: pagina siguiente;
- `b`: pagina anterior;
- `g`: inicio;
- `G`: final;
- `/texto`: buscar;
- `q`: salir.

### Copiar, mover y borrar

```bash
cp origen.txt destino.txt
cp archivo.txt carpeta/
cp -r carpeta/ carpeta_backup/
cp -a origen destino

mv archivo.txt carpeta/
mv nombre_viejo.txt nombre_nuevo.txt
mv archivo1.txt archivo2.txt carpeta/

rm archivo.txt
rm -i archivo.txt
rmdir carpeta_vacia/
rm -r carpeta/
rm -rf carpeta/
```

`rm` no manda nada a la papelera. Hay que usarlo con cuidado.

### Wildcards

```bash
ls *.txt
rm *.log
cp *.jpg *.png fotos/
ls archivo?.txt
ls [a-z]*.txt
ls archivo[!0-9].txt
```

## 5. Permisos

Cada archivo tiene permisos para:

- owner;
- group;
- others.

Y cada grupo puede tener:

- `r`: read;
- `w`: write;
- `x`: execute.

Ejemplo:

```text
-rwxr-xr--
```

Lectura:

- owner: `rwx`;
- group: `r-x`;
- others: `r--`.

### Notacion numerica

| Permiso | Valor |
| --- | --- |
| `r` | 4 |
| `w` | 2 |
| `x` | 1 |

Ejemplos comunes:

- `755` = `rwxr-xr-x`
- `644` = `rw-r--r--`
- `600` = `rw-------`

### Comandos

```bash
chmod +x script.sh
chmod 755 script.sh
chmod 644 archivo.txt
chmod -R 755 carpeta/

sudo chown usuario archivo.txt
sudo chown usuario:grupo archivo.txt
sudo chown -R usuario:grupo carpeta/
```

## 6. Entrada, salida y errores

Todo proceso suele trabajar con tres flujos:

- `stdin` (`0`): entrada;
- `stdout` (`1`): salida normal;
- `stderr` (`2`): errores.

Esto explica por que se puede redirigir cada cosa por separado.

```bash
comando > salida.txt
comando >> salida.txt
comando < entrada.txt
comando 2> errores.txt
comando > todo.txt 2>&1
comando &> todo.txt
```

### Ejemplos

```bash
cat < archivo.txt
ls > lista.txt
ls /carpeta_inexistente 2> errores.txt
find / -name "*.conf" > resultados.txt 2> /dev/null
```

`/dev/null` es un "agujero negro": todo lo que envies ahi se descarta.

## 7. Pipes y operadores de control

### Pipes

El pipe `|` conecta la salida de un comando con la entrada del siguiente.

```bash
history | grep "git"
ls -la | grep ".txt"
cat archivo.txt | wc -w
ps aux | grep usuario
cut -d',' -f2 datos.csv | sort | uniq -c | sort -rn
```

### Operadores de control

No hay que confundir pipe con operadores de ejecucion.

```bash
mkdir carpeta && cd carpeta
ping -c1 google.com || echo "Sin conexion"
echo "Inicio"; comando_que_falla; echo "Fin"
```

Resumen:

- `|`: pasa datos entre comandos;
- `&&`: ejecuta lo siguiente si lo anterior salio bien;
- `||`: ejecuta lo siguiente si lo anterior fallo;
- `;`: ejecuta en secuencia siempre.

## 8. Variables

```bash
nombre="Juan"
edad=25
echo "$nombre"
echo "$edad"
```

Tambien podes capturar la salida de un comando:

```bash
usuario=$(whoami)
fecha=$(date)
echo "$usuario"
echo "$fecha"
```

### Variables comunes de entorno

```bash
echo $HOME
echo $USER
echo $PWD
echo $PATH
echo $SHELL
```

### Regla importante

En una asignacion no hay espacios alrededor de `=`.

Correcto:

```bash
nombre="Juan"
```

Incorrecto:

```bash
nombre = "Juan"
```

## 9. Scripts

```bash
#!/bin/bash
echo "Hola mundo"
echo "Usuario: $USER"
echo "Fecha: $(date)"
echo "Estas en: $(pwd)"
```

Para ejecutarlo:

```bash
chmod +x hola.sh
./hola.sh
```

La primera linea es el `shebang`: indica con que interprete correr el archivo.

## 10. Condicionales y comparaciones

### Strings vs numeros

Para texto:

```bash
[ "$nombre" = "Juan" ]
[ "$nombre" != "Pedro" ]
```

Para numeros:

```bash
[ "$edad" -eq 25 ]
[ "$edad" -gt 18 ]
[ "$edad" -le 30 ]
```

### Por que no usar `>` y `<` para numeros

Porque en Bash esos simbolos suelen usarse para redireccion.

### Condicionales

```bash
if [ -f "archivo.txt" ]; then
  echo "El archivo existe"
fi

if [ "$USER" = "root" ]; then
  echo "Sos root"
else
  echo "No sos root"
fi

if [ "$edad" -lt 18 ]; then
  echo "Menor de edad"
elif [ "$edad" -lt 65 ]; then
  echo "Adulto"
else
  echo "Jubilado"
fi
```

### Tests comunes sobre archivos

```bash
[ -f "archivo" ]   # existe y es archivo
[ -d "carpeta" ]   # existe y es directorio
[ -e "algo" ]      # existe
[ -r "archivo" ]   # lectura
[ -w "archivo" ]   # escritura
[ -x "archivo" ]   # ejecucion
[ -s "archivo" ]   # no esta vacio
```

## 11. Aritmetica

La forma mas usada es:

```bash
resultado=$((5 + 3))
echo $resultado
```

Con variables:

```bash
a=10
b=3
suma=$((a + b))
resta=$((a - b))
multiplicacion=$((a * b))
division=$((a / b))
resto=$((a % b))
```

Tambien existe:

```bash
let "resultado = 5 + 3"
resultado=$(expr 5 + 3)
```

Bash trabaja naturalmente con enteros. Para decimales suele apoyarse en herramientas externas como `bc`.

## 12. Arrays

### Crear arrays

```bash
frutas=("manzana" "banana" "naranja")
colores[0]="rojo"
colores[1]="verde"
colores[2]="azul"
```

### Acceder

```bash
echo ${frutas[0]}
echo ${frutas[1]}
echo ${frutas[@]}
echo ${#frutas[@]}
echo ${!frutas[@]}
```

### Modificar

```bash
frutas+=("pera")
unset frutas[1]
```

### Arrays asociativos

```bash
declare -A telefonos
telefonos[ana]="1234"
telefonos[juan]="5678"
echo ${telefonos[ana]}
```

## 13. Parentesis, llaves y corchetes

Este tema aparece mucho y suele confundir porque simbolos parecidos hacen cosas distintas.

### `( )`

Se usan, entre otras cosas, para subshells o para declarar arrays.

```bash
(cd /tmp && ls)
frutas=("manzana" "banana")
```

### `(( ))`

Se usan para evaluacion aritmetica.

```bash
((resultado = 5 + 3))
((contador++))
((edad >= 18)) && echo "Mayor de edad"
```

### `[ ]`

Es el test clasico.

```bash
[ "$nombre" = "Juan" ]
[ -f archivo.txt ]
```

### `[[ ]]`

Es un test extendido de Bash, mas comodo y seguro en varios casos.

```bash
[[ $nombre == J* ]]
[[ $texto =~ ^[0-9]+$ ]]
```

### `{ }`

Se usan para agrupar comandos o para expansion de llaves.

```bash
{ echo "uno"; echo "dos"; }
mkdir -p proyecto/{src,docs,tests}
```

## 14. Loops y funciones

### `for`

```bash
for archivo in *.txt; do
  echo "$archivo"
done
```

### `while`

```bash
contador=0
while [ $contador -lt 3 ]; do
  echo $contador
  contador=$((contador + 1))
done
```

### `case`

```bash
case "$opcion" in
  1) echo "Elegiste uno" ;;
  2) echo "Elegiste dos" ;;
  *) echo "Opcion invalida" ;;
esac
```

### Funciones

```bash
saludar() {
  echo "Hola, $1"
}

saludar "Ana"
```

## 15. Input del usuario

```bash
read nombre
echo "Hola, $nombre"
```

Con mensaje:

```bash
read -p "Ingresa tu nombre: " nombre
echo "Hola, $nombre"
```

## 16. Comandos utiles

Los que mas se repiten en esta unidad:

- `pwd`
- `ls`
- `cd`
- `mkdir`
- `touch`
- `cat`
- `less`
- `head`
- `tail`
- `cp`
- `mv`
- `rm`
- `chmod`
- `chown`
- `grep`
- `sort`
- `uniq`
- `wc`
- `history`
- `find`

## 17. Ejercicios practicos

### Navegacion

```bash
pwd
ls -la
cd ~
mkdir practica_bash
cd practica_bash
pwd
```

### Archivos

```bash
mkdir -p proyecto/{src,docs,tests}
touch proyecto/src/main.py
touch proyecto/src/utils.py
touch proyecto/docs/readme.md
touch proyecto/tests/test_main.py
ls -R proyecto/
cp proyecto/src/*.py proyecto/backup/
mv proyecto/docs/readme.md proyecto/docs/README.md
rm -r proyecto/tests/
```

### Permisos

```bash
echo '#!/bin/bash' > saludo.sh
echo 'echo "Hola!"' >> saludo.sh
ls -l saludo.sh
chmod +x saludo.sh
./saludo.sh
```

### Variables y script basico

```bash
#!/bin/bash
nombre="Mundo"
echo "Hola, $nombre"
```

### Regla final

Si te perdes al leer un comando, preguntate:

1. de donde lee;
2. que ejecuta;
3. a donde escribe;
4. sobre que archivos o rutas trabaja.

Esa forma de leer Bash ordena casi todo el tema.


