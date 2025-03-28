# HybridCache in .NET (Microsoft.Extensions.Caching.Hybrid)

Microsoft.Extensions.Caching.Hybrid is now officially stable as of version **9.3.0**. This library enables fast L1 + L2 caching in .NET applications, combining local in-memory cache with distributed caching (e.g., Redis) to improve performance and scalability.

## 🔥 Why Use HybridCache?

HybridCache provides a **multi-layered caching approach**:

- **L1 Cache** (Local, In-Memory) - Fast retrieval but limited by memory size.
- **L2 Cache** (Distributed, e.g., Redis) - Shared across multiple application instances.
- **Automatic Cache Miss Handling** - If L1 misses, it retrieves from L2 before querying the source.

## 📦 Installing HybridCache

Before using HybridCache, install the NuGet package:

```sh
 dotnet add package Microsoft.Extensions.Caching.Hybrid
 dotnet add package Microsoft.Extensions.Caching.StackExchangeRedis
 dotnet add package Microsoft.Extensions.Caching.SqlServer
```

## ⚙️ Configuring HybridCache in ASP.NET Core

Modify your `Program.cs` or `Startup.cs` to add HybridCache with Redis as L2:

```csharp
using Microsoft.Extensions.Caching.Hybrid;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddHybridCache(options =>
{
    options.DefaultEntryOptions = new HybridCacheEntryOptions
    {
        LocalCacheExpiration = TimeSpan.FromMinutes(1), // L1 cache expiry
        Expiration = TimeSpan.FromMinutes(5) // L2 cache expiry
    };
});

// Register Redis as the distributed cache
builder.AddRedisDistributedCache("redis");

var app = builder.Build();
```

## 🛠 Using HybridCache in a Service

HybridCache simplifies caching logic by providing an easy-to-use API. Below is an example service that caches results:

```csharp
public class SomeService
{
    private readonly HybridCache _cache;

    public SomeService(HybridCache cache)
    {
        _cache = cache;
    }

    public async Task<string> GetSomeInfoAsync(string name, int id, CancellationToken token = default)
    {
        return await _cache.GetOrCreateAsync(
            $"{name}-{id}", // Unique key for cache entry
            async cancel => await GetDataFromTheSourceAsync(name, id, cancel),
            cancellationToken: token
        );
    }

    private async Task<string> GetDataFromTheSourceAsync(string name, int id, CancellationToken token)
    {
        // Simulate data fetching
        await Task.Delay(100, token);
        return $"someinfo-{name}-{id}";
    }
}
```

### Explanation:

- The method `GetSomeInfoAsync` first checks if the data is available in **L1 or L2 cache**.
- If **cache miss** occurs, it retrieves data from the source (`GetDataFromTheSourceAsync`).
- The retrieved data is then **stored in both L1 and L2 caches** for future access.

## 📌 HybridCache Best Practices

### ✅ Use a Unique Cache Key

Always ensure cache keys are **unique and consistent** for stored values.

```csharp
$"user-{userId}-profile"
```

### ✅ Choose Expiry Times Wisely
Balance **performance and data freshness** by configuring appropriate cache expiration times.

### ✅ Monitor Cache Performance
Use logging and telemetry to track **cache hit/miss rates** and adjust settings accordingly.

### ✅ Consider Cache Invalidation
If your data changes frequently, ensure cache invalidation strategies are in place.


# How to see redis keys in Docker


```sh
# Check Running Containers
docker ps

# Access the Redis Container
docker exec -it bde87eb4d7df bash

# Run the Redis CLI
redis-cli

# Check Stored Keys
keys *
```


## 🔗 References

1. [HybridCache library in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/hybrid?view=aspnetcore-9.0) - Microsoft Documentation.
2. ["HybridCache is finally stable!!! FAST L1 + L2 Cache in .NET"](https://www.youtube.com/watch?v=wlNHmZHQ5sY) - Milan Jovanovic on YouTube.

---

🚀 **Now you're ready to implement blazing-fast caching in your .NET apps using HybridCache!**