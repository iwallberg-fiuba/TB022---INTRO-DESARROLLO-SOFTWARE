# Apunte largo - Git

## Fuentes trabajadas

- `intro-git.pdf`
- `Git.htm`

## Idea central

Git es un sistema de control de versiones distribuido. Su objetivo es registrar cambios sobre archivos y permitir:

- volver a estados anteriores,
- entender la evolucion del proyecto,
- coordinar trabajo entre varias personas,
- y desarrollar lineas de trabajo paralelas de forma controlada.

El material base cubre la introduccion general y el HTML de Canva agrega la parte operativa de ramas, PRs, conflictos y buenas practicas.

## 1. Que es control de versiones

Control de versiones es software que registra cambios a lo largo del tiempo.

### Que permite

- recuperar versiones anteriores,
- ver historial completo,
- saber quien cambio que,
- saber cuando lo cambio,
- comparar estados del proyecto,
- trabajar en equipo sin sobrescribir trabajo ajeno.

### Problema que resuelve

Sin control de versiones:

- se pierden cambios,
- no hay trazabilidad,
- es facil romper algo sin poder volver,
- el trabajo en equipo se vuelve caotico.

## 2. Breve historia

### Sistemas anteriores

- SCCS: local.
- RCS: local.
- CVS: centralizado.
- SVN: centralizado.
- BitKeeper: distribuido.
- Mercurial: distribuido.
- Git: distribuido.

### Centralizado vs distribuido

#### Centralizado

- depende de un servidor unico,
- el historial fuerte vive en el servidor,
- el cliente depende mucho de conectividad y del central.

#### Distribuido

- cada desarrollador tiene copia completa del historial,
- se puede trabajar localmente con mas libertad,
- el modelo favorece ramas y flujos no lineales.

## 3. Como nace Git

El kernel Linux usaba BitKeeper. Al romperse esa relacion, Linus Torvalds crea Git en 2005 con objetivos claros:

- velocidad,
- diseño simple,
- soporte para desarrollo no lineal,
- capacidad de manejar muchas ramas,
- modelo completamente distribuido,
- open source.

## 4. Que es un repositorio

Un repositorio es un directorio cuyo historial de cambios es trackeado por Git.

### Caracteristicas

- Se crea con `git init`.
- Contiene una carpeta oculta `.git/`.
- Puede ser local o remoto.

### `.git/`

La carpeta `.git/` guarda:

- metadata,
- commits,
- referencias,
- ramas,
- configuracion interna del repositorio.

## 5. Los tres estados de Git

Esta es una de las ideas mas importantes para examen.

### Working Directory

- Es donde editas los archivos.
- Aca viven tus cambios todavia no preparados para commit.

### Staging Area

- Zona intermedia.
- Aca elegis que cambios van al proximo commit.
- Tambien se llama `index`.

### Repository

- Historial ya confirmado.
- Representa el estado persistente dentro del repo Git.

### Idea clave

Git no pasa directamente de "edite" a "historial". Primero seleccionas que entra al commit.

## 6. Flujo basico

1. Modificas archivos.
2. Revisas diferencias.
3. Agregas al staging con `git add`.
4. Confirmas con `git commit`.
5. Subes al remoto con `git push` si queres compartir.

### Interpretacion conceptual

- editar = trabajar,
- `add` = preparar,
- `commit` = registrar,
- `push` = publicar.

## 7. Comandos fundamentales

### Inicializacion y estado

- `git init`
- `git status`
- `git diff`

### Preparacion y confirmacion

- `git add <archivo>`
- `git commit -m "mensaje"`

### Historial

- `git log`
- `git log --graph --oneline`

### Remotos

- `git clone <url>`
- `git pull`
- `git push`

### Ramas

- `git branch`
- `git checkout <rama>`
- `git merge <rama>`

## 8. Lectura de algunos comandos

### `git status`

Te dice:

- que archivos cambiaron,
- cuales estan en staging,
- cuales no,
- si hay conflictos,
- en que rama estas.

### `git diff`

Muestra diferencias aun no stageadas.

### `git log --graph --oneline`

Resume el historial y ayuda a visualizar ramas y merges.

## 9. Branches

El Canva `Git.htm` esta muy enfocado en esto.

### Que es una rama

- Una linea de trabajo independiente.
- Permite hacer cambios sin afectar directamente `main`.

### Para que sirve

- desarrollar features nuevas,
- arreglar bugs,
- probar ideas,
- trabajar en paralelo con otras personas.

### Idea de fondo

La rama desacopla trabajo en progreso del codigo principal.

## 10. Flujo tipico con ramas

El material presenta un "flujo esperado":

1. Crear branch.
2. Hacer cambios.
3. Hacer commits y push.
4. Crear PR.
5. Revisar PR.
6. Merge a `main`.

### Por que es sano este flujo

- mantiene `main` mas estable,
- hace visible el trabajo en curso,
- fuerza una instancia de revision,
- reduce integraciones caoticas.

## 11. Pull Request

### Que es

Un PR es una solicitud para integrar cambios de una rama en otra.

