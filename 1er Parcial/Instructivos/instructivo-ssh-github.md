# Instructivo - SSH y GitHub

## Objetivo

Configurar una clave SSH para autenticarte con GitHub y luego clonar un repositorio remoto.

## 1. Generar la clave SSH

Ejecuta:

```bash
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```

- Usa el mail con el que te registraste en GitHub.
- Presiona `Enter` para aceptar la ruta por defecto.
- Define una passphrase si queres proteger la clave.

## 2. Agregar la clave al agente SSH

Ejecuta:

```bash
ssh-add ~/.ssh/id_ed25519
```

- Ingresa la passphrase si te la pide.

## 3. Mostrar la clave publica

Ejecuta:

```bash
cat ~/.ssh/id_ed25519.pub
```

- Copia todo el contenido que aparece.

## 4. Cargar la clave en GitHub

1. Entra a GitHub.
2. Inicia sesion.
3. Ve a tu foto de perfil.
4. Entra en `Settings`.
5. Abre `SSH and GPG keys`.
6. Toca `New SSH key`.
7. Escribe un titulo descriptivo.
8. Pega la clave publica en `Key`.
9. Confirma con `Add SSH key`.

## 5. Crear un repositorio remoto

1. En GitHub, toca el `+` de arriba a la derecha.
2. Elige `New Repository`.
3. Completa nombre, privacidad y descripcion opcional.
4. Crea el repositorio.

## 6. Clonar el repositorio

1. Copia la URL SSH del repositorio.
2. Ejecuta:

```bash
git clone git@github.com:usuario/repositorio.git
```

3. Entra a la carpeta creada:

```bash
cd repositorio
```

## 7. Verificacion minima

- Si `git clone` funciona, la autenticacion SSH ya esta operativa.
- Si falla, revisar:
- que la clave publica este bien cargada,
- que el agente SSH tenga la clave privada,
- que estes usando la URL SSH y no HTTPS.
