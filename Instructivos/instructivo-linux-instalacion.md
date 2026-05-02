# Instructivo - Linux Instalacion

## Objetivo

Separar las opciones practicas para empezar a usar Linux segun el entorno.

## 1. Opcion A: Dual-Boot

### Cuándo sirve

Cuando queres Linux instalado en la misma maquina junto con otro sistema operativo.

### Pasos generales

1. Hacer backup de datos importantes.
2. Verificar espacio libre en disco.
3. Crear particion para Linux si hace falta.
4. Preparar USB o medio booteable.
5. Arrancar desde ese medio.
6. Instalar Linux junto al sistema existente.
7. Completar instalacion y reiniciar.
8. Elegir sistema desde el gestor de arranque.

## 2. Opcion B: Maquina Virtual

### Cuándo sirve

Cuando queres probar Linux sin tocar el sistema principal.

### Con VirtualBox o VMware

1. Instalar VirtualBox o VMware Player.
2. Crear nueva maquina virtual.
3. Asignar RAM y disco.
4. Montar imagen ISO de Linux.
5. Iniciar VM.
6. Seguir instalador.
7. Ajustar configuracion despues si hace falta.

## 3. Opcion C: Contenedor Docker

### Cuándo sirve

Cuando queres experimentar un entorno Linux aislado sin instalar un sistema completo.

### Pasos basicos

1. Instalar Docker.
2. Descargar una imagen, por ejemplo:

```bash
docker pull ubuntu
```

3. Ejecutar contenedor interactivo:

```bash
docker run -it ubuntu
```

4. Trabajar dentro del contenedor.

## 4. Verificaciones utiles

### Confirmar shell y usuario

- mirar el prompt,
- `$` suele indicar usuario comun,
- `#` suele indicar root.

### Confirmar ubicacion actual

```bash
pwd
```

### Listar archivos

```bash
ls -la
```

## 5. Recomendacion practica

- Si queres entorno real y comodo: instalacion nativa o dual-boot.
- Si queres probar sin tocar mucho: VM.
- Si queres solo entorno aislado de trabajo puntual: contenedor.
