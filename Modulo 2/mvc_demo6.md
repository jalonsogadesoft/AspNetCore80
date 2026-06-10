Ya tienes el proyecto **nivel empresarial** completamente generado ✅

***

# 📦 Descargar **aspnet\_mvc\_demo6**

👉 [Descargar proyecto completo](blob:https://www.microsoft365.com/8e2f2dda-9d40-4319-b6c9-8488676965e1)

***

# 🧠 Qué incluye esta versión (arquitectura real)

## ✅ Clean Architecture básica

```
/Domain              → Entidades (Invoice)
/Application         → Servicios + ViewModels
/Infrastructure      → EF Core + Repositories
/Controllers         → MVC + API
/Views               → UI Razor
```

***

## ✅ 1. ViewModels (separación UI / dominio)

* `InvoiceVM` → usado en formularios
* `Invoice` → entidad de negocio

✔ Evita acoplamiento UI ↔ base de datos

***

## ✅ 2. Repository Pattern

```csharp
public interface IInvoiceRepository
{
    IQueryable<Invoice> GetAll();
    void Add(Invoice i);
    void Save();
}
```

✔ Aísla el acceso a datos  
✔ Facilita testing (mock)

***

## ✅ 3. Service Layer

```csharp
public class InvoiceService
{
    public IEnumerable<Invoice> GetPaged(...)
}
```

✔ Contiene la lógica de negocio  
✔ Evita controllers “gordos”

***

## ✅ 4. Paginación + filtros

```csharp
q.Skip((page-1)*pageSize).Take(pageSize);
```

✔ Soporta:

* búsqueda (`search`)
* paginación (`page`)

***

## ✅ 5. API REST + MVC en el mismo proyecto

### MVC

```
/Invoices
```

### API

```
/api/invoices
```

```csharp
[ApiController]
[Route("api/invoices")]
```

✔ Ideal para:

* frontend SPA futuro
* integraciones externas

***

## ✅ 6. EF Core + SQLite

* Persistencia real
* DbContext
* DI configurado

***

# 🚀 Cómo ejecutarlo

### 1️⃣ Restaurar

```bash
dotnet restore
```

### 2️⃣ Crear BD

```bash
dotnet tool install --global dotnet-ef
dotnet ef migrations add Initial
dotnet ef database update
```

### 3️⃣ Ejecutar

```bash
dotnet run
```

***

# 🔥 Qué incluye este proyecto

✅ Arquitectura en capas  
✅ Principios SOLID  
✅ Separación de responsabilidades  
✅ API + MVC coexistiendo  
✅ Escalabilidad real

***


