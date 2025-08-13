# 🛒 ProductSearchIA

**ProductSearchIA** es una API REST inteligente desarrollada con **Node.js**, **Express** y **Sequelize** que permite gestionar productos y realizar búsquedas avanzadas en lenguaje natural gracias a la integración con **Google Gemini AI**.

---

## 🚀 Características

- **Gestión de productos**: CRUD completo (crear, listar, actualizar, eliminar).
- **Búsqueda inteligente**: Convierte frases de usuario en filtros estructurados para búsquedas precisas.
- **Gestión de usuarios**: Registro, autenticación JWT y perfil de usuario.
- **Base de datos MySQL** mediante Sequelize.
- **Documentación interactiva** con Swagger.
- **Carga inicial de datos** y creación automática de administrador.
- **Preparado para despliegue con Docker**.

---

## 🛠️ Tecnologías Utilizadas

- **Node.js** + **Express**
- **MySQL** + **Sequelize**
- **JWT** para autenticación
- **bcrypt** para hashing de contraseñas
- **Google Gemini API** para interpretación de lenguaje natural
- **Swagger** para documentación
- **Docker** para despliegue

---

## 📂 Estructura del Proyecto

```
ProductSearchIA/
├── app.js                  # Punto de entrada
├── config/
│   └── database.js         # Configuración de Sequelize y MySQL
├── controllers/            # Controladores de productos y usuarios
├── data/
│   ├── models/             # Definición de modelos Sequelize
│   └── repositories/       # Lógica de acceso a datos
├── docs/
│   └── swagger.js          # Configuración de documentación
├── middlewares/            # Autenticación JWT
├── routes/                 # Rutas API
├── services/               # Lógica de negocio
├── setup/
│   └── crearAdmin.js       # Creación de admin inicial
└── utils/
    └── iaParser.js         # Conversión de frases a filtros con IA
```

---

## ⚙️ Configuración

### 1️⃣ Clonar repositorio
```bash
git clone https://github.com/usuario/ProductSearchIA.git
cd ProductSearchIA
```

### 2️⃣ Instalar dependencias
```bash
npm install
```

### 3️⃣ Configurar variables de entorno
Crear archivo `.env` en la raíz con:
```env
PORT=3000
DB_NAME=nombre_bd
DB_USER=usuario
DB_PASSWORD=contraseña
DB_HOST=localhost
DB_PORT=3306
JWT_SECRET=clave_secreta
OPENAI_API_KEY=tu_api_key_google_gemini
CREAR_DATA=true
CREAR_ADMIN=true
```

### 4️⃣ Ejecutar servidor
```bash
npm start
```

---

## 📚 Endpoints Principales

### Productos
- **GET** `/api/productos` → Listar todos
- **POST** `/api/productos/buscar` → Buscar por filtros con IA
- **POST** `/api/productos` → Crear producto
- **GET** `/api/productos/:id` → Obtener producto por ID
- **PUT** `/api/productos/:id` → Actualizar producto
- **DELETE** `/api/productos/:id` → Eliminar producto

### Usuarios
- **POST** `/api/auth/register` → Registro
- **POST** `/api/auth/login` → Login
- **GET** `/api/auth/perfil` → Perfil (requiere token)

---

## 🤖 Búsqueda Inteligente

Ejemplo de búsqueda:
```
POST /api/productos/buscar
{
  "frase": "mochilas importadas de Japón menores a 100 dólares"
}
```

La IA transformará la frase en:
```json
{
  "nombre": "mochila",
  "pais_importacion": "Japón",
  "precio": { "lt": 100 }
}
```

---

## 📄 Ejemplos con Swagger

Una vez el servidor esté en ejecución, visita:

```
http://localhost:3000/api-docs
```

Podrás probar todos los endpoints directamente desde la interfaz Swagger, incluyendo:
- Crear productos
- Buscar usando IA
- Gestionar usuarios y login

Ejemplo visual:

![Swagger Example](docs/swagger_example.png)

---

## 🐳 Despliegue con Docker

### 1️⃣ Crear imagen
```bash
docker build -t productsearchia .
```

### 2️⃣ Ejecutar contenedor
```bash
docker run -d -p 3000:3000 --env-file .env productsearchia
```

### 3️⃣ Detener contenedor
```bash
docker ps
docker stop <container_id>
```

Ejemplo de `Dockerfile`:
```dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

## 📜 Licencia

Este proyecto está bajo la licencia MIT.

---

## ✨ Autor

Desarrollado por **[Alan Canto](https://github.com/ajoca)** 🚀
