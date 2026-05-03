
> **Idea:** entender Linux no es aprender comandos sueltos, sino entender el sistema sobre el que despues corren Bash, Docker, servidores y muchas herramientas de desarrollo.

## Keywords a saber

`kernel`, `distro`, `GNU/Linux`, `Unix-like`, `filesystem`, `shell`, `terminal`, `permisos`, `rutas absolutas`, `rutas relativas`, `root`, `WSL2`, `dual-boot`, `maquina virtual`

> **Para estudiar:** si una keyword no te queda clara, intenta responder esta pregunta: `habla del sistema, de su estructura o de la forma en que yo interactuo con el?`

## Definiciones rapidas

La idea de esta tabla es que cada palabra te ayude a armar una imagen mental del sistema, no que quede como vocabulario aislado.

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `kernel` | Nucleo del sistema operativo que administra hardware, procesos y memoria. | No es "todo Linux". Es la capa central que media entre programas y maquina. Si el sistema fuera una empresa, seria la parte que coordina recursos y decide quien usa que. |
| `distro` | Distribucion: sistema completo armado alrededor del kernel Linux. | Cuando instalas Ubuntu o Debian, no instalas solo el kernel: instalas un sistema usable con paquetes, shell, herramientas y convenciones. |
| `GNU/Linux` | Forma de remarcar que el sistema incluye kernel Linux mas herramientas GNU. | Sirve para no confundir "el nucleo" con "el sistema completo que usa una persona real". |
| `Unix-like` | Sistema que se comporta de forma parecida a Unix aunque no sea Unix original. | Lo importante no es la copia exacta, sino que comparte ideas como permisos, jerarquia de archivos y uso fuerte de shell. |
| `filesystem` | Forma en que el sistema organiza archivos, directorios y rutas. | No es solo "donde estan los archivos": define una estructura mental de navegacion y ubicacion de recursos. |
| `shell` | Programa que interpreta comandos y permite interactuar con el sistema. | Es el intermediario textual entre vos y el sistema operativo. Vos escribis una orden; el shell decide como interpretarla y ejecutarla. |
| `terminal` | Interfaz donde escribis comandos y ves resultados del shell. | La terminal es la ventana; el shell es el interprete que trabaja dentro de ella. Mezclarlos es un error muy comun al empezar. |
| `permisos` | Reglas que indican quien puede leer, escribir o ejecutar archivos. | Son clave porque Linux esta pensado para varios usuarios y procesos. No todo el mundo puede hacer todo sobre cualquier archivo. |
| `rutas absolutas` | Caminos que indican la ubicacion completa desde la raiz del sistema. | Funcionan como una direccion completa: no dependen de donde estes parado en ese momento. |
| `rutas relativas` | Caminos expresados respecto del directorio actual. | Son mas comodas para moverte localmente, pero solo tienen sentido si sabes desde donde estas trabajando. |
| `root` | Usuario administrador o raiz del filesystem segun el contexto. | Puede significar dos cosas distintas: el usuario con maximos privilegios o la carpeta `/` desde la que cuelga todo el arbol. |
| `WSL2` | Subsistema de Windows que permite correr Linux con integracion fuerte. | Es util porque acerca mucho la experiencia Linux sin obligarte a cambiar por completo de sistema operativo. |
| `dual-boot` | Instalacion de dos sistemas operativos para elegir al arrancar la maquina. | Da una experiencia nativa real, pero implica tocar el arranque y particionado del disco. |
| `maquina virtual` | Sistema invitado que corre dentro de otro usando virtualizacion. | Sirve para probar Linux sin modificar demasiado la maquina principal, a cambio de gastar mas recursos. |

## Tabla comparativa rapida

| Concepto | Que es | Ejemplo de uso |
| --- | --- | --- |
| `Linux` | El kernel o, en uso cotidiano, el sistema basado en ese kernel | administrar procesos y hardware |
| `distro` | El sistema completo listo para usar | Ubuntu, Debian, Fedora |
| `GNU/Linux` | Forma mas precisa de nombrar al sistema completo | destacar que no es solo el kernel |

