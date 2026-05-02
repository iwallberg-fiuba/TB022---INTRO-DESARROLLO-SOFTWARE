# Apunte largo - SSH Keys

## Fuente trabajada

- `ssh-keys.pdf`

## Idea central

SSH significa Secure Shell. Es un protocolo para comunicacion segura entre maquinas. En el contexto del material, se usa para autenticarte contra GitHub de forma segura usando criptografia de clave publica.

## 1. Para que sirve SSH

- establecer conexiones seguras,
- autenticar usuarios o maquinas,
- cifrar la comunicacion,
- operar servicios remotos sin mandar credenciales en texto plano.

## 2. SSH y GitHub

GitHub pide autenticacion para operaciones que modifican repositorios remotos. Una forma comun de resolverlo es configurar claves SSH.

### Ventajas

- evita ingresar credenciales manualmente en cada operacion,
- usa autenticacion fuerte basada en par de claves,
- es flujo estandar para trabajar con remotos.

## 3. Par de claves

El material menciona:

- clave privada: `id_ed25519`
- clave publica: `id_ed25519.pub`

### Clave privada

- nunca se comparte,
- queda en tu maquina,
- prueba tu identidad.

### Clave publica

- se puede compartir,
- se sube a GitHub,
- permite que GitHub reconozca tu identidad criptografica.

## 4. Flujo de configuracion

1. Generar el par de claves.
2. Conservar la clave privada en tu maquina.
3. Copiar la clave publica.
4. Subirla a GitHub en `Settings -> SSH and GPG keys -> New SSH key`.
5. Verificar la conexion.

## 5. Logica de seguridad

La autenticacion no consiste en mandar la clave privada al servidor. Consiste en demostrar posesion de la privada frente a una publica que el servidor ya conoce.

### Idea importante

- publica: identifica.
- privada: autentica.

## 6. Riesgos y buenas practicas

- nunca compartir la clave privada,
- no subirla a repositorios,
- no mandarla por chat,
- entender que quien la posea puede hacerse pasar por vos ante ese sistema.

## 7. Posibles preguntas de parcial

1. Que es SSH?
2. Para que se usa SSH con GitHub?
3. Diferencia entre clave publica y privada.
4. Por que la privada no debe compartirse?
5. Cual es el flujo general de configuracion?

## 8. Memorizacion rapida

- SSH = protocolo de comunicacion segura.
- GitHub puede autenticarse via SSH.
- Se usa un par de claves.
- Publica se sube. Privada se guarda.
