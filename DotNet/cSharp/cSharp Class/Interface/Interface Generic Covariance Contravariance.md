---
keywords: |-
  Generic in out
  interface in out
  interface generic in out
  what is in out
  in out
  out in
---
#cSharp 
##### covariant = to out
- I need a class that has a method that can produce a base type, I'll also accept a derived class version of the needed class since its derived version can produce a derived type that can also be considered a base type, per [[Liskov Substitution Principle (LSP)]].
- "I'll also accept a derived class version" this phrase means it is covariant.
Example:
```c#
//I need a fruit farm(base class) so i can produce fruits(base type)
//But what I have is an apple farm(derived class) that produce apples (derive type)
IProducer<Apple> appleFarm = new AppleProducer(); 
//thats ok, I'll just mark it as covariant(out) since apple is also a fruit
IProducer<Fruit> fruitFarm = appleFarm; 

Apple apple = appleFarm.Produce();
//I can produce fruits since apple is a fruit
Fruit fruit = apple; 
```
##### contravariant = to in
- I need a class that has a method that can consume a derive type,  I'll also accept the base class version of the needed class since the base class of this derive class can consume the base type and thus can consume the derive type per [[Liskov Substitution Principle (LSP)]].
- "I'll also accept the base class version" this phrase means it is contravariant
Example:
```c#
//I need an apple bakery(derive class) so i can use my apples(derive type)
//But what I have is a fruit bakery(base class) that uses fruits(base type)
IConsumer<Fruit> fruitBakery = new FruitConsumer();
//thats ok, I'll just mark it as contravariant(in) since a fruit bakery can also consume apples
IConsumer<Apple> appleBakery = fruitBakery;

//can consume apples and any fruits
fruitBakery.Consume(new Apple());
fruitBakery.Consume(new Fruit());
appleBakery.Consume(new Apple());
```

So basically:
- if you mark an interface generic as covariant, it must be able to **out**put the generic type and you'll be able to convert a derive type of the generic type into its base type.
```c#
IProducer<Apple> appleFarm = new AppleProducer(); 
IProducer<Fruit> fruitFarm = appleFarm; 

Apple apple = appleFarm.Produce();
Fruit fruit = apple; 
```

- if you mark an interface generic as contravariant, it must be able to **in**put the generic type and you'll be able to convert a derive type of the generic type into its base type.
```c#
IConsumer<Fruit> fruitBakery = new FruitConsumer();
IConsumer<Apple> appleBakery = fruitBakery;

fruitBakery.Consume(new Apple());
fruitBakery.Consume(new Fruit());
appleBakery.Consume(new Apple());
```

to understand why we do this, see [[Liskov Substitution Principle (LSP)]].

Full code:
```c#
public interface IProducer<out T>
{
    T Produce();
}
 
public class Fruit { }
 
public class Apple : Fruit { }
 
public class FruitProducer : IProducer<Fruit>
{
    public Fruit Produce() => new Fruit();
}
 
public class AppleProducer : IProducer<Apple>
{
    public Apple Produce() => new Apple();
}
 
public interface IConsumer<in T>
{
    void Consume(T item);
}
 
public class FruitConsumer : IConsumer<Fruit>
{
    public void Consume(Fruit item)
    {
        // Consume the fruit
    }
}
 
public class AppleConsumer : IConsumer<Apple>
{
    public void Consume(Apple item)
    {
        // Consume the apple
    }
}
```

