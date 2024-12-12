The IoC container is responsible for creating, managing, and injecting dependencies into the components that request them.
1. **Inversion of Control (IoC):** IoC is a design principle where the control of the flow of a program is inverted. Instead of a component controlling the instantiation and management of its dependencies, the control is inverted to an external container or framework.
    
2. **Dependency Injection (DI):** DI is a specific implementation of IoC, where dependencies are "injected" into a component rather than the component creating or managing its dependencies. This promotes loose coupling and easier testing.
    
3. **IoC Container:** An IoC container is a framework or library that manages the instantiation and lifetime of objects, as well as the injection of dependencies. It typically includes a container class that holds registrations of types and their dependencies.
    
4. **Registration:** In an IoC container, you register types and their dependencies. This involves telling the container how to create instances of different types and how to fulfill the dependencies of those types.
    
5. **Resolution:** When a component needs an instance of a type, it asks the IoC container to resolve that type. The container then creates an instance, injects any required dependencies, and returns the fully constructed object.
    
6. **Lifetime Management:** IoC containers often support different lifetime management options for registered types, such as transient (a new instance every time), scoped (a single instance per scope, e.g., per HTTP request), and singleton (a single shared instance).

in net core MVC injecting them looks like here:
[[Services - Service layer]]