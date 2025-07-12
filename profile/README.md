# 🌱 AgroWeb - Plataforma de Productos Agropecuarios

## 📋 Descripción del Proyecto

**AgroWeb** es una plataforma web completa para la gestión y comercialización de productos agropecuarios colombianos, desarrollada con arquitectura de microservicios moderna y tecnologías escalables.

### 🎯 Objetivo Principal
Facilitar la conexión entre productores agrícolas y consumidores finales mediante una plataforma digital robusta, segura y fácil de usar.

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                    🌐 Frontend (React)                      │
│                 http://localhost:5173                      │
└─────────────────────┬───────────────────────────────────────┘
                      │
          ┌───────────┴───────────┐
          │                       │
     ┌────▼────┐             ┌────▼────┐
     │🥕 API   │             │👥 API   │
     │Productos│             │Usuarios │
     │:5000    │             │:5001    │
     └────┬────┘             └────┬────┘
          │                       │
     ┌────▼────┐             ┌────▼────┐
     │Cassandra│             │ Pandas  │
     │ Docker  │             │DataFrame│
     │ :9042   │             │(Memory) │
     └─────────┘             └─────────┘
```

## 🛠️ Stack Tecnológico

### � Frontend
- **Framework**: React 18 con TypeScript
- **Estilos**: Tailwind CSS
- **Build Tool**: Vite
- **Estado**: React Hooks + Context API
- **HTTP**: Fetch API nativo
- **Ruteo**: React Router (si aplicable)

### 🔧 Backend - Servicio de Productos
- **Lenguaje**: Python 3.11
- **Framework**: Flask
- **Base de Datos**: Apache Cassandra (NoSQL)
- **Arquitectura**: Clean Architecture
- **Documentación**: Swagger/OpenAPI
- **Containerización**: Docker + Docker Compose
- **Variables de Entorno**: python-dotenv

### 👥 Backend - Servicio de Usuarios
- **Lenguaje**: Python 3.8+
- **Framework**: Flask
- **Almacenamiento**: Pandas DataFrame (en memoria)
- **Arquitectura**: Clean Architecture
- **Documentación**: Swagger/OpenAPI
- **Autenticación**: Básica con validación de credenciales

### 🗄️ Bases de Datos
- **Productos**: Cassandra - NoSQL distribuida para alta escalabilidad
- **Usuarios**: Pandas DataFrame - Solución en memoria para prototipado rápido

## ✨ Características Principales

### 📦 Gestión de Productos
- ✅ **CRUD Completo**: Crear, leer, actualizar, eliminar productos
- ✅ **Categorización**: Organización por tipos de productos agrícolas
- ✅ **Inventario**: Control de stock y disponibilidad
- ✅ **Metadatos**: Precio, origen, descripciones detalladas
- ✅ **Imágenes**: Soporte para URLs de imágenes de productos
- ✅ **Filtros**: Por categoría, disponibilidad, precio
- ✅ **IDs Auto-generados**: UUID para identificación única

### 👤 Gestión de Usuarios
- ✅ **Registro**: Creación de cuentas de usuario
- ✅ **Autenticación**: Login con email y contraseña
- ✅ **Perfiles**: Información personal y de contacto
- ✅ **Validación**: Verificación de datos de entrada
- ✅ **Consultas**: Búsqueda por documento o email

### 🎨 Interfaz de Usuario
- ✅ **Responsive Design**: Adaptable a móviles y escritorio
- ✅ **Catálogo Dinámico**: Visualización de productos desde API
- ✅ **Filtros Interactivos**: Por categoría con actualización en tiempo real
- ✅ **Cards de Producto**: Información visual completa
- ✅ **Estado de Carga**: Indicadores de loading y errores
- ✅ **Formularios**: Registro y login de usuarios

## 🔒 Seguridad y Configuración

### 🛡️ Medidas de Seguridad
- **Variables de Entorno**: Configuración sensible externalizada
- **CORS Configurado**: Solo permite frontend autorizado
- **Debug Mode**: Deshabilitado para producción
- **Host Binding**: Restringido a localhost
- **Validación de Entrada**: En todos los endpoints
- **Manejo de Errores**: Respuestas consistentes y seguras

### ⚙️ Configuración de Entorno
- **Desarrollo**: Configuración optimizada para desarrollo local
- **Producción**: Variables de entorno para deployment
- **Docker**: Contenedores para dependencias externas
- **Logging**: Configuración de logs por nivel

## 📊 Datos y Esquemas

### 🥕 Modelo de Producto
```json
{
  "productId": "uuid-auto-generado",
  "name": "Nombre del producto",
  "description": "Descripción detallada",
  "category": "Categoría (Frutas, Verduras, etc.)",
  "price": 1500.0,
  "originalPrice": 2000.0,
  "stock": 100,
  "unit": "kg",
  "origin": "Región de origen",
  "imageUrl": "URL de la imagen",
  "isOrganic": true,
  "isBestSeller": false,
  "freeShipping": true,
  "isActive": true,
  "createdAt": "timestamp"
}
```

### 👤 Modelo de Usuario
```json
{
  "numberDocument": "123456789",
  "typeDocument": "CC",
  "firstName": "Nombre",
  "middleName": "Segundo nombre",
  "surName1": "Apellido paterno",
  "surName2": "Apellido materno",
  "username": "usuario",
  "bornDate": "1990-01-01",
  "department": "Departamento",
  "municipality": "Municipio",
  "trail": "Dirección",
  "email": "email@dominio.com",
  "phoneNumber": "+57300000000",
  "age": 30,
  "hashPassword": "contraseña"
}
```

## 🚀 Guía de Instalación y Ejecución

### 📋 Prerequisitos
- **Anaconda/Miniconda** (Python 3.11 para productos)
- **Python 3.8+** (para usuarios)
- **Node.js 18+** (para frontend)
- **Docker Desktop** (para Cassandra)

### ⚡ Inicio Rápido

1. **Configurar Entorno de Productos**
```bash
conda create -n agroweb python=3.11 -y
conda activate agroweb
conda install cassandra-driver -y
cd Serv_GestionProductos
pip install -r requirements.txt
```

2. **Configurar Servicio de Usuarios**
```bash
cd Serv_Usuarios
pip install -r requirements.txt
```

3. **Configurar Frontend**
```bash
cd FrontEnd
npm install
```

4. **Iniciar Base de Datos**
```bash
cd Serv_GestionProductos
docker-compose up -d
```

5. **Ejecutar Servicios** (en terminales separadas)
```bash
# Terminal 1 - Productos
conda activate agroweb && cd Serv_GestionProductos && python app.py

