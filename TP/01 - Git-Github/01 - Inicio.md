
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
