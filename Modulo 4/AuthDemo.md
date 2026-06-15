Updated todo list

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
$base = "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3"
dotnet new mvc -n AuthDemo -o "$base\AuthDemo" --framework net8.0
Write-Host "Proyecto creado"

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
$base = "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3"
dotnet new mvc -n AuthDemo -o "$base\AuthDemo" --framework net8.0
Write-Host "Proyecto creado"

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
$base = "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
cd $base

# Agregar paquetes NuGet
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer --version 8.0.0
dotnet add package System.IdentityModel.Tokens.Jwt --version 7.7.1
dotnet add package Microsoft.AspNetCore.Cryptography.KeyDerivation --version 8.0.0

# Crear estructura de carpetas
@("Models\Enums","Models\ViewModels","Authorization\Requirements","Authorization\Handlers",
  "Services","Controllers","Views\Account","Views\Dashboard","Views\Admin",
  "Views\Reports","Views\HR","Views\Token") | ForEach-Object {
    New-Item -ItemType Directory -Path "$base\$_" -Force | Out-Null
}
Write-Host "Paquetes instalados y directorios creados"

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
$base = "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
cd $base

# Agregar paquetes NuGet
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer --version 8.0.0
dotnet add package System.IdentityModel.Tokens.Jwt --version 7.7.1
dotnet add package Microsoft.AspNetCore.Cryptography.KeyDerivation --version 8.0.0

# Crear estructura de carpetas
@("Models\Enums","Models\ViewModels","Authorization\Requirements","Authorization\Handlers",
  "Services","Controllers","Views\Account","Views\Dashboard","Views\Admin",
  "Views\Reports","Views\HR","Views\Token") | ForEach-Object {
    New-Item -ItemType Directory -Path "$base\$_" -Force | Out-Null
}
Write-Host "Paquetes instalados y directorios creados"

Ahora creo todos los archivos en paralelo — empezando por modelos, enums y constantes:
````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````
Ahora los Requirements y Handlers de autorización:
````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````
Ahora los servicios (password hasher, user store, JWT):
````

````

````

````

````

````
Ahora los controladores:
````

````

````

````

````

````

````

````

````

````

````

````
Ahora `Program.cs` con toda la configuración de autenticación y autorización, y `appsettings.json`:

Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/appsettings.json)

Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/Program.cs)


````

````

````

````
Ahora las vistas. Empiezo con el layout y las vistas más importantes en paralelo:

Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/Views/Shared/_Layout.cshtml)


````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````

````
Ahora actualizamos `_ViewImports.cshtml` y la Home page:

Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/Views/Home/Index.cshtml)

Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/Views/_ViewImports.cshtml)


````

````

````

````


