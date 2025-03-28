---
tags:
  - aspire
  - dot-net
  - replicas
  - hosting
---
### What is .WithReplicas(x) in .NET Aspire?

​In .NET Aspire, the `WithReplicas` method is used to configure the application host to start multiple instances (replicas) of a specified project. This is particularly useful for simulating scaled-out scenarios during development and testing. By default, when multiple replicas are configured, the application host automatically starts a reverse proxy to load balance traffic between these replicas. 

**Usage Example:**

```csharp
var builder = DistributedApplication.CreateBuilder(args);  

builder.AddProject<Projects.InventoryService>("inventoryservice")        
	.WithReplicas(3);
```

In this example, three instances of the `InventoryService` project are started, and the reverse proxy distributes incoming traffic among them. 

**Considerations:**

- **Dashboard Visibility:** Be aware that when transitioning from a single instance to multiple replicas, the main service may no longer appear in the dashboard as expected. Instead, only the replicas might be displayed. This behavior is noted in the .NET Aspire GitHub repository. ​
- **Load Balancing Limitations:** The default load balancer operates at the TCP level, which may not effectively distribute HTTP requests across replicas. Consequently, you might observe that all requests are routed to a single replica. Addressing this requires additional configuration or alternative load-balancing strategies.

It's also advisable to avoid using the `WithReplicas` method with projects that perform database migrations, as this could lead to conflicts or unintended behavior.

