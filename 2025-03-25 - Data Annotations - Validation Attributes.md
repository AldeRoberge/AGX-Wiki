## Validation attributes

A conceptually similar but with a different implementation is the validation attributes provided by [Data Annotations](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-9.0#validation-attributes).

```csharp
public class Movie
{
    public int Id { get; set; }

    [Required]
    [StringLength(100)]
    public string Title { get; set; } = null!;

    [ClassicMovie(1960)]
    [DataType(DataType.Date)]
    [Display(Name = "Release Date")]
    public DateTime ReleaseDate { get; set; }

    [Required]
    [StringLength(1000)]
    public string Description { get; set; } = null!;

    [Range(0, 999.99)]
    public decimal Price { get; set; }
}

```

It includes some built-in validation like :

- **EmailAddress**: Validates that the property has an email format.  
- **Phone**: Validates that the property has a telephone number format.  
- **Range**: Validates that the property value falls within a specified range.  
- **Required**: Validates that the field isn't null. 
- A full list can be found HERE

Additionally, can provide an error message : 

```csharp
[StringLength(8, ErrorMessage = "Name length can't be more than 8.")]
```

Read more here : [Model validation in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-9.0#validation-attributes)
#### The issue...

But as Milan notes : 
> While functional, Data Annotations can be limiting for complex validation scenarios.

## Why FluentValidation Over Data Annotations?

Data Annotations work well for simple validations, but FluentValidation offers several advantages:

- More expressive and flexible validation rules
- Better support for complex conditional validations
- Cleaner separation of concerns (validation logic separate from model)
- Easier testing of validation rules
- Better support for custom validation logic
- Allows for injecting dependencies into validators

