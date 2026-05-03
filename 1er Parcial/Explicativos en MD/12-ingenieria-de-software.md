
> **Idea:** este tema explica por que construir software bien no es solo programar, sino organizar un proceso completo con criterio de calidad.

## Keywords a saber

`software`, `ingenieria`, `IEEE 729`, `requerimientos`, `diseno`, `implementacion`, `testing`, `validacion`, `despliegue`, `mantenimiento`, `calidad`, `usabilidad`, `seguridad`

> **Para estudiar:** trata de responder cada keyword con una pregunta de proceso: `que problema resuelve esta etapa o este concepto?`

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `software` | Conjunto de programas, reglas, datos y documentacion de un sistema. | Esto importa porque rompe la idea reducida de que software = solo codigo fuente. Tambien incluye reglas de uso, datos y soporte documental. |
| `ingenieria` | Aplicacion de conocimientos para resolver problemas reales con metodo. | La palabra clave es metodo: no alcanza con improvisar una solucion que ande "mas o menos". |
| `IEEE 729` | Estandar citado para definir software de forma mas completa que "codigo". | Sirve como respaldo formal para una definicion mas rica y menos intuitiva pero mas correcta. |
| `requerimientos` | Necesidades y condiciones que el sistema debe satisfacer. | Son el puente entre el problema del mundo real y lo que despues se construye tecnicamente. |
| `diseno` | Etapa en la que se define como se organizara la solucion. | No escribe codigo todavia, pero decide estructura, responsabilidades y arquitectura. |
| `implementacion` | Construccion concreta del sistema mediante codigo. | Es donde la idea se vuelve producto funcional, pero no deberia arrancar sin requerimientos y diseno previos razonables. |
| `testing` | Conjunto de pruebas para detectar problemas y revisar comportamiento. | Hace visible si el sistema realmente se comporta como esperamos, no solo si "compila". |
| `validacion` | Comprobacion de que el producto satisface lo que el cliente necesita. | La pregunta central es: hicimos el producto correcto para este problema? |
| `despliegue` | Paso del software hacia entornos donde queda disponible para uso real. | No es un detalle final menor: cambia el contexto, el riesgo y el publico del sistema. |
| `mantenimiento` | Correccion, mejora y adaptacion del software en el tiempo. | En la practica real, suele consumir muchisimo esfuerzo. El software rara vez termina al primer release. |
| `calidad` | Medida de que tan correcto, util y sostenible resulta el software. | No es una sola propiedad; mezcla funcionalidad, seguridad, rendimiento, claridad y otras dimensiones. |
| `usabilidad` | Facilidad con la que una persona puede entender y usar el sistema. | Un sistema puede funcionar tecnicamente y aun asi ser malo si el usuario no logra usarlo bien. |
| `seguridad` | Capacidad del sistema para proteger datos, accesos y operaciones. | En muchos contextos no es opcional ni "extra": define si el sistema es aceptable o no. |

## Tabla comparativa rapida

| Concepto | Pregunta que responde | Ejemplo |
| --- | --- | --- |
| `requerimiento funcional` | que debe hacer el sistema | registrar usuarios |
| `requerimiento no funcional` | como debe comportarse | responder en menos de 2 segundos |
| `validacion` | hicimos el producto correcto | satisface al usuario |
| `verificacion` | lo hicimos correctamente | no falla al ejecutar |

## Mapa mental rapido

La materia se entiende mejor si la pensas como un recorrido:

```text
primero entiendo una necesidad
-> la traduzco en requerimientos
-> diseno una solucion
-> la implemento
-> la pruebo
-> la despliego
-> y la sigo manteniendo porque el contexto cambia
```

Eso explica por que ingenieria de software no es sinonimo de programacion.

## Lo que mas se suele confundir

- `programar` no es lo mismo que hacer `ingenieria de software`: programar escribe la solucion; la ingenieria organiza su construccion y evolucion.
- `validacion` y `verificacion` no son sinonimos: una pregunta si hiciste el producto correcto y la otra si lo hiciste correctamente.
- un `requerimiento funcional` y uno `no funcional` son igual de importantes; uno define que hace el sistema y el otro como debe comportarse.

## Como leer este apunte

La idea de este apunte es dejar clara una distincion central de la materia:

```text
ingenieria de software no es solo programar;
es organizar de forma completa la creacion, validacion, despliegue y evolucion del software
```

## 1. Que es la ingenieria

La ingenieria puede pensarse como un conjunto de conocimientos aplicados en acciones sobre ciertas areas con un fin.

### Estructura general

- conocimientos;
- acciones;
- areas;
- fin.

### Conocimientos

- cientificos;
- tecnicos;
- empiricos.

### Acciones

- invencion;
- desarrollo;
- optimizacion;
- validacion;
- mantenimiento.

### Areas

- maquinaria;
- equipos;
- procesos;
- sistemas.

### Fin

- satisfacer una necesidad;
- resolver un problema.

### Sintesis

La ingenieria aplica conocimientos cientificos, tecnicos y empiricos para actuar sobre sistemas y procesos con el objetivo de resolver necesidades reales.

## 2. Que es el software

Decir que el software es "la parte intangible de una computadora" es una definicion incompleta.

El software esta presente en casi todos los aspectos de la vida cotidiana y no se reduce solo al codigo fuente.

### Definicion segun IEEE 729

Segun el estandar IEEE 729, el software es el conjunto de programas de computo, procedimientos, reglas, documentacion y datos asociados que forman parte de la operacion de un sistema de computacion.

Entonces, software incluye:

- programas;
- procedimientos;
- reglas;
- documentacion;
- datos asociados.

## 3. Tipos de software

Algunos tipos importantes son:

- de sistema: brinda servicios a otros programas;
- de aplicacion: resuelve necesidades especificas del usuario;
- cientifico o de ingenieria: se usa para simulaciones, calculos o investigacion;
- embebido: esta integrado en dispositivos como autos o electrodomesticos;
- de inteligencia artificial: se usa para toma de decisiones y aprendizaje.

Cada tipo de software tiene restricciones, riesgos y criterios de calidad distintos.

## 4. Que es buen software

Un buen software no solo funciona: tambien debe sostenerse bien en el uso real.

Buen software:

- cumple su objetivo funcional;
- es usable y accesible;
- tiene buena performance;
- es mantenible en el tiempo;
- es confiable;
- es seguro.

Esto muestra que importa tanto lo que el sistema hace como la forma en que se comporta.

## 5. Que es la ingenieria de software

La ingenieria de software es la aplicacion de la ingenieria al proceso completo de creacion de software.

Va desde que se identifica una necesidad hasta el despliegue y mantenimiento del sistema.

Es un proceso:

- completo;
- iterativo;
- incremental.

No siempre avanza en linea recta: muchas veces hay que volver a etapas previas para ajustar decisiones, corregir problemas o incorporar cambios.

## 6. Por que es importante

La ingenieria de software es importante porque:

- gobiernos y empresas dependen de sistemas software;
- los sistemas criticos deben ser robustos y tolerantes a fallos;
- se necesitan sistemas que puedan mantenerse y escalar con facilidad.

En proyectos reales, improvisar suele salir caro. Hace falta proceso, validacion y criterios claros de calidad.

## 7. Etapas de la ingenieria de software

Una forma clasica de estudiarla es a traves de seis etapas.

## 7.1 Analisis de requerimientos

El objetivo es entender que necesita el cliente o el usuario final.

Esto permite construir el producto adecuado, en lugar de construir bien un producto que no sirve.

### Preguntas clave

- cual es el objetivo del sistema;
- como se adaptara a las necesidades del usuario;
- como se utilizara.

### Actividades de ingenieria de requerimientos

- indagacion;
- negociacion;
- especificacion;
- validacion.

### Objetivos de esta etapa

- describir que quiere el cliente;
- establecer la base del diseno;
- definir requerimientos verificables.

### Requerimientos funcionales y no funcionales

#### Requerimientos funcionales

Especifican lo que el sistema debe hacer.

Incluyen funcionalidades, servicios y tareas que el software debe realizar.

Ejemplos:

- registrar usuarios;
- enviar correos;
- calcular resultados.

#### Requerimientos no funcionales

Describen como debe comportarse el sistema.

Incluyen restricciones y propiedades de calidad.

Ejemplos:

- tiempo de respuesta;
- escalabilidad;
- seguridad;
- usabilidad.

Ambos tipos son esenciales para construir un sistema que no solo funcione, sino que tambien sea util, eficiente y sostenible.

## 7.2 Diseno

A partir de los requerimientos funcionales y no funcionales, se escoge la arquitectura de software mas adecuada.

Un diseno correcto permite construir un sistema:

- escalable;
- mantenible;
- confiable.

El diseno define como se organiza la solucion antes de implementarla.

## 7.3 Implementacion

Consiste en transformar los requerimientos en un producto funcional mediante la escritura de codigo.

Pero no basta con programar. El proceso debe ser organizado para evitar problemas de calidad, mantenimiento y escalabilidad.

## 7.4 Testing y validacion

En esta etapa aparecen dos ideas relacionadas pero distintas:

- validacion: demostrar que el software cumple los requerimientos del cliente;
- verificacion: encontrar errores de funcionamiento.

### Tipos de pruebas

- unitarias: verifican el correcto funcionamiento de componentes o funciones individuales;
- de integracion: evaluan la interaccion entre varios modulos o componentes;
- de aceptacion del usuario (UAT): las realizan usuarios finales para validar que el sistema cumple sus expectativas;
- de usabilidad: evaluan experiencia de uso, accesibilidad, navegabilidad y facilidad de uso.

Una idea importante: tener un equipo de QA no exime a los desarrolladores de probar su propio codigo.

## 7.5 Despliegue

Antes de llegar a produccion, el software suele pasar por distintos entornos.

### Entornos habituales

- development: ambiente donde los programadores escriben y prueban el codigo de manera inicial;
- QA: entorno donde se hacen pruebas exhaustivas antes de liberar el sistema;
- preproduccion o staging: replica el entorno de produccion y se usa para validaciones finales;
- produccion: entorno donde el software queda disponible para usuarios finales.

Cada entorno cumple un rol en la validacion progresiva del sistema.

## 7.6 Mantenimiento

El mantenimiento es necesario para que el software siga siendo util y relevante a lo largo del tiempo.

Una vez desplegado, el software continua evolucionando:

- surgen nuevos requerimientos;
- se descubren errores;
- cambia el negocio o el contexto.

Por eso el proceso no termina cuando el sistema "anda". Muchas veces hay que volver a etapas previas y seguir iterando.

## 8. Idea final para estudiar

Una buena sintesis es esta:

```text
la ingenieria de software aplica principios de ingenieria al proceso completo de crear software,
desde la necesidad inicial hasta su despliegue y mantenimiento
```

Y una version aun mas corta:

```text
hacer software no es solo escribir codigo;
es construir sistemas utiles, confiables y mantenibles
```


