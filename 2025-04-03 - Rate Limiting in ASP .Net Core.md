**Rate limiting** is about restricting the number of requests to your application. It's usually applied within a specific time window or based on other criteria.

It's helpful for a few reasons:

- Improves security
- Guards against DDoS attacks
- Prevents overloading of application servers
- Reduces costs by preventing unnecessary resource consumption

Here's how to define a **rate limit policy** by calling the `AddTokenBucketLimiter` method:

```csharp
```csharp
builder.Services.AddRateLimiter(options =>
{
    options.AddPolicy("fixed-by-ip", httpContext =>
        RateLimitPartition.GetFixedWindowLimiter(
            partitionKey: httpContext.Connection.RemoteIpAddress?.ToString(),
            factory: _ => new FixedWindowRateLimiterOptions
            {
                PermitLimit = 10,
                Window = TimeSpan.FromMinutes(1)
            }));
});
```

```
You also have to add the `RateLimitingMiddleware` to the request pipeline:
```

```csharp
app.UseRateLimiter();
```


If your application is running behind a **reverse proxy**, you need to make sure not to rate limit the proxy IP address. Reverse proxies usually **forward** the original IP address with the `X-Forwarded-For` header. So you can use it as the **partition key**:

```csharp
builder.Services.AddRateLimiter(options =>
{
    options.AddPolicy("fixed-by-ip", httpContext =>
        RateLimitPartition.GetFixedWindowLimiter(
            httpContext.Request.Headers["X-Forwarded-For"].ToString(),
            factory: _ => new FixedWindowRateLimiterOptions
            {
                PermitLimit = 10,
                Window = TimeSpan.FromMinutes(1)
            }));
});
```

## [Rate Limiting Users By Identity](https://www.milanjovanovic.tech/blog/advanced-rate-limiting-use-cases-in-dotnet?utm_source=X&utm_medium=social&utm_campaign=31.03.2025#rate-limiting-users-by-identity)

If you require users to **authenticate** with your API, you can determine who the current is. Then you can use the user's **identity** as the **partition key** for a `RateLimitPartition`.

Here's how you would create such a rate limit policy:

```csharp
builder.Services.AddRateLimiter(options =>
{
    options.AddPolicy("fixed-by-user", httpContext =>
        RateLimitPartition.GetFixedWindowLimiter(
            partitionKey: httpContext.User.Identity?.Name?.ToString(),
            factory: _ => new FixedWindowRateLimiterOptions
            {
                PermitLimit = 10,
                Window = TimeSpan.FromMinutes(1)
            }));
});
```

I'm using the `User.Identity` value on the `HttpContext` to get the current user's `Name` claim. This usually corresponds to the `sub` claim inside a JWT - which is the user identifier.