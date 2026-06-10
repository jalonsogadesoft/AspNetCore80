
## 🧠 1. Code First con Azure SQL

* EF Core con proveedor `SqlServer`
* Conexión preparada para Azure SQL en `appsettings.json`

```json
"DefaultConnection": "Server=tcp:YOURSERVER.database.windows.net;Initial Catalog=YOURDB;..."
```

👉 EF Core permite crear y sincronizar la base de datos desde el modelo (Code First) [\[eu-prod.as...rosoft.com\]](https://eu-prod.asyncgw.teams.microsoft.com/v1/objects/0-weu-d20-cc758c969515081fdd88e94bf9015d8c/views/original/aspnet_mvc_EF_CodeFirst_AzureSQL.zip)

***

## 🧱 2. Modelo relacional completo

Incluye:

### 👤 Customer

* 1 → N Facturas

### 🧾 Invoice

* N → M Productos (tabla intermedia)

### 📦 Product

### 🔗 InvoiceProduct (tabla puente N:M)

👉 Este patrón es estándar en EF Core para relaciones muchos-a-muchos complejas [\[c-sharpcorner.com\]](https://www.c-sharpcorner.com/article/code-first-approach-in-asp-net-core-mvc-with-ef-core-migration/)

***

## 🗄️ 3. DbContext

```csharp
public DbSet<Customer> Customers
public DbSet<Product> Products
public DbSet<Invoice> Invoices
public DbSet<InvoiceProduct> InvoiceProducts
```

***

## ✅ 4. CRUD básico funcional

* Listado de facturas
* Creación
* Persistencia en Azure SQL

***

# ⚙️ Cómo ejecutarlo

## 1️⃣ Ajusta conexión

Edita:

```
appsettings.json
```

👉 Sustituye:

* `YOURSERVER`
* `YOURDB`
* `user/password`

***

## 2️⃣ Crear base de datos

```bash
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```

👉 EF Core creará automáticamente:

* tablas
* relaciones
* claves foráneas

***

## 3️⃣ Ejecutar

```bash
dotnet run
```

***

# ⚠️ Nota

Es una **versión simplificada funcional** que incluye:

✅ Modelo relacional  
✅ EF Core Code First  
✅ Azure SQL  
✅ MVC funcional



