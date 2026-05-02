# Apunte largo - Ingenieria de Software

## Fuentes trabajadas

- `Ingenieria de Software.pdf`
- `Etapas de la Ingenieria de Software.pdf`

## Idea global del tema

El material quiere instalar una idea fuerte: desarrollar software profesionalmente no es solo programar. La Ingenieria de Software aparece como aplicacion disciplinada de conocimientos, tecnicas, procesos y criterios de calidad al ciclo de vida completo del software.

## 1. Que es ingenieria

Las definiciones trabajadas en las diapositivas convergen en un patron:

- hay conocimientos,
- esos conocimientos se aplican,
- se aplican sobre sistemas, procesos o tecnologias,
- se hace con un fin practico:
- resolver problemas,
- satisfacer necesidades,
- producir soluciones utiles.

### Elementos del patron

#### Conocimientos

- cientificos,
- tecnicos,
- empiricos.

#### Acciones

- inventar,
- diseñar,
- desarrollar,
- construir,
- validar,
- optimizar,
- mantener,
- gestionar.

#### Areas de aplicacion

- sistemas,
- procesos,
- herramientas,
- maquinas,
- estructuras,
- tecnologias.

#### Fin

- resolver un problema practico,
- responder a una necesidad real.

## 2. Que es software

El material discute la definicion simplista de "la parte intangible de la computadora" y la reemplaza por una nocion mucho mas rica.

### Definicion citada

Segun el estandar IEEE 729, software es el conjunto de:

- programas,
- procedimientos,
- reglas,
- documentacion,
- datos asociados.

### Consecuencia importante

Software no es solo codigo fuente.

Tambien incluye:

- comportamiento esperado,
- reglas de operacion,
- informacion asociada,
- y soporte documental.

## 3. Tipos de software mencionados

- de sistema,
- de aplicacion,
- de ingenieria o ciencias,
- embebido,
- IA.

### Mensaje de fondo

El software esta en todas partes y no existe un unico tipo de problema de software.

## 4. Que hace a un buen software

Esta lista es clave para parcial.

### Atributos mencionados

- cumple su objetivo,
- puede ser usado,
- tiene buena performance,
- es mantenible,
- es confiable,
- es seguro.

### Interpretacion breve de cada uno

#### Cumplir objetivo

Resuelve el problema para el cual fue construido.

#### Poder ser usado

No alcanza con que "tecnicamente ande"; debe poder ser operado por personas o sistemas.

#### Buena performance

Usa los recursos de manera razonable y responde en tiempos aceptables.

#### Mantenibilidad

Puede evolucionar, corregirse y adaptarse sin volverse inmanejable.

#### Confiabilidad

Se comporta de forma predecible y estable.

#### Seguridad

Protege datos, procesos y accesos frente a usos indebidos o ataques.

## 5. Por que hace falta Ingenieria de Software

El material lo justifica con varios escenarios.

### Escenario 1: multiples interesados

Como el software impacta a muchas personas, aparecen:

- usuarios finales,
- clientes,
- negocio,
- equipo tecnico,
- operaciones,
- y otras partes interesadas.

Eso genera requisitos diversos y a veces contradictorios.

### Escenario 2: complejidad

Sistemas masivos, redes, plataformas y productos de uso real implican decisiones de arquitectura delicadas.

### Escenario 3: criticidad de los fallos

Un error chico puede ser:

- grave para el usuario,
- costoso para la organizacion,
- o critico en sistemas sensibles.

### Escenario 4: evolucion permanente

El software popular o util inevitablemente recibe:

- pedidos de mejora,
- cambios de negocio,
- correcciones,
- nuevas restricciones.

### Conclusión

No basta con sentarse a programar. Hace falta proceso, criterio, validacion, diseño y mantenimiento.

## 6. Definicion de Ingenieria de Software

Aplicar ingenieria al proceso completo de creacion de software, desde la aparicion de una necesidad o problema hasta el despliegue y mantenimiento de la solucion.

## 7. Actividades que incluye

- comprender la necesidad,
- organizar el desarrollo,
- diseñar el software,
- implementarlo,
- probarlo,
- validarlo,
- desplegarlo,
- mantenerlo.

## 8. Idea metodologica fuerte

El material aclara que hoy la Ingenieria de Software:

- no se piensa solo como secuencia lineal,
- tambien es iterativa,
- tambien es incremental.

### Que significa

#### Iterativa

Se vuelve sobre decisiones, requerimientos y soluciones varias veces.

#### Incremental

El sistema suele crecer por partes, agregando capacidad de manera progresiva.

## 9. Etapas del proceso

## 9.1 Analisis de requerimientos

### Objetivo

Entender que quiere o necesita el cliente o usuario.

### Preguntas que intenta responder

- cual es el objetivo?
- como se adapta a necesidades de usuarios finales?
- como se va a usar?
- cual es el alcance?

### Frase central del material

Construir el producto adecuado no es lo mismo que construir adecuadamente el producto.

### Diferencia clave

#### Construir el producto adecuado

Resolver el problema correcto.

#### Construir adecuadamente el producto

Implementar bien una solucion.

Se puede programar "muy bien" algo que no era lo que el usuario necesitaba.

### Ingenieria de requerimientos

El material menciona:

- indagacion,
- negociacion,
- especificacion,
- validacion.

### Objetivos concretos

