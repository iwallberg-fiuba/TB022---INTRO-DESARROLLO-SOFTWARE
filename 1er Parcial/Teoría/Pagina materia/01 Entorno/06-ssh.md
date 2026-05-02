
> **Idea:** SSH deja de parecer una receta arbitraria cuando entendes que el problema real es demostrar identidad sin mandar la contrasena en cada operacion.

## Keywords a saber

`SSH`, `clave publica`, `clave privada`, `ssh-keygen`, `ssh-agent`, `ssh-add`, `GitHub`, `autenticacion`, `remote`, `git@github.com`, `passphrase`

> **Para estudiar:** pensa siempre en el flujo completo: generar, guardar, compartir la parte correcta y verificar la identidad.

## Definiciones rapidas

| Keyword | Definicion | Para entenderlo mejor |
| --- | --- | --- |
| `SSH` | Protocolo para comunicacion segura y autenticacion entre maquinas. | En este contexto importa menos la teoria de redes y mas la idea de acceso confiable sin mandar la contrasena todo el tiempo. |
| `clave publica` | Parte del par de claves que se comparte con servicios como GitHub. | Se comparte porque por si sola no alcanza para hacerse pasar por vos. Sirve para que el servicio sepa con que verificarte. |
| `clave privada` | Parte secreta del par de claves que queda en tu maquina. | Es la pieza sensible del sistema. Si se filtra, tu identidad tecnica queda comprometida. |
| `ssh-keygen` | Comando que genera un par de claves SSH. | Es el punto de arranque de todo el flujo: sin ese par, no hay autenticacion por clave publica. |
| `ssh-agent` | Proceso que mantiene claves cargadas en memoria para no reingresarlas. | Hace mas comodo el trabajo diario porque evita desbloquear la clave en cada operacion. |
| `ssh-add` | Comando para agregar una clave al `ssh-agent`. | Sin este paso, a veces la clave existe pero no esta activa para el uso inmediato. |
| `GitHub` | Plataforma que aloja repositorios Git y valida tu acceso remoto. | En este tema importa porque actua como servidor que necesita confiar en que sos vos. |
| `autenticacion` | Proceso para demostrar que realmente sos quien intenta conectarse. | No es lo mismo que autorizacion: primero probas identidad, despues el servicio decide que te deja hacer. |
| `remote` | Referencia a un repositorio alojado en otro lugar. | Es el "destino remoto" con el que tu repo local se sincroniza. |
| `git@github.com` | Formato de direccion SSH usado para conectar con GitHub. | Esa forma ya te indica que Git usara SSH en lugar de HTTPS para hablar con GitHub. |
| `passphrase` | Frase extra que protege el uso de una clave privada. | Funciona como una capa adicional: aunque alguien copie el archivo, todavia necesita esa frase para usarlo. |

## Tabla comparativa rapida

| Concepto | Se comparte | Para que sirve |
| --- | --- | --- |
| `clave publica` | Si | Identificar con que clave debe validarte GitHub |
| `clave privada` | No | Probar tu identidad al firmar la conexion |

## Mapa mental rapido

El flujo completo es este:

```text
genero un par de claves
-> subo la publica a GitHub
-> guardo la privada en mi maquina
-> GitHub verifica que quien se conecta posee la privada correcta
```

Si se entiende esa logica, deja de parecer magia o una receta arbitraria.

## Lo que mas se suele confundir

- `clave publica` y `clave privada` nacen juntas, pero no cumplen el mismo rol: una se comparte y la otra prueba tu identidad.
- `autenticacion` no es lo mismo que `autorizacion`: primero el sistema verifica quien sos y despues decide que te permite hacer.
- usar direccion SSH como `git@github.com:...` no es solo otra sintaxis; implica cambiar el mecanismo de conexion respecto de HTTPS.

## Como leer este apunte

Este archivo conserva el flujo practico del instructivo original, pero lo reordena para que se entienda primero la logica y despues los pasos.

La idea no es solo "seguir una receta", sino comprender:

- que es SSH;
- que papel cumplen la clave publica y la privada;
- por que GitHub las usa;
- y como se configura el acceso sin contrasenas en cada push.

## 1. Que es SSH

SSH significa `Secure Shell`.

Es un protocolo que permite comunicacion segura entre maquinas.

En el contexto de GitHub, se usa sobre todo para autenticacion:

- demostrar que sos vos;
- sin mandar tu contrasena en cada operacion;
- usando criptografia de clave publica.

## 2. Clave publica y clave privada

Cuando generas una clave SSH, en realidad generas un par:

- clave privada;
- clave publica.

### Clave privada

- queda en tu maquina;
- no se comparte;
- prueba tu identidad.

### Clave publica

