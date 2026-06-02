<br>

### Configurar SSH

<br>

- Extra: [Apunte sobre Conexión Github y Repo](https://www.intro-camejo.com.ar/docs/Material/Apuntes/configurar-ssh-key)

<br>
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
