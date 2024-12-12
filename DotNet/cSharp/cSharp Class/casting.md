---
keywords: |-
  downcasting c#
  upcasting c#
  convert from subclass to baseclass
  convert from baseclass to subclass
  comma before value
---
#cSharp 
# Upcasting:
from subclass to baseclass
```c#
class Animal { }
class Dog : Animal { }

Dog dog = new Dog();
Animal animal = dog; // Upcasting (implicit)
```
implicit casting is always used in upcasting because it is safe, no changes are happening when upcasting.
# Downcasting:
```c#
Animal myAnimal = new Dog();
Dog dog = (Dog)myAnimal; // Downcasting (explicit), explicit downcasting is unsafe, use 'as' or 'is' if possible
```
Downcasting needs to be explicit because it is unsafe, not all baseclass can be used the same way as its subclass.
>[!warning]
Explicit downcasting is considered unsafe, use is or as see: [[is as]].
