Te explico **paso a paso y en detalle** cómo implementar pruebas con **xUnit en ASP.NET Core 8 MVC con Razor**, cubriendo desde lo básico hasta escenarios reales (unitarios e integración).

***

# 🧱 1. Tipos de pruebas en ASP.NET Core

Antes de empezar, distingue:

| Tipo                | Qué prueba                                |
| ------------------- | ----------------------------------------- |
| ✅ Unit tests        | Lógica aislada (controladores, servicios) |
| ✅ Integration tests | App completa (routing, middleware, DB)    |

Con xUnit puedes hacer ambos.

***

# ⚙️ 2. Crear el proyecto de tests

## ✅ Opción CLI

```bash
dotnet new xunit -n MyApp.Tests
dotnet sln add MyApp.Tests
```

## ✅ Añadir referencia al proyecto MVC

```bash
dotnet add MyApp.Tests reference MyApp
```

***

# 📦 3. Paquetes necesarios

Para ASP.NET Core 8 normalmente necesitas:

```bash
dotnet add package Microsoft.AspNetCore.Mvc.Testing
dotnet add package Moq
dotnet add package FluentAssertions
```

***

# 🧪 4. Pruebas unitarias de controladores (MVC)

## 🎯 Ejemplo de controlador

```csharp
public class HomeController : Controller
{
    private readonly IProductService _service;

    public HomeController(IProductService service)
    {
        _service = service;
    }

    public IActionResult Index()
    {
        var products = _service.GetAll();
        return View(products);
    }
}
```

***

## ✅ Test unitario con xUnit + Moq

```csharp
public class HomeControllerTests
{
    [Fact]
    public void Index_Returns_View_With_Products()
    {
        // Arrange
        var mockService = new Mock<IProductService>();
        mockService.Setup(s => s.GetAll())
                   .Returns(new List<string> { "A", "B" });

        var controller = new HomeController(mockService.Object);

        // Act
        var result = controller.Index();

        // Assert
        var viewResult = Assert.IsType<ViewResult>(result);
        var model = Assert.IsAssignableFrom<IEnumerable<string>>(viewResult.Model);

        Assert.Equal(2, model.Count());
    }
}
```

***

## 📌 Claves importantes

* xUnit usa `[Fact]` en vez de `[Test]`
* No hay `SetUp` → se usa el **constructor**
* Mockeas dependencias con **Moq**

***

# 🧪 5. Pruebas de Razor Pages

## 🎯 Razor Page Model

```csharp
public class IndexModel : PageModel
{
    public string Message { get; private set; }

    public void OnGet()
    {
        Message = "Hola";
    }
}
```

## ✅ Test

```csharp
public class IndexModelTests
{
    [Fact]
    public void OnGet_Sets_Message()
    {
        var model = new IndexModel();

        model.OnGet();

        Assert.Equal("Hola", model.Message);
    }
}
```

***

# 🌐 6. Pruebas de integración (IMPORTANTÍSIMO)

Aquí pruebas la app real: routing, middleware, DI, etc.

***

## 🧩 6.1 Crear `WebApplicationFactory`

ASP.NET Core 8 usa **Program.cs minimal hosting**.

```csharp
public class CustomWebApplicationFactory<TProgram>
    : WebApplicationFactory<TProgram> where TProgram : class
{
}
```

***

## ✅ Test de integración básico

```csharp
public class HomeIntegrationTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly HttpClient _client;

    public HomeIntegrationTests(WebApplicationFactory<Program> factory)
    {
        _client = factory.CreateClient();
    }

    [Fact]
    public async Task Get_Index_Returns_Success()
    {
        var response = await _client.GetAsync("/");

        response.EnsureSuccessStatusCode();

        var content = await response.Content.ReadAsStringAsync();

        Assert.Contains("Welcome", content);
    }
}
```

***

# 🗄️ 7. Probar con base de datos (EF Core)

## ✅ Usar InMemory DB para tests

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseInMemoryDatabase("TestDb"));
```

***

## ✅ Sobrescribir servicios en tests

```csharp
public class CustomFactory : WebApplicationFactory<Program>
{
    protected override void ConfigureWebHost(IWebHostBuilder builder)
    {
        builder.ConfigureServices(services =>
        {
            var descriptor = services.SingleOrDefault(
                d => d.ServiceType == typeof(DbContextOptions<AppDbContext>));

            services.Remove(descriptor);

            services.AddDbContext<AppDbContext>(options =>
                options.UseInMemoryDatabase("TestDb"));
        });
    }
}
```

***

# 🧪 8. Test completo con DB

```csharp
public class ProductTests : IClassFixture<CustomFactory>
{
    private readonly HttpClient _client;

    public ProductTests(CustomFactory factory)
    {
        _client = factory.CreateClient();
    }