- se puede compartir;
- se sube a GitHub;
- le dice a GitHub con que clave verificar tu autenticacion.

La idea central es esta:

- publica: identifica;
- privada: autentica.

## 3. Por que usar SSH con GitHub

Porque GitHub necesita autenticarte para operaciones que modifican repositorios remotos.

Ejemplos:

- `git clone` de un repo publico puede no pedir autenticacion;
- `git push` a tu repo si necesita saber que realmente sos vos.

Usar SSH evita escribir credenciales cada vez y deja un flujo mas comodo y seguro.

## 4. Generar la clave

En terminal:

```bash
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```

Que significa:

- `ssh-keygen`: genera claves;
- `-t ed25519`: usa el algoritmo `ed25519`;
- `-C`: agrega un comentario, normalmente tu email.

Cuando lo ejecutes:

1. te preguntara donde guardar la clave;
2. normalmente podes aceptar la ruta por defecto;
3. te pedira una passphrase;
4. la repetis para confirmarla.

La passphrase no reemplaza la clave. Es una capa extra de seguridad sobre tu clave privada.

## 5. Donde quedan los archivos

Por defecto suelen guardarse en:

```text
~/.ssh/
```

Normalmente aparecen dos archivos:

- `id_ed25519`: clave privada;
- `id_ed25519.pub`: clave publica.

Regla importante:

- el archivo sin `.pub` no se comparte;
- el archivo con `.pub` es el que si se copia a GitHub.

## 6. Activar el agente SSH

El agente SSH es un proceso que guarda temporalmente tus claves en memoria para no pedirlas todo el tiempo.

Primero se inicia:

```bash
eval "$(ssh-agent -s)"
```

Despues se agrega la clave:

```bash
ssh-add ~/.ssh/id_ed25519
```

Si la clave tiene passphrase, te la pedira en este paso.

## 7. Copiar la clave publica

Tenes que copiar el contenido del archivo `.pub`.

Por ejemplo:

```bash
cat ~/.ssh/id_ed25519.pub
```

Eso muestra una linea larga que empieza con algo como:

```text
ssh-ed25519 AAAAC3...
```

Ese texto completo es la clave publica que se agrega en GitHub.

## 8. Agregar la clave en GitHub

Dentro de GitHub:

1. entras a `Settings`;
2. vas a `SSH and GPG keys`;
3. elegis `New SSH key`;
4. pegas la clave publica;
5. guardas.

En ese momento GitHub pasa a reconocer esa clave como tuya.

## 9. Probar la conexion

Para verificar que todo quedo bien:

```bash
ssh -T git@github.com
```

La primera vez puede preguntar si confias en el host. Si corresponde, aceptas.

Si esta todo correcto, GitHub responde con un mensaje de autenticacion exitosa.

Idea importante:

- esto no te abre una shell interactiva en GitHub;
- solo verifica identidad y conectividad.

## 10. Cambiar la URL remota del repositorio

Si tu repo estaba configurado con HTTPS, puede convenir pasarlo a SSH.

Ver la URL actual:

```bash
git remote -v
```

Cambiarla:

```bash
git remote set-url origin git@github.com:usuario/repositorio.git
```

Desde ahi, `push`, `pull` y `fetch` usaran SSH.

## 11. Que problema resuelve todo esto

Sin SSH, el flujo suele depender de contrasenas, tokens o login frecuente.

Con SSH:

- tu maquina se identifica con una clave;
- GitHub valida que la clave publica asociada coincide;
- vos trabajas con un flujo mas directo.

No es magia: es autenticacion criptografica.

## 12. Errores comunes

### Permission denied (publickey)

Suele significar alguna de estas cosas:

- la clave no fue agregada a GitHub;
- el agente SSH no esta usando la clave;
- el repo sigue con URL HTTPS;
- se uso otra clave distinta a la registrada.

### Agregar la clave equivocada

Error tipico:

- subir la privada en vez de la publica.

Recorda:

- publica: archivo `.pub`;
- privada: archivo sin `.pub`.

### No recordar donde se guardo la clave

Si elegiste una ruta distinta a la default, despues tenes que usar esa misma ruta con `ssh-add`.

## 13. Resumen rapido

Flujo completo:

1. generar clave con `ssh-keygen`;
2. iniciar `ssh-agent`;
3. agregar clave con `ssh-add`;
4. copiar clave publica;
5. pegarla en GitHub;
6. probar con `ssh -T git@github.com`;
7. usar URL remota SSH en el repo.

## 14. Idea final para examen o practica

Si te preguntan para que sirve configurar una SSH key con GitHub, una buena respuesta corta seria:

```text
Sirve para autenticar de forma segura una maquina frente a GitHub usando criptografia de clave publica, evitando ingresar credenciales manualmente en cada operacion remota.
```


