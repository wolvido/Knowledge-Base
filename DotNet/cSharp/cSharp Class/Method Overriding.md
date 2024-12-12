---
keywords: |-
  change method in base class
  different method in subclass
  creating a modified method of a baseclass
---
#cSharp 
Overrides from the virtual or abstract method.
```c#
class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Some generic animal sound.");
    }
}

class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
}

class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Meow!");
    }
}
```
can also use abstract modifier instead of virtual, if you are planning to make a virtual that has no implementation. see [[Modifiers]] for more details.
Basically abstract modifier is just like virtual without implementation, example:
```c#
abstract class Animal // Abstract class
{
    public abstract void MakeSound(); // Abstract method (no implementation)
}

class Dog : Animal // Concrete subclass
{
    public override void MakeSound() // Implementing the abstract method
    {
        Console.WriteLine("Dog barks");
    }
}

class Cat : Animal // Concrete subclass
{
    public override void MakeSound() // Implementing the abstract method
    {
        Console.WriteLine("Cat meows");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Animal dog = new Dog();
        Animal cat = new Cat();

        dog.MakeSound(); // Calls MakeSound in Dog class
        cat.MakeSound(); // Calls MakeSound in Cat class
    }
}
```