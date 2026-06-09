
## 📁 Configuración por entorno

* `appsettings.json` → configuración base
* `appsettings.Development.json` → override en desarrollo
* `appsettings.Production.json` → override en producción

***


## 1️⃣ Entorno actual en tiempo real

Endpoint:

```
/env
```

Devuelve:

```json
{
  "Entorno": "Development",
  "EsDevelopment": true,
  "EsProduction": false
}
```

***

## 2️⃣ Comportamiento distinto según entorno

Endpoint:

```
/mensaje
```

### En Development:

```
[DEV] Mensaje de Development - Información detallada para desarrollo
```

### En Production:

```
[PROD] Mensaje de Production
```

👉 Misma API, comportamiento distinto

***

## 3️⃣ Middleware condicionado por entorno

```csharp
if (app.Environment.IsDevelopment())
{
    app.Use(async (context, next) =>
    {
        Console.WriteLine("Middleware SOLO en Development");
        await next();
    });
}
```

✔ Solo se ejecuta en Development  
✔ Ejemplo de buenas prácticas

***

# 🧪 Cómo usarlo en el ejemplo

## 🔹 Paso 1 – Ejecutar en Development (por defecto)

```bash
dotnet run
```

👉 Ver:

* `/env`
* `/mensaje`

***

## 🔹 Paso 2 – Cambiar a Production

### Windows:

```bash
set ASPNETCORE_ENVIRONMENT=Production
dotnet run
```

### Linux / Mac:

```bash
export ASPNETCORE_ENVIRONMENT=Production
dotnet run
```

👉 Ver cómo cambia TODO:

* Configuración
* Mensaje
* Middleware

***

# 🎯 Conceptos clave

✅ Sistema de entornos en ASP.NET Core  
✅ Archivos `appsettings.{Environment}.json`  
✅ Uso de `IHostEnvironment`  
✅ Buenas prácticas:

* logs en dev
* menos info en producción

***

# 💡 Conclusión

> “No cambias el código para cambiar el comportamiento…  
> cambias el entorno”

***

