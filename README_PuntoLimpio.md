# 🗺️ Proyecto PuntoLimpio

## Descripción
**PuntoLimpio** es una aplicación web que permite reportar y visualizar puntos de residuos en un mapa interactivo.  
Desarrollado con **NestJS (Backend)** y **React + Vite (Frontend)**, con autenticación por roles (Admin y Ciudadano).

---

## 🚀 Requisitos previos
- Node.js (v18 o superior)
- MySQL (v8 o superior)
- Git (opcional)
- Navegador actualizado

---

## 📁 Estructura del proyecto
```
/proyecto
 ├─ residuos-api/        # Servidor backend NestJS
 └─ residuos-web/        # Aplicación frontend React
```

---

## 🧩 Instalación

### 1. Base de datos MySQL
Crear base de datos y tablas:

```sql
CREATE DATABASE residuos_lima CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE residuos_lima;

CREATE TABLE roles (...);
CREATE TABLE users (...);
CREATE TABLE waste_types (...);
CREATE TABLE report_statuses (...);
CREATE TABLE reports (...);
```

Semillas básicas:

```sql
INSERT INTO roles (id,name) VALUES (1,'ciudadano'),(2,'admin');
INSERT INTO report_statuses (id,code,name) VALUES
(1,'reportado','Reportado'),
(2,'en_proceso','En proceso'),
(3,'solucionado','Solucionado');
INSERT INTO waste_types (id,name) VALUES
(1,'Basura general'),(2,'Reciclables'),(3,'Desmonte'),(4,'Orgánico'),(5,'Peligroso');
```

Usuarios demo:
```sql
INSERT INTO users (role_id,full_name,email,password_hash) VALUES
(1,'Ciudadano Demo','demo@correo.com','$2b$10$W3wF3D0f6TEa5IOnOAlTmuGqHtnk/fSRLbPTzxfQ2nJkJwHain8Ya'),
(2,'Admin General','admin@correo.com','$2b$10$W3wF3D0f6TEa5IOnOAlTmuGqHtnk/fSRLbPTzxfQ2nJkJwHain8Ya');
```

---

## ⚙️ Backend (residuos-api)

### Instalación
```bash
cd residuos-api
npm install
```

### Variables de entorno
Crear archivo `.env` en `residuos-api`:

```env
DB_HOST=127.0.0.1
DB_PORT=3306
DB_USER=root
DB_PASS=tu_contraseña
DB_NAME=residuos_lima
JWT_SECRET=super_secreto_cambialo
JWT_EXPIRES_IN=7d
```

### Ejecución
```bash
npm run start:dev
```
API en: **http://localhost:3000/api**

---

## 💻 Frontend (residuos-web)

### Instalación
```bash
cd residuos-web
npm install
```

### Configuración
Crear `.env` en `residuos-web`:

```env
VITE_API_URL=http://localhost:3000/api
```

### Ejecución
```bash
npm run dev
```
Frontend en: **http://localhost:5173**

---

## 🧠 Roles y funcionalidades

| Rol | Permisos |
|-----|-----------|
| **Ciudadano** | Ver mapa, crear reportes |
| **Admin** | Ver todos los reportes, cambiar estado |

Usuarios demo:
- Ciudadano → `demo@correo.com / 123456`
- Admin → `admin@correo.com / 123456`

---

## 🧪 Endpoints principales (API REST)

| Método | Ruta | Descripción |
|---------|------|-------------|
| POST | /auth/login | Inicia sesión |
| POST | /auth/register | Registra usuario |
| GET | /reports | Lista pública de reportes |
| GET | /reports/my | Lista reportes del usuario |
| POST | /reports | Crea nuevo reporte |
| PATCH | /reports/:id/status | Cambia estado (solo admin) |

---

## 🧭 Verificación rápida

1. API responde en `http://localhost:3000/api/reports`
2. Frontend visible en `http://localhost:5173`
3. Mapa muestra marcadores sin login
4. Login → crear reportes
5. Admin → cambiar estados

---

## 🛠 Errores comunes

| Error | Causa | Solución |
|--------|--------|-----------|
| `Access denied for user ''@'localhost'` | `.env` no leído | Revisar ConfigModule en NestJS |
| `Cannot POST /api/auth/login` | URL base incorrecta | Revisar `VITE_API_URL` o proxy Vite |
| No muestra marcadores | Endpoint público no responde | Revisar `/api/reports` |

---

## 📦 Despliegue

### Backend
```bash
npm run build
node dist/main.js
```

### Frontend
```bash
npm run build
npm run preview
```

---

## 🔐 Seguridad
- Cambia `JWT_SECRET` en producción
- Usa usuario MySQL no-root
- Configura CORS si el front está en otro dominio

---

## 👨‍💻 Autor
**Proyecto Tesis - Punto Limpio**  
Desarrollado con ❤️ por [Tu Nombre].
