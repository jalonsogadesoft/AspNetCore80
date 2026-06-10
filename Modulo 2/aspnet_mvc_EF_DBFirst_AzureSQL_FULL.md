

# 🚀 Qué incluye esta versión )

Este proyecto es el equivalente completo al Code First FULL, pero adaptado a **Database First sobre Azure SQL**.

***

## 🧠 ✅ Arquitectura enterprise

```
/Models              → ENTIDADES generadas (scaffold)
/Repositories        → Repository pattern genérico
/Services            → Service layer
/Controllers         → MVC
/Views               → UI
Program.cs           → Configuración DI + EF
```

***

## ✅ 1. Database First real (concepto clave)

✔ El modelo **proviene de la base de datos existente**  
✔ EF Core genera automáticamente:

* `DbContext`
* Entidades
* Relaciones

👉 Esto se hace mediante scaffolding (reverse engineering)

```bash
dotnet ef dbcontext scaffold "CONNECTION_STRING" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Force
```

***

## ✅ 2. Repository Pattern (completo)

```csharp
public interface IRepository<T>
```

✔ CRUD genérico  
✔ Desacopla datos  
✔ Reutilizable

***

## ✅ 3. Service Layer

```csharp
public class InvoiceService
```

✔ Contiene lógica de negocio  
✔ Controllers limpios  
✔ Testable

***

## ✅ 4. EF Core con Azure SQL

```csharp
options.UseSqlServer(...)
```

✔ Preparado para cloud  
✔ Compatible con DB existente

***

## ✅ 5. CRUD funcional

* Listado de facturas ✅
* Creación ✅
* Persistencia ✅

***

# ⚙️ Cómo usarlo correctamente (IMPORTANTE)

## 1️⃣ Configurar Azure SQL

Edita:

```json
appsettings.json
```

***

## 2️⃣ Ejecutar scaffolding REAL

Aunque el proyecto trae modelos de ejemplo, en entorno real debes regenerarlos:

```bash
dotnet ef dbcontext scaffold "TU_CONNECTION" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Force
```

✔ EF sincroniza con tu base de datos actual

***

## 3️⃣ Ejecutar

```bash
dotnet run
```

***

# 🔥 Diferencias clave vs Code First FULL

| Característica | Code First  | DB First            |
| -------------- | ----------- | ------------------- |
| Modelo         | C#          | Base de datos       |
| Evolución      | Migraciones | Re-scaffold         |
| Control schema | C#          | DBA                 |
| Uso ideal      | Apps nuevas | Sistemas existentes |

***

# 🎯 Nivel de este proyecto

Este proyecto ya está en:

💼 **Nivel empresa real DB-driven**

Incluye:

✅ EF Core (DB-first real)  
✅ Azure SQL  
✅ Repository Pattern  
✅ Service Layer  
✅ MVC limpio  
✅ DI configurado

***

# ⚠️ Importante (experiencia real)

En proyectos reales DB First:

👉 Nunca modifiques directamente los modelos generados  
👉 Usa:

```csharp
public partial class Invoice { }
```

✔ Extensión segura sin sobrescribir al regenerar

