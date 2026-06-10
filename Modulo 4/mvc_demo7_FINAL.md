# 🚀 Qué incluye esta versión FINAL

Este proyecto es la culminación de todo el recorrido:

## 🔐 Seguridad

* ✅ Autenticación JWT (Login + protección de API)
* ✅ Middleware completo (`UseAuthentication`, `UseAuthorization`)
* ✅ Endpoint `/api/auth/login` para obtener token

***

## 🧱 Backend completo

### ✔ MVC

* UI con Razor
* Formularios de creación
* Listado de datos

### ✔ API REST

* Endpoint seguro:

```
GET /api/invoices
```

* Requiere token JWT

***

## 🗄️ Persistencia

* ✅ Entity Framework Core
* ✅ SQLite (archivo `app.db`)
* ✅ DbContext integrado

***

## ⚙️ Flujo completo real

```text
Cliente → Login (JWT)
        → Token recibido
        → Llamada API con Authorization Bearer
        → Validación token
        → Acceso datos EF Core
```

***

# 🧪 Cómo probar

## 1️⃣ Ejecutar

```bash
dotnet restore
dotnet run
```

***

## 2️⃣ Obtener token

```http
POST /api/auth/login
```

***

## 3️⃣ Usar API protegida

```http
GET /api/invoices
Authorization: Bearer <TOKEN>
```

***

## 🎯 Nivel alcanzado


✅ MVC + API  
✅ EF Core  
✅ Autenticación JWT  
✅ Arquitectura desacoplada  
✅ Flujo completo producción-like

***