    [Fact]
    public async Task Create_Product_Works()
    {
        var response = await _client.PostAsync("/Products/Create",
            new FormUrlEncodedContent(new[]
            {
                new KeyValuePair<string, string>("Name", "Test")
            }));

        Assert.Equal(HttpStatusCode.Redirect, response.StatusCode);
    }
}
```

***

# 🔄 9. Buenas prácticas

## ✅ Organización

* `Tests/Controllers`
* `Tests/Services`
* `Tests/Integration`

## ✅ Naming

```
Metodo_Escenario_ResultadoEsperado
```

Ejemplo:

```
Index_NoProducts_ReturnsEmptyList
```

***

## ✅ Aislamiento

* Unit tests → usar mocks
* Integration → usar DB en memoria

***

## ✅ Usar FluentAssertions (mejor legibilidad)

```csharp
result.Should().BeOfType<ViewResult>();
```

***

# ✅ Resumen final

Para probar ASP.NET Core 8 MVC Razor con xUnit:

1. ✅ Crear proyecto xUnit
2. ✅ Referenciar tu proyecto MVC
3. ✅ Usar Moq para unit tests
4. ✅ Probar controllers y PageModels
5. ✅ Usar `WebApplicationFactory` para integración
6. ✅ Simular DB con InMemory
7. ✅ Organizar bien los tests

***



En **xUnit** (un framework de testing para .NET), las **fixtures** son una forma de **compartir contexto o estado entre múltiples tests**, evitando repetir la misma configuración una y otra vez.

Dicho de forma sencilla:  
👉 una fixture te permite preparar algo (datos, conexiones, objetos, etc.) una sola vez y reutilizarlo en varios tests.

***

# 🧩 Tipos de fixtures en xUnit

xUnit tiene varios tipos de fixtures según el alcance que necesitas:

## 1. **Class Fixture (`IClassFixture`)**

Se usa cuando quieres compartir datos entre todos los tests de **una misma clase**.

### ✅ Ejemplo típico

* Crear una conexión a base de datos
* Preparar datos comunes

```csharp
public class DatabaseFixture
{
    public string ConnectionString { get; }

    public DatabaseFixture()
    {
        ConnectionString = "Server=localhost;Database=test;";
        // Inicialización (ej: abrir conexión)
    }
}

public class MyTests : IClassFixture<DatabaseFixture>
{
    private readonly DatabaseFixture _fixture;

    public MyTests(DatabaseFixture fixture)
    {
        _fixture = fixture;
    }

    [Fact]
    public void Test1()
    {
        Assert.NotNull(_fixture.ConnectionString);
    }

    [Fact]
    public void Test2()
    {
        Assert.Contains("Server", _fixture.ConnectionString);
    }
}
```

📌 La fixture se crea **una sola vez por clase de tests**.

***

## 2. **Collection Fixture (`ICollectionFixture`)**

Se usa cuando quieres compartir datos entre **varias clases de tests**.

### ✅ Ejemplo

```csharp
[CollectionDefinition("Database collection")]
public class DatabaseCollection : ICollectionFixture<DatabaseFixture>
{
}

[Collection("Database collection")]
public class TestClass1
{
    private readonly DatabaseFixture _fixture;

    public TestClass1(DatabaseFixture fixture)
    {
        _fixture = fixture;
    }
}

[Collection("Database collection")]
public class TestClass2
{
    private readonly DatabaseFixture _fixture;

    public TestClass2(DatabaseFixture fixture)
    {
        _fixture = fixture;
    }
}
```

📌 Aquí la fixture se comparte entre múltiples clases.

***

## 3. **Constructor y `IDisposable`**

Las fixtures suelen implementar limpieza de recursos:

```csharp
public class DatabaseFixture : IDisposable
{
    public DatabaseFixture()
    {
        // Setup
    }

    public void Dispose()
    {
        // Cleanup (cerrar conexión, liberar recursos)
    }
}
```

***

# 🧠 ¿Por qué usar fixtures?

## ✅ Ventajas

* Evitas repetir código de configuración
* Mejoras rendimiento (setup una sola vez)
* Código más limpio y mantenible
* Permite compartir recursos complejos (DB, API, etc.)

## ❗ Importante

* xUnit **crea una instancia nueva por test** (por defecto)
* Las fixtures rompen ese comportamiento para compartir estado

***

# 🆚 Fixtures vs Setup tradicional

En otros frameworks (como NUnit o MSTest), tienes métodos tipo:

* `SetUp`
* `TestInitialize`

En xUnit:

* No existe `SetUp`
* Se usa el **constructor**
* Y las **fixtures** para compartir contexto

***

# ✅ Resumen rápido

| Concepto             | Qué hace                            |
| -------------------- | ----------------------------------- |
| `IClassFixture`      | Comparte estado dentro de una clase |
| `ICollectionFixture` | Comparte estado entre varias clases |
| Constructor          | Inicializa cada test                |
| `Dispose`            | Limpia recursos                     |

***




