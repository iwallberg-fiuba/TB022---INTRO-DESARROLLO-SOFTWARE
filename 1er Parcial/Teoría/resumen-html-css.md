# Apunte largo - HTML y CSS

## Fuente trabajada

- `HTML y CSS  Intro al Desarrollo de Software.md`

## Idea global del tema

HTML y CSS cumplen funciones distintas pero complementarias:

- HTML estructura el contenido.
- CSS define presentacion, estilo y parte del layout.

## 1. Que es HTML

HTML significa `HyperText Markup Language`.

### Para que sirve

- estructurar paginas web,
- organizar contenido de forma jerarquica,
- indicar al navegador que elementos existen.

### Regla mental

HTML es el esqueleto de la pagina.

## 2. Estructura basica de un documento HTML

- `<!DOCTYPE html>`
- `<html lang="es">`
- `<head>`
- `<body>`

### `head`

Contiene metadatos como:

- `meta charset`
- `title`
- `meta viewport`

### `body`

Contiene lo visible para el usuario.

## 3. Elementos importantes de HTML

### Enlaces

- `<a href="...">`

### Listas

- `<ul>`
- `<ol>`
- `<li>`

### Imagenes

- `<img src="..." alt="...">`

### Tablas

- `<table>`
- `<tr>`
- `<th>`
- `<td>`

### Formularios

- `<form>`
- `<input>`

### Atributos utiles en formularios

- `placeholder`
- `required`
- `maxlength`
- `pattern`

## 4. Estructura semantica y organizacion

### `<nav>`

Bloque de navegacion.

### `<footer>`

Pie de pagina.

### `<div>`

Contenedor generico para agrupar contenido.

## 5. `class` e `id`

### `class`

- puede repetirse,
- agrupa elementos para estilos o comportamiento.

### `id`

- debe ser unico,
- identifica un elemento particular.

## 6. Que es CSS

CSS significa `Cascading Style Sheets`.

### Para que sirve

- color,
- tipografia,
- espaciado,
- tamaños,
- disposicion,
- fondos,
- estados visuales.

### Regla mental

CSS es la presentacion del HTML.

## 7. Formas de incluir CSS

### En linea

Con atributo `style`.

### Interno

Con etiqueta `<style>` dentro de `head`.

### Externo

Con archivo `.css` enlazado con `<link>`.

### Forma recomendada

Archivo externo.

## 8. Sintaxis basica de CSS

```css
selector {
  propiedad: valor;
}
```

## 9. Selectores

- de tipo
- universal
- descendiente
- de ID
- agrupados
- pseudo-clases como `:hover`

## 10. Modelo de caja

Cada elemento se piensa como una caja con:

- contenido
- padding
- border
- margin

## 11. Layout

### Grid

- bidimensional
- filas y columnas
- util para layouts estructurados

### Flexbox

- flexible
- muy util para una dimension principal
- organiza items dentro de un contenedor flex

## 12. Posibles preguntas de parcial

1. Que es HTML?
2. Para que sirve CSS?
3. Diferencia entre HTML y CSS.
4. Que partes basicas tiene un documento HTML?
5. Para que sirven `head` y `body`?
6. Para que sirven `class` e `id`?
7. Que es el box model?
8. Diferencia general entre Grid y Flexbox.

## 13. Memorizacion rapida

- HTML = estructura.
- CSS = estilo y layout.
- `head` = metadatos.
- `body` = contenido visible.
- `class` agrupa; `id` identifica.
- Box model = content + padding + border + margin.
