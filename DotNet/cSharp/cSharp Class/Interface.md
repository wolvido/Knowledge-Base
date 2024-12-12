#cSharp 
It sets the contract that a class should follow.
Interfaces allow you to define a common set of methods and properties that classes can adhere to, enabling great versatility thus polymorphism and code reusability. An interface is basically a placeholder for any class that can fulfill its use. It allows for greater extensibility, and decoupled polymorphism.
Its like a parent but only for behavior.
To really understand interface capabilities and demonstrate extensibility see: [[Interface Extensibility and Polymorphism]].

How to know when to use:
- **Polymorphism:** Interfaces enable polymorphism, allowing objects of different classes to be treated as instances of a common interface. If you need to work with objects generically and rely on polymorphism, interfaces are a valuable tool.
- **Decoupling**: If you foresee the need to switch out implementations or plug in different behaviors without affecting other parts of your code, interfaces can facilitate this decoupling. It has the ability to pass a class in an object, instead of an object requiring another object. So you pass the class into the object parameter and the object itself will insatiate the class itself, instead of instantiating it outside the object and be required by the requiring object.
- **Multiple Inheritance of Behavior:** a class can inherit from only one base class, but it can implement multiple interfaces. If you need to define a set of methods that different classes should implement, an interface is a good choice.
- **Abstraction of Commonality:** When you have several classes that share common behavior but don't necessarily have a common ancestor, interfaces can help abstract away this commonality. For example, if you have various classes that can be serialized, you can create an `ISerializable` interface to define the serialization contract.
- **Enforcing a Contract:** Use interfaces to enforce a contract or a specific set of methods that derived classes must implement. This ensures that classes adhering to the interface will have certain behavior, which can be useful for creating a consistent API.
- **Mocking and Unit Testing:** Interfaces are useful when writing unit tests. You can create mock implementations of interfaces to isolate and test components in isolation, without relying on concrete implementations.
	Interface is extremely advantageous in Unit Testing see [[Interface Unit Testing]]