- describir lo que quiere el cliente,
- establecer base para el diseño,
- definir requerimientos que luego se puedan validar.

### Por que es importante

Evita:

- desvíos,
- retrasos,
- costos extra,
- y malentendidos estructurales.

## 9.2 Diseño

### Idea central

En base a requerimientos funcionales y no funcionales, hay que elegir una arquitectura adecuada.

### El material insiste en esto

Una buena arquitectura cuesta, pero una mala cuesta mucho mas.

### Casos citados como ejemplo de mal diseño

Las diapositivas muestran situaciones donde mala arquitectura provoca:

- problemas graves de escalabilidad,
- lentitud extrema,
- colapso en lanzamiento,
- retrabajo carisimo,
- perdida de usuarios,
- impacto economico,
- hasta impacto politico.

### Lectura para examen

Diseño no es "decorar" ni "dibujar cajitas". Es tomar decisiones estructurales sobre como se va a organizar la solucion.

## 9.3 Implementacion

### Que es

Pasar de requerimientos y diseño a un producto funcional.

### Que remarca el material

No es simplemente "escribir codigo". Tiene que ser un proceso organizado.

### Por que

Porque codigo sin proceso puede derivar rapido en:

- caos estructural,
- baja mantenibilidad,
- dificultad para probar,
- errores mas costosos.

## 9.4 Testing y validacion

### Distincion clave del material

No son exactamente lo mismo.

#### Validacion

Demostrar al cliente o usuario que el software cumple los requerimientos.

#### Verificacion

Encontrar errores en el funcionamiento.

### Otra idea importante

Las pruebas tambien pueden inspirar cambios en requerimientos. O sea, testear no solo detecta bugs: tambien revela entendimientos incompletos del problema.

### Tipos de test mencionados

- pruebas unitarias,
- pruebas de integracion,
- UAT,
- pruebas de usabilidad.

### Quien prueba

El material marca un punto muy importante:

que exista QA no quiere decir que el desarrollador no tenga que probar su codigo.

## 9.5 Despliegue

### Idea central

El software no pasa de la notebook del dev a produccion de forma directa y ciega.

### Entornos mencionados

- Development.
- QA.
- Preproduccion o Staging.
- Produccion.

### Que transmite esto

Hay una progresion de confianza y control antes de llegar al entorno real de usuarios.

## 9.6 Mantenimiento

### Que pasa despues del despliegue

Segun el material:

- aparecen errores no detectados,
- surgen nuevos requerimientos,
- el negocio cambia,
- el software necesita actualizarse para conservar utilidad.

### Idea muy importante

El mantenimiento no es "una fase triste al final". Es parte esencial de la vida real del software.

## 10. Distinciones que mas conviene saber

### Producto adecuado vs producto bien construido

- uno apunta al problema correcto,
- el otro a la ejecucion correcta.

### Validacion vs verificacion

- validacion = cumplimos lo que se necesitaba?
- verificacion = funciona bien?

### Programar vs hacer Ingenieria de Software

- programar es una actividad,
- ingenieria de software es el proceso profesional completo.

### Lineal vs iterativo/incremental

- lineal da una imagen simplificada,
- realista es pensar en evolucion y retroalimentacion.

## 11. Mensaje de fondo del curso

- El software es omnipresente.
- Su impacto puede ser enorme.
- Su complejidad exige metodologia.
- La calidad no aparece sola.
- La arquitectura y la mantenibilidad no son extras, son parte del problema principal.

## 12. Confusiones comunes

### Confusion 1

Pensar que requerimientos es solo "anotar lo que pide el cliente".

No. Tambien implica entender alcance, negociar y formalizar algo validable.

### Confusion 2

Pensar que diseño es solo interfaz visual.

No. En el material, diseño apunta sobre todo a arquitectura y organizacion de la solucion.

### Confusion 3

Pensar que testing es responsabilidad exclusiva de QA.

No. El desarrollador tambien prueba y verifica.

### Confusion 4

Pensar que al desplegar se termina el trabajo.

No. El software entra en mantenimiento y evolucion.

## 13. Posibles preguntas de parcial

1. Que se entiende por ingenieria en general?
2. Cual es la definicion amplia de software?
3. Que tipos de software menciona el material?
4. Que caracteristicas hacen a un buen software?
5. Por que no alcanza con sentarse a programar?
6. Que es la Ingenieria de Software?
7. Cuales son sus etapas?
8. Por que es importante el analisis de requerimientos?
9. Diferencia entre construir el producto adecuado y construir adecuadamente el producto.
10. Por que el diseño es una etapa critica?
11. Que significa que la implementacion debe ser organizada?
12. Diferencia entre validacion y verificacion.
13. Que tipos de pruebas menciona el material?
14. Que entornos de despliegue se nombran?
15. Por que el mantenimiento es inevitable?
16. Que significa que el proceso sea iterativo e incremental?

## 14. Memorizacion rapida

- Ingenieria = conocimiento aplicado a resolver problemas.
- Software = programas + reglas + procedimientos + documentacion + datos.
- Buen software: util, usable, performante, mantenible, confiable, seguro.
- Ingenieria de Software = aplicar ingenieria al ciclo de vida completo.
- Etapas: requerimientos, diseño, implementacion, testing/validacion, despliegue, mantenimiento.
- Validacion = cumple lo pedido.
- Verificacion = funciona correctamente.
- El proceso real es iterativo e incremental.
