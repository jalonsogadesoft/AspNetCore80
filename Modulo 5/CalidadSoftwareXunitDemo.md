Aplicación demo ASP.NET Core 8 MVC + Razor con xUnit con 15 pruebas unitarias.

Demo  centrada en reglas de negocio  (precio final, envío gratis, score de calidad y checklist de release), con UI en QualityLab y navegación desde el layout. 
En pruebas (CalidadSoftwareXunitDemo.Tests) quedaron ejemplos de xUnit: [Fact], [Theory] con InlineData, MemberData, ClassData, Trait, Assert.Throws, Assert.Collection, IClassFixture e ICollectionFixture, además de tests de controlador con fake service para validar interacción y modelo de vista.

Para ejecutarla: dotnet run --project .\CalidadSoftwareXunitDemo.Web
Para pruebas: dotnet test .\CalidadSoftwareXunitDemo.sln

