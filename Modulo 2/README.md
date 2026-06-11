

# ✅ 1. Tener instalado el SDK de .NET

## ✔ Requisito imprescindible

Necesitas tener instalado el SDK (no solo runtime):

👉 Comprueba:

```bash
dotnet --version
```

Si no funciona:
👉 Descarga desde: <https://dotnet.microsoft.com/download>

***

# ✅ 2. Instalar la herramienta `dotnet-ef`

Esta es la CLI que te permite ejecutar comandos como:

```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## 🔧 Instalación global

```bash
dotnet tool install --global dotnet-ef
```

## 🔄 Actualizar (recomendado)

```bash
dotnet tool update --global dotnet-ef
```

***

## ✅ Verificar instalación

```bash
dotnet ef
```

👉 Si funciona, verás ayuda de comandos ✅

***

# ✅ 3. Instalar paquetes NuGet en tu proyecto

Dentro de tu proyecto ASP.NET necesitas estos paquetes:

```bash
dotnet add package Microsoft.EntityFrameworkCore.Tools
dotnet add package Microsoft.EntityFrameworkCore.Design
```

Y según la base de datos:

## 🔹 SQLite

```bash
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
```

## 🔹 Azure SQL / SQL Server

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

***

# ✅ 4. Tener un DbContext configurado

Ejemplo mínimo:

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Invoice> Invoices { get; set; }

    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options) { }
}
```

***

# ✅ 5. Configurar EF en Program.cs

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

***

# ✅ 6. (Muy importante) Estar en el directorio correcto

Ejecuta los comandos desde donde está el `.csproj`:

```bash
cd ruta/al/proyecto
```

***

# ✅ 7. Comandos básicos que ya deberían funcionarte

```bash
# Crear migración
dotnet ef migrations add InitialCreate

# Aplicar a base de datos
dotnet ef database update

# Ver migraciones
dotnet ef migrations list
```

***

# 🚨 Problemas típicos (muy comunes)

## ❌ “dotnet ef no se reconoce”

👉 Solución:

```bash
dotnet tool install --global dotnet-ef
```

***

## ❌ “No DbContext was found”

👉 Solución:

* Revisa que el proyecto compile
* Que tengas clase que herede de `DbContext`

***

## ❌ Problemas en proyectos múltiples

👉 Usa:

```bash
dotnet ef migrations add InitialCreate --project NombreProyecto
```

***

## ❌ No encuentra conexión

👉 Revisa:

* `appsettings.json`
* `Program.cs`

***

# 🧠 Resumen rápido

✅ Necesitas:

* .NET SDK
* `dotnet-ef` tool
* Paquetes EF Core (Tools + provider)
* DbContext configurado
* Ejecutar desde carpeta del proyecto

***


