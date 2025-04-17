
## Prerequisites

- **.NET SDK** 6.0 or later
- **Visual Studio** 2022 (17.4+) / VS Code with latest C# extension
- A **SDK-style** solution (i.e. your `.csproj` files begin with `<Project Sdk="Microsoft.NET.Sdk">…`)

---

## 1. Enable Central Package Management

1. **At the root of your solution**, create a file named:
    
    ```
    Directory.Packages.props
    ```
    
2. Populate it with your shared package versions:
    
    ```xml
    <Project>
      <!-- Opt into Central Package Management -->
      <PropertyGroup>
        <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
      </PropertyGroup>
    
      <!-- Define all your package versions in one place -->
      <ItemGroup>
        <PackageVersion Include="Newtonsoft.Json" Version="13.0.3" />
        <PackageVersion Include="Serilog"          Version="2.12.0" />
        <PackageVersion Include="Dapper"           Version="2.0.123" />
        <!-- add more packages here… -->
      </ItemGroup>
    </Project>
    ```
    
    > **Note:** Any `<PackageReference>` in your projects can now omit the `Version="…"`.  
    > The MSBuild property `<ManagePackageVersionsCentrally>` tells all projects under this folder to look here for version numbers.
    

## 2. Update Your Projects

Open each `.csproj` in your solution and:

1. **Remove** all `Version="…"` attributes from `<PackageReference>` items.
2. **(Optional)** If you have legacy projects where you need per‑project overrides, you can still specify a version:
    
    ```xml
    <ItemGroup>
      <!-- Will override the centrally defined version -->
      <PackageReference Include="Serilog" Version="2.11.0" />
    </ItemGroup>
    ```
    
3. A typical `<ItemGroup>` now looks like:
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <TargetFramework>net7.0</TargetFramework>
      </PropertyGroup>
    
      <ItemGroup>
        <!-- Versions are pulled from Directory.Packages.props -->
        <PackageReference Include="Newtonsoft.Json" />
        <PackageReference Include="Dapper" />
      </ItemGroup>
    </Project>
    ```
    

---

## 3. Restore & Verify

1. In your solution folder, run:
    
    ```bash
    dotnet restore
    ```
    
2. Build your solution:
    
    ```bash
    dotnet build
    ```
    
    You should see no complaints about missing or mismatched package versions.
    

---

## 4. Advanced Tips

- **Adding a new package**:
    
    1. Add its `<PackageVersion>` entry in **Directory.Packages.props**.
        
    2. Reference it in any project with `<PackageReference Include="…"/>`.
        
- **Transitive versions**:  
    Central versions also affect transitive dependencies; if a library you consume brings in `Foo.Bar` v1.2.3 and you define `Foo.Bar` v1.2.4 centrally, the higher version wins.
    
- **Consistency checks**:  
    Visual Studio’s NuGet UI will now gray out the version column for projects under central management.
    
- **Mixing with `Directory.Packages.targets`**:  
    If you need build‑time injection of package versions (e.g. for custom MSBuild logic), you can also author `Directory.Packages.targets` alongside your `.props`.
    

---

That’s it! You now have a single source of truth for all your NuGet package versions—easier upgrades, audits, and fewer merge conflicts.




---

You can use 

```
Version="[^"]*"
```
    
To match versions and mass remove them after moving them to the Directory.Pacakges.props file.