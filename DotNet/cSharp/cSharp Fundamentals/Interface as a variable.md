---
keywords: |-
  initialized interface
  interface as a data type
  interface initialized
  interface holding data
---
#cSharp 
sample:
```c#
IInterfaceSample sampleVariable = new SampleClass(sample, sample2);
```
**Interface as a variable why?**
Lets say you have:
```c#
interface IAnimal 
{
    void Euthanize();
}

public class Dog : IAnimal
{
    void Euthanize()
    {
	    Console.Writeline("cat poison injection");
    }
}
 
public class Cat : IAnimal
{
    void Euthanize()
    {
	    Console.Writeline("dog poison injection");
    }
}

public class AnotherAnimalEtc : IAnimal
{
	// euthanize implementation
}
//so on and so forth many animal implementations
```
- Now, you need to find the animal to euthanize, you use `AnimalFinder` utility class.
- So first you store it in a variable called `animalToEuthanize`.
- But wait, what data type should the `animalToEuthanize` have If the `AnimalFinder` can return a Dog type or a Cat type or anything.
```csharp
Cat animalToEuthanize = AnimalFinder.FindByName("kevin"); //Kevin might be a dog or a giraffe, that would throw an error
```
So that's why you use:
```c#
IAnimal animalToEuthanize = AnimalFinder.FindByName("kevin");
```
any result of `AnimalFinder` would not throw an error, as long as  `AnimalFinder` returns an animal.

>[!info]
>If you got confused about an interface used as a function, dont be, its not used as a function that makes no sense, 
>its probably used as the **return** type of the function 