### Que pasa adentro de un PR

El material lo resume en cuatro ejes:

- revision de codigo,
- comentarios y sugerencias,
- validacion,
- aprobacion.

### Para que sirve

- revisar antes de mergear,
- recibir feedback del equipo,
- documentar discusion tecnica,
- centralizar aprobacion.

## 12. Estrategias de ramas

El material muestra varias.

### Estrategia minima

- `main`
- `feature`

Simple y comun en equipos chicos o flujos iniciales.

### Estrategia intermedia

- `main`
- `develop`
- `feature`

Separa rama estable de rama de integracion.

### Gitflow

- `main`
- `develop`
- `release`
- `hotfix`
- `feature`

Mas estructurada. Aporta orden pero tambien mas proceso.

### Que conviene entender

No memorizar nombres por reflejo, sino la idea:

- ramas pueden representar estabilidad,
- integracion,
- trabajo nuevo,
- correcciones urgentes.

## 13. Conflictos

### Como se producen

El material del Canva menciona tres casos tipicos:

- modificaciones simultaneas en la misma linea,
- reorganizaciones grandes del codigo en ramas distintas,
- eliminacion de un archivo en una rama mientras en otra se modifica.

### Como evitarlos

- pulls frecuentes,
- commits atomicos,
- comunicacion con el equipo.

### Por que ayudan los commits atomicos

Porque concentran una idea por commit y vuelven mas facil:

- revisar,
- revertir,
- entender,
- y resolver conflictos.

## 14. Como resolver conflictos

1. Ejecutar `git status` para detectar archivos conflictivos.
2. Abrir los archivos y corregir incompatibilidades manualmente.
3. Verificar que el resultado final tenga sentido funcional.
4. Agregar los archivos resueltos.
5. Committear la resolucion.

### Idea importante

Resolver conflicto no es "hacer desaparecer marcas", sino decidir correctamente que version final debe quedar.

## 15. `git restore`

El material cierra con este comando porque apunta a operaciones comunes de recuperacion.

### `git restore --staged archivo.txt`

- saca el archivo del staging,
- mantiene cambios locales.

### `git restore archivo.txt`

- restaura el archivo a la version del ultimo commit,
- descarta cambios no confirmados de ese archivo.

### `git restore --source=<commit-id> archivo.txt`

- trae la version de un commit especifico,
- sin tocar el resto del proyecto.

## 16. Git local vs hosting remoto

El material remarca algo conceptual:

- Git es una herramienta local.
- GitHub, GitLab, Bitbucket o Gitea son servicios para alojar repositorios remotos.

### Por que importa esta distincion

Porque muchas personas mezclan:

- Git = sistema de versionado,
- GitHub = plataforma de colaboracion sobre repositorios Git.

No son lo mismo.

## 17. Subir un repositorio

El PDF menciona crear primero un repo vacio en GitHub, sin README ni `.gitignore`, para luego vincular el local y subirlo.

### Que idea hay detras

Evitar conflictos iniciales innecesarios entre historial local y archivos creados automaticamente en el remoto.

## 18. Buenas practicas que se desprenden del material

- no trabajar todo directo en `main`,
- hacer ramas chicas y concretas,
- hacer commits atomicos,
- hacer pull frecuente,
- revisar PRs con criterio tecnico,
- usar el historial como herramienta de trabajo, no solo como formalidad.

## 19. Confusiones comunes

### Confusion 1

Pensar que `git add` "guarda definitivamente".

No. Solo prepara para commit.

### Confusion 2

Pensar que `push` crea el historial.

No. El historial nace con `commit`; `push` lo publica en un remoto.

### Confusion 3

Pensar que branch y repositorio son lo mismo.

No. La branch es una linea dentro del repositorio.

### Confusion 4

Pensar que conflicto es señal de fracaso.

No. Es una consecuencia normal de trabajo paralelo sobre partes relacionadas.

## 20. Posibles preguntas de parcial

1. Que es control de versiones y para que sirve?
2. Diferencia entre sistema centralizado y distribuido.
3. Por que Git se considera distribuido?
4. Que es un repositorio?
5. Para que sirve la carpeta `.git/`?
6. Explica los tres estados: working directory, staging area y repository.
7. Explica el flujo basico de Git.
8. Diferencia entre `git add`, `git commit` y `git push`.
9. Que es una branch y para que sirve?
10. Que es un pull request?
11. Como se originan conflictos?
12. Como se pueden evitar?
13. Como se resuelven?
14. Para que sirve `git restore` en sus variantes principales?
15. Diferencia entre Git y GitHub.

## 21. Memorizacion rapida

- Git registra historia de cambios.
- Es distribuido: cada clon tiene historial completo.
- Repo = directorio trackeado por Git.
- Estados: working directory, staging, repository.
- Flujo: editar -> add -> commit -> push.
- Branch = linea independiente de desarrollo.
- PR = pedido de integracion con revision.
- Conflictos nacen por cambios incompatibles sobre mismo contenido.
- `git restore` ayuda a deshacer o recuperar estados puntuales.
