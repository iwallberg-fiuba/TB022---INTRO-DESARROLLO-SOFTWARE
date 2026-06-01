
Table of Contents

Conexión con docker
- Qué usar de docker
- Conexión con base de datos

DBeaver

etapa: desarrollo
- flujo para crear las cosas
- flujo para conectar las cosas
- flujo para cuando estas desarrollando sobre las estructuras ya conectadas y creadas

etapa: Testings
- flujo para crear testeos
- flujo para correr testeos

etapa: deployment
- flujo deployment 


Git y github
Nota: el sistema operativo no cambia en nada en ninguno de los flujos explicados. Igualmente, recomiendo usar `Git Bash` (viene con git y funciona con Windows).


---

Requerimientos Previos

Descargar e instalar:
- Git
- IDE (Visual Studio Code o cualquier otra)


Iniciar sesión en Git (única vez)
1. Abrir la terminal
2. Escribir los siguientes comandos:

```shell
git config --global user.name "tu-nombre"
git config --global user.email "tu-mail@email.com"
```


---

## Crear Repositorio

1. Estar en la carpeta donde se desea crear el repositorio.
2. Click derecho en la carpeta y seleccionar **"Abrir en Terminal"** o abrir en Git Bash (el nombre puede variar según el sistema operativo).
3. Ejecutar:

```shell
git init
```

Esto crea un repositorio Git local (aparece una carpeta oculta `.git`).

4. Verificar el estado del repositorio:

```shell
git status
```

5. Agregar los archivos al área de staging:

```shell
git add .
```

6. Crear el primer commit:

```shell
git commit -m "Primer commit"
```

## Configurar SSH

[Conexión Github y Repo](https://www.intro-camejo.com.ar/docs/Material/Apuntes/configurar-ssh-key)

7. Generar una clave SSH:

```shell
ssh-keygen -t ed25519 -C "tu-mail@email.com"
```

8. Iniciar el agente SSH:

```shell
eval "$(ssh-agent -s)"
```

9. Agregar la clave al agente:

```shell
ssh-add ~/.ssh/id_ed25519
```

10. Mostrar la clave pública:

```shell
cat ~/.ssh/id_ed25519.pub
```

11. Copiar la respuesta de la terminal y agregarla en:

```text
GitHub
↓
Settings
↓
SSH and GPG Keys
↓
New SSH Key
```

12. Verificar la conexión:

```shell
ssh -T git@github.com
```

## Enlace con GitHub 

13. Crear un repositorio vacío en GitHub (el famoso repo remoto "origin").

14. Vincular el repositorio local al remoto usando SSH:

```shell
git remote add origin git@github.com:usuario/nombre-del-repositorio.git
```

15. Enviar los cambios a GitHub.

Si la rama principal se llama `main`:

```shell
git push -u origin main
```

A partir de este momento ya se puede trabajar normalmente con Git y GitHub.

## Colaboradores

Desde GitHub:

```text
Settings
↓
Collaborators
↓
Add people
```

Agregar las cuentas deseadas.

Cuando acepten la invitación, deberán:

1. Configurar SSH (pasos 7 al 12).
2. Clonar el repositorio:

```shell
git clone git@github.com:usuario/mi-proyecto.git
```

Y ya podrán trabajar normalmente con comandos como:

```shell
git pull
git add .
git commit -m "mensaje"
git push
```

---

## Crear ramas
Nota: Uso switch porque me resulta más práctico.

- La rama principal suele llamarse `main`.
- No se debe trabajar directamente sobre ella.

1. Ver las ramas existentes:

```shell
git branch
```

2. Cada integrante debería tener su propia rama. Para crearla:
Nota: al crearla ya quedas parado en esa nueva rama.

```shell
git switch -c nombre-de-la-rama
```

**Para subirla a Github:**

```shell
git push -u origin nombre-de-la-rama
```

Nota: ejemplos de nombres de ramas

```shell
git switch -c feature/login
git switch -c feature/navbar
git switch -c fix/dockerfile
git switch -c docs/readme
```

- Si se desea cambiar de rama:

```shell
git switch nombre-rama-destino
```

---

## Trabajar con ramas y con colaboradores

Estás en VS Code con el proyecto abierto.

1. Verificar en qué rama estás:

```shell
git branch
```

o:

```shell
git status
```

2. Cambiar a tu rama si es necesario:

```shell
git switch nombre-rama-destino
```

3. Traer los cambios más recientes del repositorio remoto:

```shell
git pull
```

4. Verificar el estado actualizado del repositorio:

```shell
git status
```

5. Realizar los cambios deseados en el código.

6. Agregar los cambios al área de staging:

```shell
git add .
```

7. Crear un commit:

```shell
git commit -m "mensaje"
```

Ejemplos de mensaje de commit:

```shell
git commit -m "Agrego pantalla de login"
git commit -m "Corrijo error en Dockerfile"
git commit -m "Actualizo README"
```

8. Subir los cambios a GitHub:

```shell
git push
```

Una vez hechos estos pasos: 
¿Qué pasa si el feature que quería agregar ya está completamente listo y no se volverá a editar? -> ahí aparecen las Pull Requests (PR).

---

## Pull Request (PR)

Un Pull Request es una solicitud para que los cambios de una rama se incorporen a otra (generalmente a `main`).
El **Pull Request ocurre en GitHub**, mientras que **add, commit, push, pull, switch y merge local** son comandos de Git.

1. Ir a GitHub.

2. Seleccionar:

```text
Pull Requests
↓
New Pull Request
```

3. Elegir:

Base branch: rama destino (generalmente main)
Compare branch: rama a incorporar a la rama destino (la tuya)

4. Revisar los cambios que muestra GitHub.

5. Confirmar "Crear el Pull Request".

Ahora se debe esperar a que el Pull Request (PR) pase la etapa de Revisión para después hacer el Merge.


## Revisión

6. Los integrantes del equipo pueden:

* Leer el código.
* Comentar líneas específicas.
* Sugerir cambios.
* Aprobar o rechazar el Pull Request.

```text
GitHub
↓
Pull Request 
↓
Revisión de todos los colaboradores
↓
Botón Merge Pull Request
```

La línea de tiempo de ramas sería algo como:

```text
main
 │
 ├── feature/login
 │       ↓
 │      Pull Request
 │       ↓
 |      Revisión
 |       ↓
 └──── merge PR 
```

## Merge de PR

7. Cuando el Pull Request fue revisado, se toca el botón `Merge Pull Request`.
GitHub combinará las ramas y main quedará actualizada en github, pero no localmente.

8. Ahora se debe apretar:

```txt
Pull Request merged successfully
↓
Delete branch
```

9. Actualizar la copia local:

```shell
git switch main
git pull
```

10. Eliminar la rama completada (la local):

```shell
git branch -d feature/login
```









