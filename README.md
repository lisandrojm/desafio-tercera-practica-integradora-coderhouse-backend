# DESAFÍO ENTREGABLE - Tercera práctica integradora - Coderhouse/Backend

Este repositorio contiene el desafío "Tercera práctica integradora" con las siguientes características:

# Objetivos

## Reestablecimiento de contraseña

Realización de un sistema de reestablecimiento de contraseña, el cual envía por medio de un correo un link que redirecciona a una página para restablecer la contraseña.

- El link del correo expira después de 1 hora de enviado.
- Se impide reestablecer la contraseña con la misma contraseña del usuario y se le indica que no se puede colocar la misma contraseña.
- Cuando el link expira se redirige al usuario a una vista que le permite generar nuevamente el correo de restablecimiento, el cual cuenta con una nueva duración de 1 hora.

<small>Directorio/s , ruta/s y método/s de referencia</small>

- `/src/components/users`

  - `/src/components/users/index.js`

    - Ruta/s:
      - /api/session/useradmin/resetpass (post)
      - /api/session/useradmin/resetpassbyemail (get)

  - `/src/components/users/usersServices/usersServices.js`
  - `/src/components/users/usersController/usersController.js`

    - Método/s:

      - resetPass
      - resetPassByEmail

- `/src/components/handlebars`

  - `/src/components/handlebars/index.js`

    - Ruta/s:
      - /resetpass/:token (get)
      - /resetpassbyemail (get)
      - /resetpassexpiredtoken (get)

  - `/src/components/handlebars/handlebarsServices/handlebarsServices.js`
  - `/src/components/handlebars/handlebarsController/handlebarsController.js`

    - Método/s:

      - getResetPass
      - getResetPassByEmail
      - getResetPassExpiredToken

## Role "premium"

Establecimiento de un nuevo rol para el schema del usuario llamado “premium”, el cual está habilitado también para crear productos.

<small>Directorio/s de referencia</small>

- `/src/models/users.js`

## Schema de producto - Campo "owner"

Modificación del schema de producto con un campo “owner”, el cual hace referencia a la persona que creó el producto.

- Si un producto se crea sin owner, se coloca por defecto “admin”.
- El campo "owner" solo guarda el \_id del usuario que lo creó. Sólo puede recibir usuarios "premium".

<small>Directorio/s de referencia</small>

- `/src/models/products.js`

## Asignación de permisos para el role "premium"

### Productos

Modificación y eliminación de productos.

- Un usuario "premium" sólo pueda borrar los productos que le pertenecen.

- El "admin" puede borrar cualquier producto, aún si es de un "owner".

<small>Directorio/s , ruta/s y método/s de referencia</small>

- `/src/components/products`

  - `/src/components/products/index.js`

    - Ruta/s:
      - /api/products/ (post)
      - /api/products/:pid (put)
      - /api/products/:pid (delete)

  - `/src/components/handlebars/handlebarsServices/handlebarsServices.js`
  - `/src/components/handlebars/handlebarsController/handlebarsController.js`

    - Método/s:

      - addProduct
      - updateProduct
      - deleteProduct

### Carrito

Agregar productos al carrito.

- Modificación de la lógica del carrito para que un usuario "premium" NO pueda agregar a su carrito un producto que le pertenece

<small>Directorio/s , ruta/s y método/s de referencia</small>

- `/src/components/carts`

  - `/src/components/carts/index.js`

    - Ruta/s:
      - /api/carts/:cid/product/:pid (post)

  - `/src/components/carts/cartsServices/cartsServices.js`
  - `/src/components/carts/cartsController/cartsController.js`

    - Método/s:

      - addProductToCart

## Implementación de la ruta /api/users/premium/:uid

Esta nueva ruta permite cambiar el rol de un usuario, de “user” a “premium” y viceversa.

<small>Directorio/s , ruta/s y método/s de referencia</small>

- `/src/components/users`

  - `/src/components/users/index.js`

    - Ruta/s:
      - /api/users/premium/:uid (put)

  - `/src/components/users/usersServices/usersServices.js`
  - `/src/components/users/usersController/usersController.js`

    - Método/s:

      - updateUserPremium

