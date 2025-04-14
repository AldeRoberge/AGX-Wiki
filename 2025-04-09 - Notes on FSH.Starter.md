```csharp
[Inject]  
protected IApiClient _client { get; set; } = default!;
```




Catalog.Domain
* Events
	* BrandCreated
	* BrandUpdated
	* ProductCreated
	* ProductUpdated
* Exceptions (Errors in my case)
	* BrandNotFoundException
	* ProductNotFoundException
* Brand
* Product


I like the idea of having permissions

```csharp
[Permissions("Permissions.Brands.Create")]
```

But at the same time, it adds unnecessary complexity.