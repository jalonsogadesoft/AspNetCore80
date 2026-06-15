
## ✅ Proyecto `AdvancedFormsDemo` — ASP.NET Core 8.0 MVC

**Ruta:** `Modulo 3\AdvancedFormsDemo`  
**Ejecutar:** `dotnet run` → `http://localhost:5071/Employees`

---

### 📁 Estructura generada

```
AdvancedFormsDemo/
├── Models/
│   ├── Employee.cs              ← Modelo principal con IValidatableObject
│   └── Enums/ (Department, Position, EmployeeStatus)
├── Validation/
│   ├── ValidNifAttribute.cs     ← Atributo personalizado NIF/NIE
│   ├── MinimumAgeAttribute.cs   ← Atributo personalizado edad mínima
│   └── MustBeTrueAttribute.cs  ← Atributo personalizado checkbox
├── Services/
│   └── EmployeeService.cs       ← Repositorio en memoria (CRUD)
├── Controllers/
│   └── EmployeesController.cs   ← CRUD completo + Remote + AJAX
├── Views/Employees/
│   ├── Index / Create / Edit / Details / Delete
│   └── _EmployeeForm.cshtml     ← Formulario reutilizado en Create y Edit
└── wwwroot/js/
    └── employees-validation.js  ← Adaptadores jQuery Validate personalizados
```

---

### 🔐 Validaciones demostradas

| Tipo | Atributo / Mecanismo | Escenario |
|------|---------------------|-----------|
| **Campo estándar** | `[Required]`, `[StringLength]`, `[EmailAddress]`, `[Range]`, `[Phone]` | Nombre, email, teléfono, salario |
| **Atributo personalizado + cliente** | `[ValidNif]` + `IClientModelValidator` | Valida formato y letra de control del NIF/NIE |
| **Atributo personalizado + cliente** | `[MinimumAge(18)]` + `IClientModelValidator` | Fecha de nacimiento ≥ 18 años |
| **Atributo personalizado + cliente** | `[MustBeTrue]` + `IClientModelValidator` | Checkbox obligatorio (política de datos) |
| **Remota (AJAX)** | `[Remote]` → `IsEmailAvailable()` | Unicidad de email en tiempo real |
| **Cruzada / registro** | `IValidatableObject.Validate()` | 4 reglas: EndDate > StartDate, baja obligatoria si Inactivo, edad mínima para trabajar (16 años), salario por rango de cargo |
| **UX dinámica** | `GetSalaryRange()` + JS | Muestra rango salarial permitido al seleccionar cargo |
