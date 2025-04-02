How to make sure that rider auto formatting does not inline this :

```
        builder.ConfigureServices(x =>
        {
            x.AddMassTransit(configurator =>
            {
                configurator.UsingRabbitMq((_, cfg) =>
                {
                    cfg.Host("rabbitmq://localhost");
                });
            });
        });
```

Into this ugly mess : 

```
        builder.ConfigureServices(x => { x.AddMassTransit(configurator => { configurator.UsingRabbitMq((_, cfg) => { cfg.Host("rabbitmq://localhost"); }); }); });
```


### **Steps to Preserve Formatting in Rider**
1. **Format Your Code Manually**
    - Arrange your code exactly as you want it to appear.
2. **Select the Code Block**
    - Highlight the portion of code you want to protect from automatic inlining.
3. **Use Detect Formatting**
    - Press `ALT + Enter`
    - Navigate to **Reformat Code > Detect Formatting**.
    - This tells Rider to recognize and apply your current formatting style.
4. **Apply Auto-Formatting** (Optional)
    - Now, when you use **Code Cleanup** or **Reformat Code (**`**Ctrl+Alt+L**`**)**, Rider will respect your detected formatting instead of inlining your code