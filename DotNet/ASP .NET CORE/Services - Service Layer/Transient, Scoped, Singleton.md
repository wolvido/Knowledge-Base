---
keywords: |-
  Transient vs Scoped vs Singleton 
  Scopes of Services
---
In the context of DIC (Dependency Injector Container).
```c#
using Services;
using ServiceContracts;

builder.Services.AddTransient<ISampleService, SampleService>();
// or
builder.Services.AddScoped<ISampleService, SampleService>();
// or
builder.Services.AddSingleton<ISampleService, SampleService>();
```
###  What does it mean?
It means what the scope of the service is. It is when a service object is created by [[IoC]] Container and when it is destroyed.
- Transient - will create a service object **Per injection/per call/per DI request**(do not confuse with per http request)  and destroy it at the end of a scope(when the http request is completed). 
- Scoped - will create a service object per **scope(browser http request)** and also destroy it at the end of a scope(when the request is completed).
- Singleton - will create a service object for the entire application lifetime and destroyed at application shutdown.

So for example: We have a GUID generator service, and you have created three instance of the GUID generator:
- If the service is transient then every instance of the GUID service will generate three different GUID's object per page http reset. If the page is reset again all the three different GUID will change to another three unique GUID since three **call/DI request** is each created a single service lifetime. 
- If the service is scoped then the three instance of GUID service will generate the same GUID, since there is only one http request so the GUID service will only create one scoped lifetime of the GUID service, and every call/DI request of the service will have to share the same service lifetime. If the page is reset, then only it will generate a new GUID but the same for all three instance.
-  If the service is singleton then the three instance of GUID service will generate the same GUID.  If the page is reset, it will **NOT** generate a new GUID it will be the same for all three instance. It will only reset if the web app is shutdown not just a reset. Every call/DI request and http request will have to share a single service lifetime until the software is reset.
#### When to choose what?
- Use **transient** if the service if you need the service to only affect per browser request, something like a key generator service, or something very self contained that the data is temporary and does not need to be shared.
- Use **Scoped**  if you need a request wide process, like for example doing a set of transactions, so that every part of the transaction does not create its own lifetime, and the set of transaction would be intact.
- Use **Singleton** if you need something that every part of the program must know in its lifetime and does not rely on a request, most singleton run on startup for example logging or caching.
### Learn next:
- What if you need a specific scope **inside** the service that creates and destroys specific methods inside the service while the service instance exist. Instead of just waiting for the whole service to be destroyed by Transient, Scoped, or Singleton scope. For example your service creates a DB connection and that DB connection needs to be destroyed when its done being used instead of waiting for the whole service to be destroyed. see [[Service Scope]].
- What if `Program.cs` is filled with service registrations and it becomes unwieldy? [[Arrange Program.cs]]
- see: [[Best Practice for Services and DI]].

#### Unity Container
Transient = TransientLifetimeManager
Scoped = HierarchicalLifetimeManager
Singleton = ContainerControlledLifetimeManager

sample register:
```c#
// Transient lifetime - new instance each time 
container.RegisterType<IMyService, MyService>(new TransientLifetimeManager()); 
// Singleton-like - shared across the container 
container.RegisterType<IMyService, MyService>(new ContainerControlledLifetimeManager());
```
