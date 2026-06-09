
## 📊 Orden REAL de prioridad en ASP.NET Core

(de menor a mayor prioridad):

1. `appsettings.json`
2. `appsettings.{Environment}.json`
3. **User Secrets** (solo Development)
4. **Variables de entorno**
5. (opcional) Command line

👉 **Regla de oro:**

> “La última fuente en cargarse gana” 

***

# 📦 Qué incluye este ejemplo

El proyecto ya está preparado para demostrar:

✅ appsettings  
✅ appsettings.Development  
✅ user secrets  
✅ variables de entorno  
✅ endpoint para ver qué valor ha ganado

***

# 🔥 Código clave

## Program.cs 

```csharp
var builder = WebApplication.CreateBuilder(args);

// =====================================
// CONFIGURACIÓN AUTOMÁTICA
// =====================================
// ASP.NET Core ya carga automáticamente:
//
// 1. appsettings.json
// 2. appsettings.Development.json
// 3. User Secrets (si Development)
// 4. Variables de entorno
//
// NO hace falta añadirlos manualmente 
//
// =====================================

// Binding fuertemente tipado
builder.Services.Configure<DemoSettings>(
    builder.Configuration.GetSection("Demo"));

var app = builder.Build();

// Endpoint para ver el valor final
app.MapGet("/config", (IConfiguration config) =>
{
    return Results.Text(config["Demo:Valor"] ?? "null");
});

// Endpoint con Options
app.MapGet("/options", (IOptions<DemoSettings> opt) =>
{
    return Results.Json(opt.Value);
});

app.Run();

// Clase de configuración
public class DemoSettings
{
    public string? Valor { get; set; }
}
```

***

# 🧪 Escenario guiado 

## 1️⃣ Valor base (appsettings.json)

```json
"Demo": {
  "Valor": "appsettings"
}
```

👉 Resultado:

```
/config → appsettings
```

***

## 2️⃣ Override con appsettings.Development.json

```json
"Demo": {
  "Valor": "development"
}
```

👉 Resultado:

```
/config → development
```

***

## 3️⃣ Añadir User Secret

```bash
dotnet user-secrets set "Demo:Valor" "secret"
```

👉 Resultado:

```
/config → secret
```

✔  **sobrescribe los JSON**

***

## 4️⃣ Variable de entorno (máxima prioridad)

```bash
set Demo__Valor=env   (Windows)
export Demo__Valor=env (Linux/Mac)
```

👉 Resultado:

```
/config → env
```



***

# 🎯 Conclusiones

## ✅ 1. No se cambia código para cambiar configuración

* Todo externo
* Ideal para DevOps

***

## ✅ 2. Separación total

| Tipo               | Ubicación               |
| ------------------ | ----------------------- |
| Config normal      | appsettings             |
| Config por entorno | appsettings.Development |
| Secretos           | user secrets            |
| Producción         | env vars                |

***

## ✅ 3. Jerarquía real 

```text
appsettings < environment json < secrets < env vars
```

***
