
# 🧠 Ejemplo básico de aplicación (usando MVC)

## ✅ 1. Controllers (en vez de Minimal API)

```csharp
builder.Services.AddControllers();
```

✔ Estructura clásica  
✔ Separación de responsabilidades  
✔ Más cercano a proyectos reales

Controller incluido:

```
/Demo/mensaje
/Demo/saludo
```

***

## ✅ 2. Pipeline middleware (orden claro y didáctico)

```csharp
app.UseStaticFiles();

app.Use(async (context, next) =>
{
    Console.WriteLine("Middleware - Antes");
    await next();
    Console.WriteLine("Middleware - Después");
});

app.UseRouting();
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers();
});
```

👉 ¿Qué se ve?:

* Flujo real de la petición
* Orden de middleware
* Ejecución antes/después

***

## ✅ 3. Static Files (wwwroot)

✔ Incluye:

```
wwwroot/index.html
```

Acceso:

```
http://localhost:5000/index.html
```

👉 Concepto clave:

> ASP.NET Core también puede servir contenido estático

***

## ✅ 4. Sin redirección HTTPS (simplificado)

```csharp
// app.UseHttpsRedirection();
```

✔ La redirección https asegura que siempre se usa el canal seguro  

***

## ✅ 5. Options Pattern (configuración clara)

```csharp
builder.Services.Configure<DemoOptions>(
    builder.Configuration.GetSection("DemoOptions"));
```

Uso en controller:

```csharp
_options.Mensaje
```

***

## ✅ 6. Inyección de dependencias (DI)

```csharp
builder.Services.AddSingleton<IServicioSaludo, ServicioSaludo>();
```

Uso:

```csharp
_servicio.Saludar();
```

***

# 🧪 Cómo usarlo

## 1️⃣ Ejecutar

```bash
dotnet run
```

***

## 2️⃣ Probar en navegador

### API (Controllers)

* <http://localhost:5000/Demo/mensaje>
* <http://localhost:5000/Demo/saludo>

***

### Static file

* <http://localhost:5000/index.html>

***

## 3️⃣ Ver consola

```
Middleware - Antes
Middleware - Después
```

👉 Se comprueba como funciona la Middleware

***

# 🎯 ¿Qué incluye el proyecto?


✅ Arquitectura real ASP.NET Core  
✅ Controllers vs Minimal API  
✅ Pipeline middleware  
✅ DI (inyección de dependencias)  
✅ Options Pattern  
✅ Static files  
✅ Orden de ejecución

***

# 🧠 Resumen

1. **Builder**
   → configura servicios

2. **Services**
   → DI + Options

3. **Pipeline**
   → Middleware

4. **Endpoints**
   → Controllers

5. **Extras**
   → static files

***

# 💡 Frase clave

> “Una aplicación ASP.NET Core = Servicios + Middleware + Endpoints”

***

