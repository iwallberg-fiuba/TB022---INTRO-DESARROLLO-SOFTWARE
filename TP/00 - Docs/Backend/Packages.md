

# Packages

Pueden servir para el Frontend, Backend, o la Base de datos.



| Concepto                    | Qué es                                                                                         | Ejemplo                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Gestor de paquetes          | Herramienta para instalar, actualizar y eliminar paquetes                                      | `npm`, `pip`, `apt`, `cargo`                                     |
| Ejecutor de paquetes          | Ejecuta paquetes sin necesidad de instalarlos globalmente / que queden instalados con persistencia.                                   | `npx` es parte de `npm`                                     |
| Paquete                     | Unidad distribuible de código o herramientas que puede instalarse                              | `dotenv`, `nodemon`, `pg`                                        |
| Librería (tipo de paquete)  | Conjunto de funcionalidades que llamás desde tu código                                         | React, jQuery, Lodash                                            |
| Framework (tipo de paquete) | Estructura que organiza una aplicación y llama a tu código                                     | Express, Next.js, Angular                                        |
| Dev Tool (tipo de paquete)  | Herramienta que ayuda durante el desarrollo, pero no forma parte de la lógica de la aplicación | `Nodemon`, `Vite`, `TypeScript`, `Webpack`, linters |


### Instalación de paquetes

```bash
npm install express pg dotenv
npm install --save-dev nodemon
```

- `--save-dev` (o `-D`) guarda las dependencias como `devDependencies` en `package.json`.
- Se utiliza para herramientas de desarrollo que no son necesarias para ejecutar la aplicación en producción.

Al instalar paquetes, npm crea o actualiza:

- `package.json`: guarda las dependencias que necesita el proyecto y los rangos de versiones compatibles.
- `package-lock.json`: guarda las versiones exactas instaladas, incluyendo las dependencias de las dependencias, para garantizar instalaciones reproducibles.


| Paquete        | Función                                                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Express.js** | Facilita la creación de servidores web y APIs que reciben solicitudes y envían respuestas.                                                                                      |
| **pg**         | Permite conectar aplicaciones Node.js con PostgreSQL y ejecutar consultas SQL.                                                                                                  |
| **dotenv**     | Lee un archivo `.env` y carga sus valores como variables de entorno para que la aplicación pueda acceder a configuraciones como puertos, usuarios, contraseñas o claves de API. |
| **nodemon**    | Reinicia automáticamente la aplicación al detectar cambios en los archivos durante el desarrollo.                                                                               |



