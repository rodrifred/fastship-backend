# FastShip API - Gestión de Envíos

## Descripción

FastShip API es un backend desarrollado con Express.js y MongoDB para la gestión de envíos de paquetes. El sistema permite registrar nuevos envíos, consultar información, actualizar estados y eliminar registros mediante una API REST.

Este proyecto fue desarrollado como parte de una actividad académica para aplicar conceptos de Express, MongoDB y Mongoose siguiendo una arquitectura basada en rutas, controladores y modelos.

---

## Tecnologías utilizadas

* Node.js
* Express.js
* MongoDB
* Mongoose
* Dotenv
* Cors
* Nodemon

---

## Requisitos

Antes de ejecutar el proyecto es necesario tener instalado:

* Node.js v20.19.0 o superior
* MongoDB Local o MongoDB Atlas
* Git
* Postman o Insomnia para pruebas

---

## Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/rodrifred/fastship-backend.git
cd fastship-backend
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Configurar variables de entorno

Crear un archivo `.env` en la raíz del proyecto:

```env
PORT=3000
MONGODB_URI=mongodb+srv://USUARIO:CONTRASENA@HOST/raguilar-fastship
```

### 4. Ejecutar el proyecto

```bash
npm run dev
```

El servidor estará disponible en:

```text
http://localhost:3000
```

---

## Seguridad de las variables de entorno

El archivo `.env` no se incluye en el repositorio
porque contiene las credenciales de MongoDB Atlas.

Se proporciona un archivo `.env.example` como
referencia para configurar la conexión.

Ejemplo de `.env.example`:

```env
PORT=3000
MONGODB_URI=TU_CADENA_DE_CONEXION
```

---

## Estructura del proyecto

```text
src/
│
├── config/
│   └── db.js
│
├── controllers/
│   └── envio.controller.js
│
├── models/
│   └── envio.model.js
│
├── routes/
│   └── envios.route.js
│
└── app.js
```

---

## Modelo de datos

Cada envío contiene la siguiente información:

```json
{
  "pedidoId": "PED001",
  "remitente": "Carlos Ramos",
  "destinatario": "Ana Torres",
  "direccionEntrega": "Av. Los Incas 123",
  "estado": "pendiente"
}
```

Estados permitidos:

* pendiente
* en tránsito
* entregado

---

# Endpoints de la API

## Crear un envío

### POST

```http
/api/envios
```

### Body

```json
{
  "pedidoId": "PED001",
  "remitente": "Carlos Ramos",
  "destinatario": "Ana Torres",
  "direccionEntrega": "Av. Los Incas 123",
  "estado": "pendiente"
}
```

### Respuesta

```json
{
  "_id": "6857ab1234",
  "pedidoId": "PED001",
  "remitente": "Carlos Ramos",
  "destinatario": "Ana Torres",
  "direccionEntrega": "Av. Los Incas 123",
  "estado": "pendiente"
}
```

---

## Obtener todos los envíos

### GET

```http
/api/envios
```

---

## Obtener envíos activos

### GET

```http
/api/envios/activos
```

Retorna únicamente los envíos cuyo estado sea:

* pendiente
* en tránsito

---

## Buscar envío por ID

### GET

```http
/api/envios/:id
```

Ejemplo:

```http
/api/envios/6857ab1234
```

---

## Actualizar un envío

### PUT

```http
/api/envios/:id
```

### Body

```json
{
  "estado": "entregado"
}
```

También es posible actualizar múltiples campos:

```json
{
  "destinatario": "Juan Pérez",
  "direccionEntrega": "Av. Perú 555",
  "estado": "en tránsito"
}
```

---

## Eliminar un envío

### DELETE

```http
/api/envios/:id
```

---

# Pruebas con Postman

1. Registrar un envío mediante POST (201 Created).
2. Listar todos los envíos mediante GET (200 OK).
3. Consultar los envíos activos mediante GET (200 OK).
4. Buscar un envío por su ID mediante GET (200 OK).
5. Actualizar el estado mediante PUT (200 OK).
6. Eliminar un envío mediante DELETE (200 OK).

Las seis pruebas se realizaron correctamente,
comprobando el funcionamiento de la API REST
y su conexión con MongoDB Atlas.

---

# Manejo de errores

La API implementa:

* Validación de campos obligatorios.
* Validación de estados permitidos mediante `enum`.
* Respuestas HTTP apropiadas.
* Bloques `try/catch`.
* Verificación de existencia antes de actualizar o eliminar registros.

---

# Justificación técnica

## Uso de MongoDB

MongoDB permite almacenar la información de cada envío como un documento independiente, facilitando la flexibilidad del modelo de datos y la escalabilidad del sistema.

## Uso de Mongoose

Mongoose simplifica la interacción con MongoDB mediante esquemas, validaciones y modelos orientados a objetos.

## Uso de Controladores

La lógica de negocio se separa de las rutas para mejorar la mantenibilidad, legibilidad y escalabilidad del proyecto.

## Uso de Rutas

Las rutas permiten exponer endpoints específicos para cada operación CRUD siguiendo los principios REST.

---

# Conclusiones

1. La implementación de Express junto con MongoDB permitió desarrollar una API REST funcional para gestionar envíos de manera eficiente y organizada.

2. La separación entre rutas, controladores y modelos facilita el mantenimiento del código y permite escalar el proyecto de forma más sencilla.

3. El uso de Mongoose ayudó a validar los datos y reducir errores al momento de interactuar con la base de datos.

4. El manejo adecuado de errores y validaciones mejora la seguridad y la experiencia de uso de la API.

5. Seguir una arquitectura organizada desde el inicio permite desarrollar aplicaciones backend más robustas y fáciles de mantener.
