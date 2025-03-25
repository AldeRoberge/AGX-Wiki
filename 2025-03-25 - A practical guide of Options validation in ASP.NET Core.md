
Summary

1. **Define Settings:** Create a class with required properties.
2. **Create a Validator:** Implement rules using FluentValidation.
3. **Register Services:** Add an extension method to bind configuration and register the validator.
4. **Integrate Validation:** Use custom classes to connect FluentValidation with the Options Pattern.
5. **Register in Program.cs:** Call the extension method to validate settings at startup.

## 1. Define the Configuration Class

Create a class to hold GitHub settings. The class maps to a configuration section (e.g., _appsettings.json_).

```csharp
namespace ADG.Server.Options;

public class GitHubSettings
{
    public const string ConfigurationSection = "GitHubSettings";

    public required string BaseUrl { get; init; }
    public required string AccessToken { get; init; }
    public required string RepositoryName { get; init; }
}
```

## 2. Create the Validator

Implement FluentValidation rules in a validator class.

```csharp
using FluentValidation;

namespace ADG.Server.Options;

public class GitHubSettingsValidator : AbstractValidator<GitHubSettings>
{
    public GitHubSettingsValidator()
    {
        RuleFor(x => x).NotNull().WithMessage("Settings are required.");
        RuleFor(x => x.BaseUrl).NotEmpty();
        RuleFor(x => x.BaseUrl)
            .Must(baseUrl => Uri.TryCreate(baseUrl, UriKind.Absolute, out _))
            .When(x => !string.IsNullOrWhiteSpace(x.BaseUrl))
            .WithMessage($"{nameof(GitHubSettings.BaseUrl)} must be a valid URL");
        RuleFor(x => x.AccessToken)
            .NotEmpty()
            .WithMessage("AccessToken is required.");
        RuleFor(x => x.RepositoryName)
            .NotEmpty()
            .WithMessage("RepositoryName is required.");
    }
}
```

## 3. Register Services for Validation

Create an extension method to wire up settings and validation.

- **Steps:**
    - Register the validator
    - Bind the configuration section
    - Add FluentValidation to the options pipeline

```csharp
using ADG.Options.Validation;
using FluentValidation;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;

namespace ADG.Server.Options;

public static class GitHubSettingsValidatorServiceExtensions
{
    public static void AddGitHubSettingsValidation(this IServiceCollection services, IConfiguration configuration)
    {
        // Register the GitHubSettings validator
        services.AddScoped<IValidator<GitHubSettings>, GitHubSettingsValidator>();

        // Bind the configuration section to GitHubSettings
        services.Configure<GitHubSettings>(configuration.GetSection(GitHubSettings.ConfigurationSection));

        // Integrate FluentValidation with the Options Pattern
        services.AddOptionsWithFluentValidation<GitHubSettings>(GitHubSettings.ConfigurationSection);
    }
}
```

---

## 4. Integrate FluentValidation with the Options Pattern

Implement helper classes to run FluentValidation when options are loaded.

### FluentValidateOptions.cs

This class uses FluentValidation to validate options during startup.

```csharp
using FluentValidation;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Options;

namespace ADG.Options.Validation;

public class FluentValidateOptions<TOptions>(
    IServiceProvider serviceProvider,
    string? name
) : IValidateOptions<TOptions>
    where TOptions : class
{
    public ValidateOptionsResult Validate(string? name1, TOptions options)
    {
        if (name is not null && name != name1)
            return ValidateOptionsResult.Skip;

        ArgumentNullException.ThrowIfNull(options);

        using var scope = serviceProvider.CreateScope();
        var validator = scope.ServiceProvider.GetRequiredService<IValidator<TOptions>>();
        var result = validator.Validate(options);

        if (result.IsValid)
            return ValidateOptionsResult.Success;

        var type = options.GetType().Name;
        var errors = result.Errors.Select(
            failure =>
                $"Validation for {failure.PropertyName} in {type} failed with error '{failure.ErrorMessage}'.").ToList();

        return ValidateOptionsResult.Fail(errors);
    }
}
```

### OptionsBuilderExtensions.cs

This extension method wires FluentValidation into the options configuration.

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Options;

namespace ADG.Options.Validation;

public static class OptionsBuilderExtensions
{
    public static void AddOptionsWithFluentValidation<TOptions>(this IServiceCollection services,
        string configurationSection)
        where TOptions : class
    {
        services.AddOptions<TOptions>()
            .BindConfiguration(configurationSection)
            .ValidateFluentValidation() // Setup FluentValidation
            .ValidateOnStart();         // Validate on application start
    }

    private static OptionsBuilder<TOptions> ValidateFluentValidation<TOptions>(
        this OptionsBuilder<TOptions> builder)
        where TOptions : class
    {
        builder.Services.AddSingleton<IValidateOptions<TOptions>>(
            serviceProvider => new FluentValidateOptions<TOptions>(
                serviceProvider,
                builder.Name));

        return builder;
    }
}
```

---

## 5. Register in Program.cs

Finally, add the GitHub settings validation in your ASP.NET Core application's `Program.cs`.

```csharp
// In Program.cs
builder.Services.AddGitHubSettingsValidation(builder.Configuration);
```



That's it! If any validation errors are found, the program will throw and print the validation errors in the consoel.