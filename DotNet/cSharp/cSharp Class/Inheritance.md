#cSharp 
keywords:
	c# inheritance
	inherit from other class
	create a child class from parent class
	class code reuse

see [[When to use coupling vs inheritance]]

There is a common reason to why extension through inheritance is hard. And that's because the relationship isn't a true `is-a` relationship, but that the developer just want to take advantage of the base class functionality.
That's wrong. Better to use [[Composition]].

**Base Class (Parent Class)**: This is the class that you want to derive from. It contains the common properties and behaviors shared by its child classes.
```c#
public class Vehicle
{
    public string Brand { get; set; }
    public int Year { get; set; }

    public void Start()
    {
        Console.WriteLine("Vehicle started.");
    }
}
```

**Derived Class (Child Class)**: This is the class that inherits from the base class. It can add additional properties and methods or override existing ones.
```c#
public class Car : Vehicle
{
    public int NumberOfDoors { get; set; }

    public void Honk()
    {
        Console.WriteLine("Honk honk!");
    }
}
```

**Using Inheritance**:
- Inherited members (properties, methods) can be accessed directly from the child class.
- You can also add new members or override inherited members.
```c#
Car myCar = new Car();
myCar.Brand = "Toyota";
myCar.Year = 2023;
myCar.NumberOfDoors = 4;
myCar.Start();  // Inherited method
myCar.Honk();   // New method
```

**Method Overriding**: Child classes can override methods from the base class to provide their own implementation. To enable this, mark the base class method as `virtual`, and in the child class, use the `override` keyword. See [[Method Overriding]].

**Access Modifiers**: Inheritance is subject to access modifiers. Members marked as `private` in the base class are not accessible in derived classes. Members marked as `protected` or `public` are accessible.

**Constructor Inheritance**: Constructors are not inherited but you don't have to rewrite the case constructor just call `base()` it acts like the base constructor. Its basically a method that runs the base constructor inside the child's constructor.
```c#
public class Car : Vehicle
{
    public Car(string brand, int year, int doors)
        : base(brand, year)
    {
        NumberOfDoors = doors;
    }

    // ...
}
```
Inheritance is a powerful feature in C# that promotes code reuse and helps you create well-organized, hierarchical class structures. However, it's essential to use inheritance judiciously and consider alternatives like composition when necessary to avoid tightly coupled and inflexible code.
#### **Important Notes and Possible Errors**:
- you cannot create a parameter-less constructor on the class child if the base class has no parameter-less constructor.
###### Liskov Principle
- A base class instantiated cannot be assigned to a derive type reference, because a base type can be anything and its derived type is just one of those things. It would break the code if the base class is so far different than the derive. It violates [[Liskov Substitution Principle (LSP)]]
```c#
Fruit fruit = null;
Apple apple = fruit; //error, violates liskov principle
```
- An instantiated derive can be held by a base class reference, since a derive is just another version of the base class.
```c#
Apple apple = null;
Fruit fruit = apple; //allowed
```
- Also a derived class instantiated to a base reference cannot call the derive's methods on the base reference, since the base class reference cannot and should not see the derive's methods, that way its encapsulated. One way it protects is it prevents your code from accidentally using the derive's methods when it is expecting the base type, since some derive can have more methods.