---

## Requisitos

Asegúrate de tener los siguientes requisitos instalados en tu entorno de desarrollo:

- Node.js
- MongoDB

## Instrucciones de instalación

Sigue estos pasos para instalar y configurar el proyecto:

1. Clona este repositorio en tu máquina local:

   ```bash
   git clone https://github.com/lisandrojm/desafio_tercera_practica_integradora
   ```

2. Navega al directorio del proyecto:

   ```bash
   cd desafio_tercera_practica_integradora
   ```

3. Instala las dependencias del proyecto ejecutando el siguiente comando:

   ```bash
   npm install
   ```

4. Configura la conexión a la base de datos MongoDB y todas las variables de entorno en el archivo `.env`. Puedes copiar el archivo `.env.example` y renombrarlo a `.env`, luego actualiza los valores con tu configuración:

   ```bash
   cp .env.example .env
   ```

   Asegúrate de tener MongoDB en ejecución , la URL de conexión correcta y todas las variables de entorno configuradas en el archivo `.env`.

5. Inicia la aplicación con el siguiente comando:

   ```bash
   npm start
   ```

   Esto iniciará el servidor Node.js y estará escuchando en el puerto especificado en el archivo `.env`.

6. Accede a la aplicación en tu navegador web ingresando la siguiente URL:

   ```
   http://localhost:<PUERTO_DE_LA_APP>
   ```

   Asegúrate de reemplazar `<PUERTO_DE_LA_APP>` con el número de puerto especificado en el archivo `.env`.

7. Ahora podrás utilizar la vista de Login en la aplicación.

## Credenciales de Admin:

### Email:

```
adminCoder@coder.com
```

### Password:

```
adminCod3r123
```

## Estructura general del proyecto

Aquí tienes la estructura del proyecto con descripciones para cada directorio:

El proyecto sigue la siguiente estructura de directorios:

- `/.env`: Variables de entorno.

- `/.env.example`: Archivo de ejemplo que muestra la estructura y variables de entorno requeridas para la configuración de la aplicación.

- `/src/components`: Carpeta contenedora de todos los componentes. Cada componente contiene un archivo index.js con sus rutas, una carpeta de controlador y una de servicios.

- `/src/config`: Archivos de configuración de la aplicación.

  - `/src/config/index.js`: Exporta variables de entorno y configuraciones generales.
  - `/src/config/mongo.js`: Configuración de Mongoose para establecer la conexión a la base de datos MongoDB.
  - `/src/config/passport.js`: Configuración de Passport para generar las estrategias de autenticación y autorización.

- `/src/models`: Modelos de datos de la aplicación.

- `/src/public`: Archivos públicos de la aplicación, como estilos CSS, imágenes y scripts JavaScript.

- `/src/routes`: Archivos de definición de rutas de la aplicación.

- `/src/utils`: Archivos relacionados con la configuración de las utilidades reutilizables.

- `/src/views`: Todas las vistas del proyecto.

## Dependencias

El proyecto utiliza las siguientes dependencias:

