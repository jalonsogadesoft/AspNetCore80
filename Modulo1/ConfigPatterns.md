# Patrón configuración de Asp.net core 8.0

# 🧠 ¿Qué es un patrón (pattern)?

Un **patrón** es una solución reutilizable a un problema común de diseño.

👉 En este contexto:

> “¿Cómo gestiono la configuración de forma limpia, mantenible y segura?”

ASP.NET Core ofrece varios **patrones de acceso a configuración**, cada uno pensado para un escenario distinto.

***

# 🎯 Problema que intentan resolver

Sin patrones:

```csharp
var valor = config["MiConfig:Mensaje"];
```

👉 Problemas:

* Strings “mágicos”
* Sin IntelliSense
* Difícil de mantener
* Errores en runtime

👉 Los patrones solucionan esto de diferentes formas.

***

# 🧩 1. IConfiguration (NO es realmente un patrón)

## ✅ Qué es

Un **servicio base** que representa un diccionario de configuración.

```csharp
config["MiConfig:Mensaje"]
```

## 🧠 Idea

👉 Acceso directo a clave/valor

***

## ✅ Ventajas

* Simple
* Flexible
* No necesitas clases

## ❌ Problemas

* No tipado
* No validación
* Difícil escalar

***

## 🎯 Cuándo usarlo

* Casos rápidos
* Debug
* Ejemplos

***

# 🧩 2. Options Pattern (IOptions<T>) ✅ patrón real

## ✅ Qué es el patrón

El **Options Pattern** consiste en:

> Mapear configuración a una clase fuertemente tipada e inyectarla mediante DI

***

## 🔹 Ejemplo

```csharp
builder.Services.Configure<MiConfig>(
    builder.Configuration.GetSection("MiConfig"));
```

```csharp
public class MiConfig
{
    public string Mensaje { get; set; }
}
```

Uso:

```csharp
app.MapGet("/", (IOptions<MiConfig> options) =>
{
    return options.Value.Mensaje;
});
```

***

## 🧠 Idea del patrón

👉 “Convertir configuración en un objeto”

***

## ✅ Ventajas

* Tipado fuerte ✅
* IntelliSense ✅
* Integración con DI ✅
* Validación posible ✅

***

## ❌ Limitación

* ❌ Los valores no cambian en runtime

***

## 🎯 Cuándo usarlo

👉 **Patrón principal en ASP.NET Core**

* APIs
* aplicaciones web
* configs estáticas

***

# 🧩 3. IOptionsSnapshot<T> ✅ patrón extendido

## ✅ Qué es el patrón

Extiende Options Pattern:

> Proporciona una nueva “foto” (snapshot) de la configuración en cada request

***

## 🔹 Ejemplo

```csharp
app.MapGet("/", (IOptionsSnapshot<MiConfig> options) =>
{
    return options.Value.Mensaje;
});
```

***

## 🧠 Idea del patrón

👉 “Dame una versión actualizada por petición”

***

## ✅ Ventajas

* Detecta cambios ✅
* Ideal para web ✅

***

## ❌ Limitaciones

* Solo funciona en ámbito request (scoped)
* No funciona en singletons

***

## 🎯 Cuándo usarlo

* Apps web
* Config que puede cambiar sin reinicio

***

# 🧩 4. IOptionsMonitor<T> ✅ patrón reactivo

## ✅ Qué es el patrón

Una evolución más avanzada:

> Permite reaccionar a cambios en configuración en tiempo real

***

## 🔹 Ejemplo

```csharp
app.MapGet("/", (IOptionsMonitor<MiConfig> options) =>
{
    return options.CurrentValue.Mensaje;
});
```

Y además:

```csharp
options.OnChange(nuevaConfig =>
{
    Console.WriteLine("La configuración ha cambiado");
});
```

***

## 🧠 Idea del patrón

👉 “Notifícame cuando cambie la configuración”

***

## ✅ Ventajas

* Cambios en caliente ✅
* Funciona en singleton ✅
* Programación reactiva ✅

***

## ❌ Limitaciones

* Más complejo
* No siempre necesario

***

## 🎯 Cuándo usarlo

* Background services
* apps dinámicas
* sistemas avanzados

***

# ⚖️ Comparativa final

| Patrón           | Tipo   | Tipado | Runtime         | Uso        |
| ---------------- | ------ | ------ | --------------- | ---------- |
| IConfiguration   | Base   | ❌      | ❌               | rápido     |
| IOptions         | Patrón | ✅      | ❌               | ✅ estándar |
| IOptionsSnapshot | Patrón | ✅      | ✅ (por request) | web        |
| IOptionsMonitor  | Patrón | ✅      | ✅ (real-time)   | avanzado   |

***

# 🧠 Diferencia conceptual

## 🔴 IConfiguration

👉 “Leo valores sueltos”

***

## 🟢 IOptions

👉 “Trabajo con un objeto de configuración”

***

## 🔵 Snapshot

👉 “Quiero consistencia por petición”

***

## 🟣 Monitor

👉 “Quiero reaccionar a cambios”

***

# 🎯 Cómo explicarlo en clase (muy potente)

Haz esta progresión:

### 1. Problema

```csharp
config["..."]
```

👉 “Esto escala mal”

***

### 2. Solución (Options Pattern)

👉 objeto tipado

***

### 3. Problema nuevo

👉 “¿y si cambia la config?”

***

### 4. Soluciones avanzadas

* Snapshot (web)
* Monitor (reactivo)

***

# 💡 Idea

> “El patrón no cambia la configuración…  
> cambia cómo la consumimos.”

***

