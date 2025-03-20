`appsettings.json` is a configuration file used in ASP.NET Core applications to store settings such as database connection strings, authentication secrets, logging configurations, and other environment-specific parameters. It acts as a central place for managing configuration values without hardcoding them in the application code.



Assume the following settings for a frontend : 

```aspnet
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


```csharp 
public class Program  
{  
    public static void Main(string[] args)  
    {        
	    var builder = WebApplication.CreateBuilder(args);  
        // Add asp.net & prometheus services  
        builder.Services.AddControllers();  
        builder.Services.AddEndpointsApiExplorer();  
        builder.Services.AddSwaggerGen();  
        // Map app settings to setting classes  
        builder.Services.Configure<EmailSettings>(builder.Configuration.GetSection("Email"));  
        builder.Services.Configure<FrontendSettings>(builder.Configuration.GetSection("Frontend"));  
        // Custom services  
        builder.Services.AddScoped<EmailTemplateRenderer>();  
        builder.Services.AddScoped<EmailSender>();  
        builder.Services.AddScoped<UserService>();  
        builder.Services.AddScoped<EmailService>();  
        builder.Services.AddHostedService<GameLoopService>();
    ```