## Mapa mental rapido

Para no perderte, pensa este tema asi:

```text
Linux no es solo una pantalla negra con comandos
-> primero existe un sistema
-> dentro del sistema hay una forma de organizar archivos y permisos
-> y vos interactuas con eso a traves de shell y terminal
```

Si esa cadena se entiende, el resto del tema deja de verse como terminos desconectados.

## Lo que mas se suele confundir

- `Linux` no es exactamente lo mismo que una `distro`: Linux es el kernel, mientras que Ubuntu o Debian son sistemas completos armados alrededor de ese kernel.
- `terminal` no es lo mismo que `shell`: la terminal muestra la interfaz, mientras que el shell interpreta lo que escribis.
- `root` puede referirse al usuario administrador o a la raiz del arbol de archivos `/`; el contexto decide cual de los dos sentidos aplica.

## Como leer este apunte

Este archivo conserva la amplitud del material largo, pero ordena mejor los temas para que Linux no aparezca como una lista suelta de definiciones.

La idea central es entender:

- que es Linux;
- por que se estudia;
- como se usa;
- y como se conecta con terminal, filesystem, permisos y herramientas de desarrollo.

## 1. Que es Linux

Cuando en la vida cotidiana se dice "Linux", muchas veces se habla del sistema completo.

Pero tecnicamente, Linux es el kernel.

Eso significa que Linux es el nucleo que:

- administra procesos;
- maneja memoria;
- se comunica con el hardware;
- organiza dispositivos, discos y red.

Sobre ese nucleo se montan otras piezas:

- shell;
- herramientas del sistema;
- bibliotecas;
- gestores de paquetes;
- entorno grafico;
- aplicaciones.

## 2. Linux y distribuciones

Una distribucion o distro es un sistema armado alrededor del kernel Linux.

Ejemplos comunes:

- Ubuntu;
- Debian;
- Fedora;
- Arch.

Entonces:

- Linux = kernel;
- distro = sistema completo construido alrededor de ese kernel.

## 3. Antecedentes: Unix y GNU

### Unix

Es un sistema historico que inspiro gran parte del modelo que despues heredaron Linux y otros sistemas Unix-like.

### GNU

Es un proyecto de software libre que aporto muchas herramientas esenciales, como:

- Bash;
- GCC;
- GDB;
- Emacs.

Por eso a veces aparece la expresion `GNU/Linux`: intenta remarcar que el sistema usable no depende solo del kernel, sino tambien de muchas herramientas de GNU.

## 4. Por que importa Linux

Linux esta en muchisimos lugares:

- servidores;
- cloud;
- supercomputadoras;
- Android;
- sistemas embebidos;
- herramientas de desarrollo;
- infraestructura web.

En la materia se estudia porque ordena muchos otros temas:

- terminal;
- Bash;
- permisos;
- Docker;
- despliegue;
- trabajo tecnico en entornos reales.

## 5. Opciones de instalacion

### Instalacion nativa o dual-boot

Te permite tener Linux instalado junto con otro sistema operativo en la misma maquina.

Ventajas:

- rendimiento real;
- acceso directo al hardware;
- experiencia completa.

Costo:

- es mas invasivo;
- hay que tocar particiones y arranque.

### Maquina virtual

Permite correr Linux dentro de otro sistema.

Ventajas:

- facil para probar;
- casi no toca el sistema principal.

Costo:

- mas consumo de recursos;
- entorno menos comodo para uso intenso.

### Contenedores

Sirven para experimentar entornos Linux aislados sin instalar una distro completa.

Ventajas:

- livianos;
- rapidos;
- muy utiles para desarrollo puntual.

Limite:

- no reemplazan toda la experiencia de un sistema Linux real.

### WSL2

En Windows, WSL2 es un punto medio muy util:

- permite usar herramientas Linux;
- integra bien con Docker;
- evita migrar por completo de sistema.

## 6. Sistema Unix-like

