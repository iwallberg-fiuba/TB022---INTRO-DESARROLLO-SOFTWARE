
Table of Contents


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