# Terminal 2 - Usuarios  
cd Serv_Usuarios && python app.py

# Terminal 3 - Frontend
cd FrontEnd && npm run dev
```

### 🌐 URLs de Acceso
- **Frontend**: http://localhost:5173
- **API Productos**: http://localhost:5000
- **API Usuarios**: http://localhost:5001
- **Swagger Productos**: http://localhost:5000/swagger
- **Swagger Usuarios**: http://localhost:5001/swagger

## 🧪 Testing y Desarrollo

### 🔬 Pruebas de API
El proyecto incluye scripts de prueba automatizados:
- `Serv_GestionProductos/test_products.py`
- `Serv_GestionProductos/populate_database.py` (datos de prueba)

### 📚 Documentación
- **Swagger UI**: Documentación interactiva de APIs
- **README**: Guías detalladas en cada servicio
- **CHANGELOG**: Historial de cambios y versiones

### 🔧 Desarrollo
- **Arquitectura Limpia**: Separación clara de responsabilidades
- **Código Modular**: Fácil mantenimiento y extensión
- **Variables de Entorno**: Configuración flexible
- **Logging**: Trazabilidad de operaciones

## 📈 Escalabilidad y Futuro

### 🎯 Características Planificadas
- Autenticación JWT para usuarios
- Sistema de roles y permisos
- Carrito de compras y pagos
- Notificaciones en tiempo real
- Sistema de reviews y ratings
- Panel administrativo
- API Gateway para microservicios

### 🏗️ Arquitectura Escalable
- **Microservicios**: Separación de responsabilidades
- **NoSQL**: Cassandra para escalabilidad horizontal
- **Containerización**: Docker para deployment
- **API REST**: Interfaces estándar
- **Frontend Desacoplado**: SPA independiente

## 👥 Equipo de Desarrollo

Proyecto desarrollado como trabajo de Ingeniería de Software 2, implementando buenas prácticas de desarrollo, arquitectura limpia y tecnologías modernas.

---

**🌱 AgroWeb - Conectando el campo con la tecnología** 🚀

*Para instrucciones detalladas de instalación y ejecución, consultar el README.md principal en la carpeta Workspace_Config.*
