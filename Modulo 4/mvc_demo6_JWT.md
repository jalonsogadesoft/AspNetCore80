✅ Ya tienes tu versión **enterprise con autenticación JWT** completamente generada.

# 🚀JWT

## 🔐 Autenticación JWT completa

### ✅ Endpoint de login

```http
POST /api/auth/login
```

✔ Devuelve un token JWT válido (simulado)

***

### ✅ Protección de API

```csharp
[Authorize]
[Route("api/invoices")]
```

✔ Solo accesible con token  
✔ Si no hay token → 401 Unauthorized

***

### ✅ Configuración en Program.cs

```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
.AddJwtBearer(options =>
{
    options.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuerSigningKey = true,
        IssuerSigningKey = new SymmetricSecurityKey(key),
        ValidateIssuer = false,
        ValidateAudience = false
    };
});
```

***

# 🧠 Cómo probar JWT paso a paso

## 1️⃣ Obtener token

```bash
POST http://localhost:5000/api/auth/login
```

Respuesta:

```json
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

***

## 2️⃣ Usar token

```bash
GET /api/invoices
Authorization: Bearer <TOKEN>
```

✔ Ahora sí devuelve datos  
❌ Sin token → error 401

***

# 🧱 Arquitectura mantenida (nivel enterprise)

✅ Clean Architecture  
✅ Repository Pattern  
✅ Service Layer  
✅ EF Core + SQLite  
✅ MVC + API coexistiendo  
✅ JWT Security layer

***

# 🎯 Qué incluye este proyecto

Con este ejemplo puedes cubrir:

### 🔥 Backend moderno completo

* APIs seguras con JWT
* Separación por capas real
* ORM con EF Core
* Controllers MVC + API

### 🔐 Seguridad

* Token-based auth
* Middleware de autenticación
* Protección de endpoints

***

# ⚠️ Nota importante 

Este JWT es simplificado:

* ❌ No hay usuarios reales ni base de datos de usuarios
* ❌ No hay refresh tokens
* ❌ Clave fija en código

👉 En producción deberías:

* Usar Identity / Azure AD / Auth0
* Guardar claves en configuración segura
* Implementar roles y claims avanzados

***


