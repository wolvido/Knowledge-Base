#cSharp 
keywords:
	reuse code but not inheritance
see [[When to use coupling vs inheritance]]

Example:
```c#
// A simple class representing a car engine.
public class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine started.");
    }
}

// A Car class composed of an Engine.
public class Car
{
    private Engine engine; // Composition: Car has-an Engine.

    public Car()
    {
        engine = new Engine(); // Create an Engine instance when a Car is created.
    }

    public void StartCar()
    {
        engine.Start(); // Delegating the Start method to the Engine component.
        Console.WriteLine("Car is moving.");
    }
}
```
- The `Car` class is composed of an `Engine` instance.
- The `Car` class doesn't inherit from `Engine`, but it uses composition to include an `Engine` as one of its components.
- When you call the `StartCar` method on a `Car` object, it delegates the `Start` method call to the `Engine` component.

so basically a class is composed of another class.