- **Express.js (v4.18.2):** Framework de Node.js para construir aplicaciones web.
- **UUID (v9.0.0):** Biblioteca para generar identificadores únicos.
- **Cors (v2.8.5):** Middleware para permitir peticiones HTTP entre diferentes dominios.
- **Dotenv (v16.3.1):** Carga variables de entorno desde un archivo .env.
- **Express-handlebars (v7.0.7):** Motor de plantillas para Express.js.
- **MongoDB (v5.6.0):** Driver de MongoDB para Node.js.
- **Mongoose (v7.3.1):** Modelado de objetos de MongoDB para Node.js.
- **Multer (v1.4.5-lts.1):** Middleware para manejar datos de formulario multipart/form-data.
- **Socket.io (v4.6.2):** Biblioteca para la comunicación en tiempo real basada en WebSockets.
- **Sweetalert2 (v11.7.12):** Biblioteca para mostrar mensajes y alertas personalizadas.
- **Connect-mongo (v5.0.0):** Middleware para almacenar sesiones de Express.js en MongoDB.
- **Cookie-parser (v1.4.6):** Middleware para analizar cookies en las solicitudes de Express.js.
- **Express-session (v1.17.3):** Middleware para manejar sesiones en Express.js.
- **Mongoose-paginate-v2 (v1.7.1):** Plugin de paginación para Mongoose.
- **Bcrypt (v5.1.0):** Biblioteca para el hashing seguro de contraseñas.
- **Passport (v0.6.0):** Middleware para autenticación en Node.js.
- **Passport-github2 (v0.1.12):** Estrategia de autenticación para Passport usando OAuth 2.0 con GitHub.
- **Passport-local (v1.0.0):** Estrategia de autenticación para Passport basada en credenciales locales.
- **Jsonwebtoken (v9.0.1):** Biblioteca para generar y verificar tokens JWT.
- **Passport-jwt (v4.0.1):** Estrategia de autenticación para Passport que utiliza tokens JWT (JSON Web Tokens) para la autenticación de usuarios.
- **Commander (v11.0.0):** Biblioteca para crear interfaces de línea de comandos interactivas en Node.js.
- **Twilio (v4.16.0):** Biblioteca para enviar y recibir mensajes de texto y realizar llamadas telefónicas a través de la API de Twilio.
- **Nodemailer (v6.9.4):** Biblioteca para enviar correos electrónicos desde una aplicación Node.js.
- **Faker (v5.5.3):** Biblioteca para generar datos falsos como nombres, direcciones, correos electrónicos, etc., útil para pruebas y desarrollo.
- **@hapi/boom (v10.0.1):** Biblioteca para manejar errores HTTP de una manera más consistente y amigable.
- **winston (v3.10.0):** Biblioteca para el registro de registros (logs) en Node.js.

## DevDependencies

El proyecto utiliza las siguientes devDependencies:

- Nodemon (v2.0.22): Utilidad que monitoriza cambios en los archivos y reinicia automáticamente la aplicación.

Estas dependencias pueden ser instaladas ejecutando el comando `npm install` en el directorio del proyecto.

## Postman Collections

- En la carpeta `postman_collections`, encontrarás los archivos necesarios para importar las colecciones en Postman y realizar pruebas en el proyecto. Las colecciones proporcionan ejemplos de solicitudes HTTP para interactuar con la API y probar su funcionalidad.

- Importante: Como el proyecto cuenta con un Middleware de autorización hay que realizar los siguientes pasos en Postman:

  1.0 - Ir a Postman/Headers/Cookies/Manage Cookies.

  2.0 - Type a domain name:localhost.

  3.0 - Template: Cookie_5=value; Path=/; Expires=Sun, 01 Sep 2024 22:47:37 GMT;

  3.1 - Loguearse como Admin o como User según corresponda para testear la ruta.

  3.2 - Una vez logueado ingresar a Application/Cookies/http://localhost:8080 y copiar el value del token jwt.

  3.3 - En el Template de la cookie de Postman reemplazar Cookie_5 por jwt y value por el value del token copiado.

  3.4 - Debe quedar un código como el siguiente (el token a continuación es un ejemplo):

  jwt=ey123456789wolrtjlwkjt.eyJfaWQiOiI2NGY3YzBkY2ZmMzY2NmQ4YTdjMDA0MDciLCJlbWFpbCI6InVzZXJAY29ycmVvLmNvbSIsInJvbGUiOiJhZG1pbiIsImZpcnN0X25hbWUiOiJ1c2VyIiwibGFzdF9uYW1lIjoidXNlciIsImFnZSI6MzMsImNhcnQiOiI2NGY3YzBkY2ZmMzY2NmQ4YTdjMDA0MDkiLCJpYXQiOjE2OTQwNTU5OTgsImV4cCI6MTY5NDE0MjM5OH0.hIYn2frVQCVNBMGI5E4sRkTqCTBhSHQ0Th0uSOUtabc; Path=/; Expires=Fri, 06 Sep 2024 03:12:07 GMT;

  3.5 - Ten en cuenta que los tokens de las cookies expiran por lo que para realizar varios tests debes volver a loguearte y copiar y pegar el token en la cookie de Postman.
