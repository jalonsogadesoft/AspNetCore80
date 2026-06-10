
## ✅ Qué contiene exactamente este proyecto

### 🗄️ Persistencia real

* Entity Framework Core
* SQLite (`invoices.db`)
* `DbContext` configurado

### 🧱 Arquitectura

```
/Models
/Data
/Controllers
/Views
appsettings.json
Program.cs
```

### ✅ Funcionalidad

* Listado de facturas desde BD
* Creación persistente (se guarda de verdad)
* Validaciones básicas (DataAnnotations)

***

## ⚙️ IMPORTANTE: pasos para que funcione

Después de descargar:

### 1️⃣ Restaurar paquetes

```bash
dotnet restore
```

***

### 2️⃣ Crear la base de datos

```bash
dotnet tool install --global dotnet-ef
dotnet ef migrations add InitialCreate
dotnet ef database update
```

***

### 3️⃣ Ejecutar

```bash
dotnet run
```

👉 Ir a:

```
http://localhost:5000/Invoices
```

***

## 🧠 Qué enseña este ejemplo 

Con este proyecto estás cubriendo:

✅ MVC completo  
✅ Validaciones  
✅ ORM (Entity Framework Core)  
✅ Base de datos real  
✅ Inyección de dependencias  
✅ Flujo real de aplicación empresarial

***