Decir que Linux es Unix-like significa que comparte ideas fundamentales con Unix.

### Estructura de archivos

Todo se organiza como un arbol cuyo origen es `/`.

```text
/
|-- home/
|-- etc/
|-- var/
|-- tmp/
|-- usr/
`-- bin/
```

Eso implica que:

- no hay letras de unidad como eje principal;
- todo cuelga de una sola jerarquia;
- los recursos se montan dentro del arbol.

### Rutas absolutas y relativas

- absoluta: empieza en `/`;
- relativa: parte desde el directorio actual;
- `.`: directorio actual;
- `..`: directorio padre.

### Multitarea y multiusuario

Linux puede manejar:

- varios procesos al mismo tiempo;
- varios usuarios con permisos distintos.

### Permisos

Controla quien puede:

- leer;
- escribir;
- ejecutar.

### POSIX

Muchos sistemas Unix-like siguen el estandar POSIX para comportarse de manera compatible en varias herramientas y programas.

## 7. Shell y linea de comandos

La linea de comandos es una forma de interactuar con el sistema por texto.

El shell es el programa que interpreta lo que escribis.

Ejemplo clasico:

```text
escribis un comando -> el shell lo interpreta -> el sistema lo ejecuta
```

En muchas distros el shell mas comun es Bash.

## 8. Emulador de terminal y prompt

Cuando usas interfaz grafica, lo normal es abrir un emulador de terminal.

Ese programa muestra el shell y deja escribir comandos.

Prompt tipico:

```text
usuario@maquina:~$
```

Lectura:

- usuario;
- maquina;
- directorio actual;
- `$` como usuario comun;
- `#` como root.

## 9. Texto puro

Este concepto es importante porque gran parte del ecosistema tecnico trabaja asi.

Texto puro significa:

- solo caracteres;
- sin formato visual extra;
- facil de leer y procesar por programas.

Eso importa porque:

- los archivos de configuracion suelen ser texto puro;
- los scripts tambien;
- muchas herramientas de Linux estan hechas para leer y producir texto.

## 10. Comandos basicos

Los mas importantes para empezar:

```bash
ls
pwd
cd
cp
mv
rm
mkdir
man
touch
chmod
cat
less
tail
head
grep
wc
find
```

No hace falta memorizarlos todos de golpe. Lo importante es entender que se repiten en flujos reales:

1. te ubicas con `pwd`;
2. inspeccionas con `ls`;
3. te moves con `cd`;
4. creas o modificas archivos;
5. lees o filtras informacion con herramientas de texto.

## 11. Permisos y usuarios

Linux toma muy en serio los permisos.

Eso significa que no cualquier usuario puede hacer cualquier cosa.

Hay permisos para:

- propietario;
- grupo;
- otros.

Y tipos de permiso:

- lectura;
- escritura;
- ejecucion.

Eso protege archivos del sistema y ordena el trabajo multiusuario.

## 12. Por que la terminal sigue siendo tan importante

Porque muchas tareas tecnicas son mas claras, repetibles y automatizables por linea de comandos.

Ejemplos:

- administrar servidores;
- trabajar con Git;
- correr scripts;
- usar Docker;
- revisar logs;
- manipular muchos archivos.

La terminal no es "una forma vieja". Es una interfaz muy potente para trabajo tecnico.

## 13. Que conviene no confundir

### Linux no es solo "otra interfaz"

No es una skin ni una app. Es un sistema completo construido alrededor de un kernel.

### Shell no es terminal

- terminal: la ventana;
- shell: el interprete.

### Kernel no es distro

- kernel: Linux;
- distro: Ubuntu, Debian, Fedora, etc.

## 14. Resumen final

Las ideas centrales del tema son:

- Linux es el kernel;
- una distro es el sistema completo;
- hereda ideas de Unix;
- organiza archivos como un arbol con raiz `/`;
- usa shell y terminal para interactuar;
- trabaja mucho con texto puro;
- da gran importancia a permisos, usuarios y herramientas de linea de comandos.
