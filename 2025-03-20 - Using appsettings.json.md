---
tags:
  - dependency-injection
  - environment
  - dev
  - settings
  - configuration
---

The `appsettings.json` file stores configuration settings for your ASP.NET Core app (e.g., environment details, URLs, routes) without hardcoding them.

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

**GlobalSettings.cs**
```csharp
public class GlobalSettings
{
    public required string Environment { get; set; }
}
```

**FrontendSettings.cs**
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


### Comparision of IOption, IOptionSnapshot and IOptionMonitor

- **IOptions** provides configuration values as they were when the app started. Changes to appsettings.json after startup won’t be reflected.
- **IOptionsSnapshot** provides a snapshot of configuration values on each request, so any changes in appsettings.json are read on every request. Cannot be injected into Singleton services, since it should only be used in services with a Scoped or Transient lifetime.
- **IOptionsMonitor** monitors for configuration changes after the app starts. It supports change notifications via the OnChange method, updating values as the configuration changes. 

**Usage Scenarios:**
- Use **IOptions** when you do not expect configuration changes at runtime.
- Use **IOptionsSnapshot** when you need the most up-to-date configuration on a per-request basis.
- Use **IOptionsMonitor** when you need to react to configuration changes globally in a singleton service.


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







Sources : 
https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-6.0
https://alirezafarokhi.medium.com/difference-between-ioptions-ioptionssnapshot-and-ioptionsmonitor-in-asp-netcore-587954bbcea