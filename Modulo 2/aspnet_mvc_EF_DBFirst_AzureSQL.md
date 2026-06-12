
Este proyecto es la versión equivalente al anterior pero usando **Database First con EF Core**:

👉 El modelo **NO se define en C#**, sino que se genera a partir de la base de datos existente.

✔ La base de datos (Azure SQL) es la fuente de verdad  
✔ EF Core genera:

* Entities
* DbContext  
  ✔ Tu código se adapta al esquema de la BD

***

# ✅ Qué incluye el ZIP

## 🧱 Estructura

```
/Models
   ├── AppDbContext.cs
   ├── Customer.cs
   ├── Product.cs
   ├── Invoice.cs

/Controllers
/Views
Program.cs
appsettings.json
```

***

## ✅ Modelos (simulan el scaffolding)

Incluye:

* Customer
* Product
* Invoice

⚠️ IMPORTANTE:  
Estos modelos están incluidos para que puedas ejecutar el proyecto directamente, pero en un entorno real:

👉 Se generan automáticamente con EF Core

***

# 🚀 Cómo hacerlo correctamente en tu entorno

## ✅ 1. Configura Azure SQL

Edita:

```json
appsettings.json
```

***

## ✅ 2. Ejecuta el scaffold (PASO CLAVE)

```bash
dotnet ef dbcontext scaffold "TU_CONNECTION_STRING" Microsoft.EntityFrameworkCore.SqlServer --output-dir Models --force
```

👉 Esto generará automáticamente:

* DbContext
* Clases C# por cada tabla
* Relaciones

✔ Sin escribir código manual

***

## ✅ 3. Ejecutar app

```bash
dotnet run
```

***

# 🔥 Diferencias clave vs Code First

| Aspecto        | Code First       | Database First      |
| -------------- | ---------------- | ------------------- |
| Modelo         | C#               | Base de datos       |
| Generación     | DB desde código  | Código desde DB     |
| Cambios schema | Migraciones      | Re-scaffold         |
| Uso típico     | Proyectos nuevos | Sistemas existentes |

👉 Database First es ideal cuando:

* La BD ya existe
* La gestiona un DBA
* Es un sistema legacy [\[bing.com\]](https://bing.com/search?q=ef+core+database+first+scaffold+command+sql+server+asp+net+core+example)

***

# 🎯 Qué puedes ver con este ejemplo

✅ Integración con Azure SQL existente  
✅ EF Core Database First  
✅ Reverse engineering  
✅ CRUD básico sobre DB real

***



Solo dime:  
👉 *“haz DBFirst FULL enterprise”* y te lo construyo 👍