Read [](file:///c%3A/Users/josem/Documents/Gadesoft/Ministerio%20de%20hacienda/Desarrollo%20en%20C%23/Documentacion/Modulo%203/AuthDemo/wwwroot/css/site.css)


````

````
Compilamos:

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
cd "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
dotnet build --configuration Release 2>&1

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
cd "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
dotnet build --configuration Release 2>&1

✅ Compilación correcta. Arrancamos la app y verificamos:

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
cd "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
dotnet run --configuration Release 2>&1

Ran terminal command: $env:PATH = "C:\Program Files\dotnet;" + $env:PATH
cd "C:\Users\josem\Documents\Gadesoft\Ministerio de hacienda\Desarrollo en C#\Documentacion\Modulo 3\AuthDemo"
dotnet run --configuration Release 2>&1



Ran terminal command: # 1. Home page
$home = Invoke-WebRequest "http://localhost:5297" -UseBasicParsing
"Home: $($home.StatusCode)"

# 2. Login page (sin autenticar)
$login = Invoke-WebRequest "http://localhost:5297/Account/Login" -UseBasicParsing
"Login: $($login.StatusCode)"

# 3. Dashboard redirige a login (no autenticado)
$dash = Invoke-WebRequest "http://localhost:5297/Dashboard" -UseBasicParsing -MaximumRedirection 0 -ErrorAction SilentlyContinue
"Dashboard sin auth: $($dash.StatusCode) (esperado 302)"

# 4. API token endpoint — obtener JWT
$body = '{"email":"admin@demo.es","password":"Demo1234!"}'
$token = Invoke-WebRequest "http://localhost:5297/api/token" `
    -Method Post -Body $body `
    -ContentType "application/json" -UseBasicParsing
"API Token: $($token.StatusCode)"
$json = $token.Content | ConvertFrom-Json
"Token (primeros 60 chars): $($json.token.Substring(0,60))..."
"Rol del usuario: $($json.user.role)"

Ran terminal command: # 1. Home page
$home = Invoke-WebRequest "http://localhost:5297" -UseBasicParsing
"Home: $($home.StatusCode)"

# 2. Login page (sin autenticar)
$login = Invoke-WebRequest "http://localhost:5297/Account/Login" -UseBasicParsing
"Login: $($login.StatusCode)"

# 3. Dashboard redirige a login (no autenticado)
$dash = Invoke-WebRequest "http://localhost:5297/Dashboard" -UseBasicParsing -MaximumRedirection 0 -ErrorAction SilentlyContinue
"Dashboard sin auth: $($dash.StatusCode) (esperado 302)"

# 4. API token endpoint — obtener JWT
$body = '{"email":"admin@demo.es","password":"Demo1234!"}'
$token = Invoke-WebRequest "http://localhost:5297/api/token" `
    -Method Post -Body $body `
    -ContentType "application/json" -UseBasicParsing
"API Token: $($token.StatusCode)"
$json = $token.Content | ConvertFrom-Json
"Token (primeros 60 chars): $($json.token.Substring(0,60))..."
"Rol del usuario: $($json.user.role)"

Todo funciona perfectamente. Verificamos también el endpoint `/api/token/me` con el JWT:

Ran terminal command: $body = '{"email":"gerente.rrhh@demo.es","password":"Demo1234!"}'
$resp = Invoke-WebRequest "http://localhost:5297/api/token" -Method Post -Body $body -ContentType "application/json" -UseBasicParsing
$jwt = ($resp.Content | ConvertFrom-Json).token

$me = Invoke-WebRequest "http://localhost:5297/api/token/me" `
    -Headers @{Authorization = "Bearer $jwt"} -UseBasicParsing
$claims = ($me.Content | ConvertFrom-Json).claims
"Claims del Gerente RRHH:"
$claims | Where-Object { $_.type -in @("email","http://schemas.microsoft.com/ws/2008/06/identity/claims/role","department","employee_status","age","hire_date") } |
    ForEach-Object { "  [$($_.type.Split('/')[-1])] = $($_.value)" }

Ran terminal command: $body = '{"email":"gerente.rrhh@demo.es","password":"Demo1234!"}'
$resp = Invoke-WebRequest "http://localhost:5297/api/token" -Method Post -Body $body -ContentType "application/json" -UseBasicParsing
$jwt = ($resp.Content | ConvertFrom-Json).token

$me = Invoke-WebRequest "http://localhost:5297/api/token/me" `
    -Headers @{Authorization = "Bearer $jwt"} -UseBasicParsing
$claims = ($me.Content | ConvertFrom-Json).claims
"Claims del Gerente RRHH:"
$claims | Where-Object { $_.type -in @("email","http://schemas.microsoft.com/ws/2008/06/identity/claims/role","department","employee_status","age","hire_date") } |
    ForEach-Object { "  [$($_.type.Split('/')[-1])] = $($_.value)" }



✅ Todo funciona correctamente. Aquí el resumen completo:

---

## ✅ Proyecto `AuthDemo` — ASP.NET Core 8.0 MVC

**Ruta:** `Modulo 3\AuthDemo`  
**Ejecutar:** `dotnet run` → `http://localhost:5297`  
**Contraseña de todos los usuarios semilla:** `Demo1234!`

---

### 📁 Estructura generada

```
AuthDemo/
├── Models/
│   ├── ApplicationUser.cs         ← Usuario personalizado (sin Identity)
│   ├── Enums/ (UserRole, Department, UserStatus)
│   └── ViewModels/ (Login, Register, Profile, AdminUserList)
├── Authorization/
│   ├── Policies.cs                ← Constantes de nombres de políticas + AppClaims
│   ├── Requirements/              ← 4 IAuthorizationRequirement
│   └── Handlers/                  ← 4 AuthorizationHandler con distintos patrones
├── Services/
│   ├── PasswordHasher.cs          ← PBKDF2-HMAC-SHA256 con salt aleatorio
│   ├── UserService.cs             ← Repositorio en memoria con 7 usuarios semilla
│   └── JwtService.cs             ← Emisión y validación de JWT
├── Controllers/
│   ├── AccountController.cs       ← Registro, Login, Logout, Perfil
│   ├── DashboardController.cs     ← [Authorize(Policy="ActiveEmployee")]
│   ├── AdminController.cs         ← [Authorize(Roles="Administrador")]
│   ├── ReportsController.cs       ← [Authorize(Policy="CanAccessFinanceReports")]
│   ├── HRController.cs            ← [Authorize(Policy="ActiveHR")]
│   └── TokenController.cs         ← API: POST /api/token, GET /api/token/me
└── Views/ (Login, Register, AccessDenied, Profile, Dashboard, Admin, Reports, HR)
```

---

### 🔐 Escenarios de autorización

| Política | Mecanismo | Descripción |
|----------|-----------|-------------|
| `RequireAdmin` | `RequireRole` | Solo rol Administrador |
| `HROnly` | `DepartmentRequirement` + handler | Claim `department = RecursosHumanos` |
| `MinimumAge18` | `MinimumAgeRequirement(18)` + handler | Claim `age ≥ 18` |
| `SeniorStaff` | `RequireRole` múltiple | Administrador o Gerente |
| `CanAccessFinanceReports` | `FinanceReportHandler` | Lógica **OR**: Admin, o Gerente+Finanzas+Activo |
| `ActiveEmployee` | `ActiveEmployeeRequirement` + `context.Fail()` | Bloquea si estado ≠ Activo |
| `ActiveHR` | **2 requisitos en AND** | Activo + RRHH simultáneamente |

### 🎟️ Claims en el JWT

**Estándar RFC 7519:** `sub`, `email`, `unique_name`, `jti`, `iat`, `nbf`, `exp`, `iss`, `aud`  
**Personalizados:** `role`, `employee_id`, `full_name`, `department`, `age`, `employee_status`, `hire_date`

### 🔑 Cuentas de prueba

| Email | Rol | Departamento | Acceso especial |
|-------|-----|--------------|-----------------|
| `admin@demo.es` | Administrador | Tecnología | Todo |
| `gerente.rrhh@demo.es` | Gerente | RRHH | Dashboard, Informes |
| `gerente.fin@demo.es` | Gerente | Finanzas | Dashboard, **Informes** |
| `rrhh@demo.es` | RRHH | RRHH | Dashboard, **Módulo RRHH** |
| `auditor@demo.es` | Auditor | Finanzas | Dashboard |
| `empleado@demo.es` | Empleado | Marketing | Solo Dashboard |
| `bloqueado@demo.es` | Empleado | Operaciones | ❌ Bloqueado (fallo `ActiveEmployee`) |
