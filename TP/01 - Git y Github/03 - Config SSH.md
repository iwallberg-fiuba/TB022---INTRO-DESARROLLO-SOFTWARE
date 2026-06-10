<br>

### Table of Contents

<br>

- [Enlazar Git con Github](#Enlazar-Git-con-Github)
- [Enlazar Repo Local Git con Repo Github](#Enlazar-Repo-Local-Git-con-Repo-Github)

<br>

- Extra: [Apunte sobre Conexión Github y Repo](https://www.intro-camejo.com.ar/docs/Material/Apuntes/configurar-ssh-key)

<br>

---

<br>

### Enlazar Git con Github

<br>

1. Generar una clave SSH en la terminal Git Bash:

```shell
ssh-keygen -t ed25519 -C "tu-mail@email.com"
```

2. Iniciar el agente SSH:

```shell
eval "$(ssh-agent -s)"
```

3. Agregar la clave al agente:

```shell
ssh-add ~/.ssh/id_ed25519
```

4. Mostrar la clave pública:

```shell
cat ~/.ssh/id_ed25519.pub
```

5. Copiar la respuesta de la terminal y ponerla en:

```text
GitHub
↓
Settings
↓
SSH and GPG Keys
↓
New SSH Key
```

6. Verificar la conexión:

```shell
ssh -T git@github.com
```

<br>

---

<br>

### Enlazar Repo Local Git con Repo GitHub 

<br>

7. Crear un repositorio vacío en GitHub (el famoso repo remoto "origin").

8. Vincular el repositorio local al remoto usando SSH:

```shell
git remote add origin git@github.com:usuario/nombre-del-repositorio.git
```

9. Enviar los cambios a GitHub.

Si la rama principal se llama `main`:

```shell
git push -u origin main
```

A partir de este momento ya se puede trabajar normalmente con Git y GitHub.
