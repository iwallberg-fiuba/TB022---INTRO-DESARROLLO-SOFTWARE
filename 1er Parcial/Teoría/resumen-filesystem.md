# Apunte largo - Filesystem

## Fuente trabajada

- `filesystem.pdf`

## Idea central

El filesystem es la estructura con la que el sistema operativo organiza y recupera archivos en un disco. Sin esa estructura, los datos existirian solo como bytes desordenados sin nombres, jerarquia ni acceso practico.

## 1. Que define un filesystem

- como se guardan los datos,
- como se nombran,
- como se organizan,
- como se recuperan.

## 2. Modelo Unix

- estructura jerarquica en forma de arbol,
- todo parte del directorio raiz `/`,
- no hay letras de unidad tipo `C:` o `D:`,
- discos y dispositivos se montan dentro del mismo arbol.

## 3. Directorios principales

### `/`

Raiz del sistema.

### `/home`

Directorios personales de usuarios.

### `/etc`

Configuracion del sistema.

### `/bin`

Programas esenciales.

### `/tmp`

Temporales.

### `/var`

Datos variables como logs o caches.

### `/usr`

Programas y bibliotecas del usuario.

## 4. Rutas

### Absoluta

Empieza desde `/`.

Ejemplo:

```text
/home/usuario/proyecto/main.c
```

### Relativa

Parte del directorio actual.

Ejemplo:

```text
proyecto/main.c
```

### Atajos

- `.` = directorio actual.
- `..` = directorio padre.

## 5. Por que esto importa

Entender filesystem es necesario para:

- navegar con terminal,
- compilar,
- mover archivos,
- usar rutas correctas,
- instalar herramientas,
- entender permisos y configuraciones.

## 6. Posibles preguntas de parcial

1. Que es un filesystem?
2. Como se organiza un filesystem Unix?
3. Que representa `/`?
4. Diferencia entre ruta absoluta y relativa.
5. Para que sirven `.` y `..`?
6. Funcion general de `/home`, `/etc`, `/bin`, `/tmp`, `/var`, `/usr`.

## 7. Memorizacion rapida

- Filesystem = organizacion de datos en disco.
- Unix = arbol unico con raiz `/`.
- Absoluta empieza en `/`.
- Relativa parte del directorio actual.
