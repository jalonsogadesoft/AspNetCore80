
# 🚀 Qué incluye esta versión FULL (nivel empresa real)


## 🧠 ✅ Arquitectura por capas completa

```
/Domain
   ├── Entities
   ├── Interfaces

/Application
   ├── Services
   ├── ViewModels

/Infrastructure
   ├── Data (DbContext)
   ├── Repositories

/Controllers
/Views
```

👉 Esta separación permite desacoplar lógica, datos y UI, esencial en aplicaciones grandes [\[bing.com\]](https://bing.com/search?q=asp+net+core+repository+pattern+service+layer+example+EF+Core+code+first+multiple+tables)

***

## ✅ Modelo complejo real (relaciones)

### 👤 Customer

* 1 → N Invoices

### 🧾 Invoice

* Relaciona:
  * Cliente
  * Productos (N:M)

### 📦 Product

* N → M con facturas

### 🔗 InvoiceProduct (tabla intermedia)

👉 Las relaciones N:M requieren tabla intermedia en EF Core [\[learn.microsoft.com\]](https://learn.microsoft.com/en-us/ef/core/modeling/relationships/many-to-many)

***

## ✅ Repository Pattern (GENÉRICO)

```csharp
public interface IRepository<T>
{
    Task<IEnumerable<T>> GetAllAsync();
    Task<T> GetByIdAsync(int id);
    Task AddAsync(T entity);
    void Update(T entity);
    void Delete(T entity);
}
```

✔ Abstrae acceso a datos  
✔ Mejora mantenibilidad y testabilidad [\[dotnettutorials.net\]](https://dotnettutorials.net/lesson/repository-design-pattern-in-asp-net-core-mvc/)

***

## ✅ Service Layer (negocio)

```csharp
public class InvoiceService
{
    private readonly IRepository<Invoice> _repo;

    public async Task<IEnumerable<Invoice>> GetAllAsync()
```

✔ Controllers limpios  
✔ Lógica centralizada

***

## ✅ CRUD completo

* Customers ✔
* Products ✔
* Invoices ✔
* Relación Invoice-Product ✔

***

## ✅ Azure SQL + EF Core Code First

Configurado en:

```csharp
options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection"))
```

👉 EF Core creará la base de datos desde el modelo

***

## ✅ ViewModels (separación UI)

✔ Evita exponer entidades directamente  
✔ Mejora seguridad y UX

***

## ✅ MVC funcional + UI

* Listados
* Formularios
* Navegación

***

# ⚙️ Cómo ejecutarlo

## 1️⃣ Configurar Azure SQL

Editar:

```
appsettings.json
```

```json
"DefaultConnection": "Server=tcp:TU_SERVER.database.windows.net;..."
```

***

## 2️⃣ Crear base de datos

```bash
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```

***

## 3️⃣ Ejecutar

```bash
dotnet run
```

***

# 🔥 Qué incluye este proyecto

✅ Clean Architecture  
✅ EF Core Code First  
✅ Azure SQL  
✅ Relaciones complejas  
✅ Repository Pattern  
✅ Service Layer  
✅ ViewModels  
✅ CRUD completo


