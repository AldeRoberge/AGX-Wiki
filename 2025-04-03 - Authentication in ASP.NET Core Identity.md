ASP.NET Core provides a built-in system known as **ASP.NET Core Identity**, which handles **authentication** (verifying who users are) and **authorization** (controlling what users can do in your application).

1. Authentication :  *“Who are you?”*
2. Authorization : *"What are you allowed to do?"*

Step 1: Start by creating a new **ASP.NET Core Web App**.

Step 2: Install **ASP.NET Core Identity** :

```csharp
dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore
```

Step 3: Configure the required services for Identity : 

```csharp
using Microsoft.AspNetCore.Identity;
using Microsoft.EntityFrameworkCore;
using IdentityApp.Data;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.

// Configure the DbContext to use SQL Server with the connection string from configuration
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"))
);

// Set up Identity services, including user registration, login, and roles
builder.Services.AddDefaultIdentity<IdentityUser>(options => 
    options.SignIn.RequireConfirmedAccount = true
)
.AddEntityFrameworkStores<ApplicationDbContext>(); // Use the ApplicationDbContext for Identity

// Add Razor Pages services for the application
builder.Services.AddRazorPages();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    // In non-development environments, use a custom error page and enforce HSTS
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection(); // Redirect HTTP requests to HTTPS
app.UseStaticFiles(); // Serve static files (e.g., CSS, JavaScript)
app.UseRouting(); // Enable routing for the app

app.UseAuthentication(); // Enable authentication middleware
app.UseAuthorization();  // Enable authorization middleware

// Map Razor Pages endpoints to the app
app.MapRazorPages();

// Run the application
app.Run();
```

Step 4: Create ApplicationDbContext : 

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore;

namespace IdentityApp.Data
{
    public class ApplicationDbContext : IdentityDbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
}
```

This class inherits from `IdentityDbContext`, which provides the necessary structure for Identity tables (like users, roles, and claims).

Step 5: Run **Entity Framework Core Migrations** to set up the Identity schema in the database:

```shell
dotnet ef migrations add InitialCreate  
dotnet ef database update
```

These commands will create all the necessary Identity tables in your database (such as `AspNetUsers`, `AspNetRoles`, `AspNetUserRoles`, etc.).

---

Understanding the Basics of ASP.NET Core Identity

## 1. User Registration

When users register on your site, Identity stores their information (like username, password, and other profile details) in the database. Passwords are securely hashed before storage, so no plain-text passwords are stored.

Example of a registration form:

```html
<form method="post" asp-page="/Account/Register">  
    <div class="form-group">  
        <label asp-for="Input.Email"></label>  
        <input asp-for="Input.Email" class="form-control" />  
    </div>  
    <div class="form-group">  
        <label asp-for="Input.Password"></label>  
        <input asp-for="Input.Password" type="password" class="form-control" />  
    </div>  
    <div class="form-group">  
        <label asp-for="Input.ConfirmPassword"></label>  
        <input asp-for="Input.ConfirmPassword" type="password" class="form-control" />  
    </div>  
    <button type="submit" class="btn btn-primary">Register</button>  
</form>
```

## 2. Login and Authentication

Once registered, users can log in using their email and password. ASP.NET Core Identity handles authentication by checking the credentials and issuing an authentication cookie to track logged-in users.

Example of a login form:

```html
<form method="post" asp-page="/Account/Login">  
    <div class="form-group">  
        <label asp-for="Input.Email"></label>  
        <input asp-for="Input.Email" class="form-control" />  
    </div>  
    <div class="form-group">  
        <label asp-for="Input.Password"></label>  
        <input asp-for="Input.Password" type="password" class="form-control" />  
    </div>  
    <button type="submit" class="btn btn-primary">Login</button>  
</form>
```

## 3. Authorization with Roles

ASP.NET Core Identity allows you to define **roles** and assign users to those roles. Roles can be used to restrict access to certain parts of the application.

For example, you could have an **Admin** role and allow only admins to access certain pages.

Example of role-based authorization in a Razor Page:

```csharp
[Authorize(Roles = "Admin")]  
public class AdminPageModel : PageModel  
{  
    public void OnGet()  
    {  
        // Only users with the Admin role can access this page  
    }  
}
``` 

