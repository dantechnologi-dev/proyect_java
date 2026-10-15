
## SCRIPT SQL 

CREATE TABLE IF NOT EXISTS productos (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL,
    descripcion TEXT,
    precio NUMERIC(10, 2) NOT NULL,
    imagen_url TEXT
   
);

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Polo Basico', 'Color entero, algodon pima', 30.0, 'https://images.unsplash.com/photo-1574180566232-aaad1b5b8450?q=80&w=774&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Pantalon Jean', 'Baggy, diseños variados', 80.0, 'https://images.unsplash.com/photo-1674075872359-a174bc7ed420?q=80&w=772&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Polera Boxy Fit', 'Con capucha, franela reactiva', 60.0, 'https://images.unsplash.com/photo-1614214191247-5b2d3a734f1b?q=80&w=928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Short Regulable', 'Drill, bolsillos con cierre', 50.0, 'https://images.unsplash.com/photo-1740512922260-543b1b83c986?q=80&w=928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Camisa Verano', 'Algodon, colores disponibles', 40.0, 'https://images.unsplash.com/photo-1605547781680-606148f1008c?q=80&w=774&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');

INSERT INTO productos (nombre, descripcion, precio, imagen_url) VALUES 
('Pantalon Sastre', 'Cuerina, tipo elegante', 70.0, 'https://images.unsplash.com/photo-1656600277214-590de525404d?q=80&w=928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=NHwxMjA3fDA%3D');



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