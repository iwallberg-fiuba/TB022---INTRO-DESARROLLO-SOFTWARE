# Instructivo - Bash Practico

## Objetivo

Tener una secuencia corta de uso practico de Bash: navegar, crear archivos, manejar permisos, redirigir salida y ejecutar scripts.

## 1. Navegacion minima

```bash
pwd
ls -la
cd ~
mkdir practica_bash
cd practica_bash
pwd
```

## 2. Crear estructura de prueba

```bash
mkdir -p proyecto/{src,docs,tests}
touch proyecto/src/main.py
touch proyecto/src/utils.py
touch proyecto/docs/readme.md
touch proyecto/tests/test_main.py
ls -R proyecto/
```

## 3. Copiar, renombrar y borrar

```bash
mkdir proyecto/backup
cp proyecto/src/*.py proyecto/backup/
mv proyecto/docs/readme.md proyecto/docs/README.md
rm -r proyecto/tests/
```

## 4. Probar permisos

```bash
echo '#!/bin/bash' > saludo.sh
echo 'echo "Hola!"' >> saludo.sh
ls -l saludo.sh
chmod +x saludo.sh
./saludo.sh
```

## 5. Redirecciones basicas

```bash
echo "Hola mundo" > archivo.txt
echo "Segunda linea" >> archivo.txt
cat archivo.txt
wc -l < archivo.txt
ls /noexiste 2> errores.txt
```

## 6. Pipes utiles

```bash
history | grep "git"
ls -la | grep ".txt"
cat archivo.txt | wc -w
```

## 7. Variables y sustitucion de comandos

```bash
nombre="Jose"
usuario=$(whoami)
echo "$nombre"
echo "$usuario"
```

## 8. Primer script

Archivo `script.sh`:

```bash
#!/bin/bash
echo "Hola desde Bash"
```

Ejecutar:

```bash
chmod +x script.sh
./script.sh
```

## 9. Input del usuario

```bash
read nombre
echo "Hola, $nombre"
```

## 10. Ejercicio integrador de entregas

El apunte complementario propone un script `gestionar_entregas.sh` con acciones:

- `inicializar`
- `procesar`
- `burlarme`

La idea es automatizar:

- creacion de carpetas,
- validacion de encabezados,
- renombrado por padron,
- transformacion de contenido.
