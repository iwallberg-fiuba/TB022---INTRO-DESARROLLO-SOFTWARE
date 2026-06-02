
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
