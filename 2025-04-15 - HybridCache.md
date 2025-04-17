# IDistributedCache ⇒ HybridCache

- **"Just works" for most cases**
- **Enhanced features:**
  - Built-in serialization
  - Stampede protection
  - L1/L2 (in-process/out-of-process) support
  - Efficient low-allocation API
  - Tagging and invalidation
  - And more!
- **More advanced options available when needed**
- **Works with existing cache backends**
- **Supports older .NET versions**
  - `Microsoft.Extensions.Cache.Hybrid`

---
### Example:

```csharp
public class SomeService(HybridCache cache)
{
    public async Task<SomeInfo> GetSomeInfoAsync(
        string name, int id, CancellationToken token = default)
    {
        return await cache.GetOrCreateAsync(
            $"{name}-{id}", // Unique key to the cache entry
            async cancel => await DataSource.GetDataAsync(name, id, cancel),
            token: token);
    }
}
