

## ⚙️ Paso 1: Configurar Variables de Entorno (`.env`)

Crea un archivo llamado `.env` en la raíz del proyecto (al mismo nivel del archivo `pom.xml`) tomando como referencia `.env.example`:

```env
# Puerto en el que se levantará la aplicación (por defecto: 8080)
PORT=8080

# Credenciales de conexión a PostgreSQL
DB_URL=jdbc:postgresql://host:puerto/nombre_base_datos?sslmode=require
DB_USER=tu_usuario
DB_PASSWORD=tu_contraseña
```

> [!NOTE]
> La aplicación carga automáticamente este archivo `.env` al iniciar gracias a un procesador de entorno personalizado (`EnvEnvironmentPostProcessor`).

---

## 🗄️ Paso 2: Estructura de la Base de Datos

La aplicación mapea la entidad `Product` con la tabla **`productos`**, compuesta por los siguientes 5 campos:

| Campo | Tipo en BD | Descripción |
| :--- | :--- | :--- |
| `id` | `BIGINT` / `SERIAL` | Identificador único autoincremental (Clave primaria). |
| `nombre` | `VARCHAR` | Nombre o título del producto. |
| `descripcion` | `VARCHAR` | Descripción detallada del producto. |
| `precio` | `NUMERIC` / `DOUBLE` | Precio unitario del producto. |
| `imagen_url` | `VARCHAR` | Enlace URL a la imagen del producto. |

---

## 🚀 Paso 3: Compilar y Ejecutar el Proyecto

Abre una terminal en la carpeta raíz del proyecto y ejecuta:

### 1. Compilar y verificar dependencias:
```bash
mvn clean compile
```

### 2. Iniciar la aplicación:
```bash
mvn spring-boot:run
```

Cuando veas un mensaje similar a:
```text
Started DemoApplication in X.XXX seconds (process running for ...)
```
la aplicación estará lista y escuchando peticiones en el puerto configurado (ej. `8080`).

---

## 🌐 Paso 4: Visualización y Pruebas

Una vez iniciada la aplicación, puedes interactuar con ella a través de:

### 1. Interfaz Interactiva (Swagger UI) 🌟
Abre en tu navegador:
👉 **[http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)**
*(o también [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html))*

Desde Swagger puedes consultar, crear, modificar y eliminar productos haciendo clic en **"Try it out"** y luego en **"Execute"**.

### 2. Documentación OpenAPI (JSON crudo)
👉 **[http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)**

---

## 📡 Endpoints de la API REST

Ruta base: `/products`

| Método | Endpoint | Descripción | Código Éxito |
| :--- | :--- | :--- | :--- |
| **GET** | `/products` | Obtiene la lista completa de productos | `200 OK` |
| **GET** | `/products/{id}` | Obtiene los detalles de un producto por su ID | `200 OK` / `404 Not Found` |
| **POST** | `/products` | Registra un nuevo producto | `201 Created` |
| **PUT** | `/products/{id}` | Actualiza los datos de un producto existente | `200 OK` / `404 Not Found` |
| **DELETE**| `/products/{id}` | Elimina un producto por su ID | `204 No Content` / `404 Not Found` |

### Ejemplo de JSON para `POST /products` o `PUT /products/{id}`:
```json
{
  "nombre": "Camiseta Deportiva",
  "descripcion": "Camiseta 100% poliéster transpirable",
  "precio": 24.99,
  "imagen_url": "https://images.unsplash.com/photo-1521572267360-ee0c2909d518"
}
```

---

## 🛑 Detener la Aplicación

Para detener el servidor en ejecución, dirígete a la terminal donde ejecutaste el comando y presiona:
```bash
Ctrl + C
```