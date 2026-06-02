
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
