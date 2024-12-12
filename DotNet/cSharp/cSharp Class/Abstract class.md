---
keywords: Parent class with no implementation
---
#cSharp 

An abstract class is a class in object-oriented programming that cannot be instantiated on its own. Instead, it serves as a blueprint or template for other classes. Abstract classes are used to define common characteristics and behaviors that its derived class **should** inherit and implement. **Should as in it's required**.
- **Used for code reusability:** Abstract classes are useful when you have a group of classes that share common attributes and behaviors. By creating an abstract class with common members, you avoid duplicating code in multiple concrete classes.
- **Cannot be instantiated:** You cannot create objects (instances) of an abstract class directly. It's meant to be a base class for other classes to inherit from.
- **Can use non abstract methods:** an abstract class can still use non abstract methods, the only requirements for an abstract class is that it needs to be inherited. Non abstract methods by the abstract class can only be used by its derived class.
Use abstract class when you have concept that can encompass, example:
```c#
public abstract class Shape // Abstract base class
{
    public abstract double CalculateArea(); // Abstract method for calculating area
    
	//can also use non abstract method see Copy method
	public void Copy() // can only be used by children/derived classes
	{ 
	//code
	}
}

public class Circle : Shape // Derived class for circles
{
    public override double CalculateArea()
    {
        return Math.PI * Math.Pow(Radius, 2);
    }
}

public class Rectangle : Shape // Derived class for rectangles
{
    public override double CalculateArea()
    {
        return Width * Height;
    }
}
```
