---
tags:
  - dependency-injection
  - environment
  - dev
  - settings
  - configuration
---
In modern development, efficiently managing configuration settings is essential. ASP.NET Core's configuration system separates settings from code, simplifying updates without altering the application. The `appsettings.json` file stores these settings, such as environment details and URLs, without hardcoding them, enhancing flexibility and security.

---
### Example `appsettings.json`

```json
{  
  "Global": {  
    "Environment": "Production"  
  },  
  "Frontend": {  
    "Url": "https://example.com",  
    "ConfirmEmail": "confirm-email",  
    "RequestPasswordReset": "request-password-reset",  
    "PasswordReset": "password-reset"  
  }
}
```
### Mapping Settings to C# Classes

```csharp
public class GlobalSettings
{
    public required string Environment { get; set; }
}
```

```csharp
public class FrontendSettings  
{  
    public required string Url { get; set; }  
    public required string ConfirmEmail { get; set; }  
    public required string RequestPasswordReset { get; set; }  
    public required string PasswordReset { get; set; }  

    public string ConfirmEmailUrl => $"{Url}/{ConfirmEmail}";  
    public string RequestPasswordResetUrl => $"{Url}/{RequestPasswordReset}";  
    public string PasswordResetUrl => $"{Url}/{PasswordReset}";  
}
```

### Loading Configuration in `Program.cs`

Bind the JSON sections to the respective classes during startup.

```csharp
public class Program  
{  
    public static void Main(string[] args)  
    {        
        var builder = WebApplication.CreateBuilder(args);  
        builder.Services.AddControllers();  

        // Bind settings sections to classes
        builder.Services.Configure<GlobalSettings>(builder.Configuration.GetSection("Global"));  
        builder.Services.Configure<FrontendSettings>(builder.Configuration.GetSection("Frontend"));  

        var app = builder.Build();  
        app.MapControllers();
        app.Run();  
    }  
}
```

---

## Using the Settings in a Controller

Inject and use the settings via dependency injection.

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Options;

[ApiController]
[Route("[controller]")]
public class AccountController : ControllerBase
{
    private readonly FrontendSettings _frontendSettings;

    public AccountController(IOptions<FrontendSettings> frontendOptions)
    {
        _frontendSettings = frontendOptions.Value;
    }

    [HttpGet("confirm-email")]
    public IActionResult ConfirmEmail()
    {
		// Get values from the frontendSettings
        var redirectUrl = _frontendSettings.ConfirmEmailUrl;
        return Redirect(redirectUrl);
    }
}
```


#### Comparision of IOption, IOptionSnapshot and IOptionMonitor

| Interface            | Behavior                                                                                                                                                                                                                        | Usage Scenario                                                                   | Scope     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | --------- |
| **IOptions**         | Provides configuration values as they were **when the app started**. Changes to appsettings.json after startup won’t be reflected.                                                                                              | When you do not expect configuration changes at runtime.                         | Singleton |
| **IOptionsSnapshot** | Provides a snapshot of configuration values on each request, so any changes in appsettings.json are **read on every request**. Cannot be injected into Singleton services; should only be used in Scoped or Transient services. | When you need the most up-to-date configuration on a per-request basis.          | Scoped    |
| **IOptionsMonitor**  | Monitors for configuration changes after the app starts and supports change notifications via the **OnChange** method, updating values as changes occur.                                                                        | When you need to react to configuration changes globally in a Singleton service. | Singleton |
#### Example of using OptionsMonitor

```csharp
	[Route("api/[controller]")]
    [ApiController]
    public class TestController : Controller
    {
        private ApplicationSettings _optionsMonitor;
        public TestController(IOptionsMonitor<ApplicationSettings> optionsMonitor)
        {
            // The current value
            _optionsMonitor = optionsMonitor.CurrentValue; 
            
            // OnChange is called when a file system watcher 
            // detects changes on disk.
            optionsMonitor.OnChange(option =>
            {
                _optionsMonitor = option;
            });

        }
    }
```


---

> [!info] References
> * https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-10.0
> * https://alirezafarokhi.medium.com/difference-between-ioptions-ioptionssnapshot-and-ioptionsmonitor-in-asp-netcore-587954bbcea