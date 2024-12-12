Simply put, the **Liskov Substitution Principle (LSP)** states that object/instance of a base class should be replaceable with object/instance of its subclasses without breaking the application, but that doesn't mean the subclass should be replaceable with the base class, because a derive type can act as its base type, but a base type can act as anything that is not the derive type.

Essentially, child classes should be designed in a way that it is able to substitute the parent class, but not vice versa. Child class should only be a specialization of the parent class, but would still have the same purpose.
>[!info] Note
>Child types are also called sub types and parent types also called supertypes.
#### 4 Rules of LSP
##### 1. [Preconditions](https://en.wikipedia.org/wiki/Precondition "Precondition") cannot be strengthened in the subtype.
A precondition refers to a condition or requirement that must be true before a particular method is invoked. Preconditions are used to establish the valid state of the system or object before executing a certain action. "Strengthen" in a sense of more stricter rules; you cannot impose stricter or more restrictive preconditions on the methods or operations inherited from the supertype.

For example, a supertype `Vehicle` with a method `startEngine()` that requires a precondition that the vehicle has enough fuel. If you have a subtype `ElectricVehicle` inheriting from `Vehicle`, and `ElectricVehicle` needs enough fuel and also a battery charge, that is breaking LSP.
###### To make sure that the subtype `ElectricVehicle` does not break the principle of not strengthening preconditions:
- **Maintain the Same Preconditions:** Keep the preconditions for methods inherited from the `Vehicle` supertype the same for `ElectricVehicle`. In the case of `startEngine()`, you would design it so that it will not check if there is both fuel and battery, it should only check if there is enough energy (either from the battery or another power source) to initiate the engine start, or for pure battery electric vehicles just replace the fuel and check for enough electricity for start engine.
- **Weaken Preconditions:** If the preconditions inherited from the supertype are not applicable to the subtype, you can weaken them. For example, if the `Vehicle` supertype has a method `refuel()` that requires access to a fuel pump, and `ElectricVehicle` doesn't require refueling in the same way, you might weaken the precondition for `refuel()` in the `ElectricVehicle` subtype to simply require access to a charging station.
- **Introduce Specific Methods:** If the behaviors of the subtype diverge significantly from those of the supertype, it might be appropriate to introduce new methods that are specific to the subtype. For instance, you could have a method `chargeBattery()` specific to `ElectricVehicle`, which is not present in the `Vehicle` supertype, and when `refuel()` method is called, simply call `chargeBattery()`.
---
##### 2. [Postconditions](https://en.wikipedia.org/wiki/Postcondition) cannot be weakened in the subtype.
Postconditions refer to conditions or guarantees that are expected to hold true after a method or operation is executed. "Weaken" in a sense of less guaranteed rules; you cannot lessen the guarantee of the postconditions on the methods or operations inherited from the supertype.

Suppose we have a supertype `Vehicle` with a method `drive(distance)` that guarantees the vehicle will move the specified distance when invoked. The postcondition here is that after calling `drive(distance)` on a `Vehicle`, the vehicle should have moved the specified distance. If `ElectricVehicle` weakens the guarantee and say the vehicle will maybe move the specified distance or not depending on the battery temperature, that breaks LSP.
###### To make sure that the subtype `ElectricVehicle` does not break the principle of not weakening preconditions:
- **Maintain the Same Postcondition:** The `ElectricVehicle` subtype should moves the specified distance after calling `drive(distance)` on an electric vehicle, just like any other vehicle. The behavior remains consistent with the supertype.
- **Strengthen the Postcondition:**  The postcondition could be strengthened in the `ElectricVehicle` subtype. For instance, it could guarantee not only that the vehicle has moved the specified distance but also that it will move on traditional fuel and battery power (hybrid) and also that it will move regardless of battery temperature.
---
##### 3. [Invariant](https://en.wikipedia.org/wiki/Class_invariant "Class invariant") cannot be weakened in the subtype.
Invariants are **properties** or **conditions** that remain unchanged throughout the lifetime of an object. It must be true throughout the lifetime of an object, compared to postcondition that is only true after, and precondition that is only true before initiation. "Weakened" in a sense of less guaranteed condition or non-effective property.

Suppose the supertype `Vehicle` has an invariant `_functionalPowerSource`. This means always having a functional fuel tank for traditional vehicles. If the `ElectricVehicle` subtype weakens this invariant by allowing instances where the battery may not be functional sometimes depending on the temperature of the battery, then it breaks LSP.
###### To make sure that the subtype `ElectricVehicle` does not break the principle of not weakening Invariants:
- **Maintain the Same Invariant:** `_functionalPowerSource` of `ElectricVehicle` must always be functional at all times regardless of battery temperature.
- **Strengthen the Invariant:** `_functionalPowerSource` of `ElectricVehicle` must always be functional and can also draw power from traditional fuel or battery power (hybrid) and that it may also draw power from an emergency power source.
---
##### 4. History constraint (the "history rule").
The history rule states that the behavior of the object must follow the "historical behavior" of the base class. While Invariant rule is for properties and condition, the history rule is for the behaviour.
###### Example: 
Imagine a robot class that has a `move(x,y,z)` method, x,y,z for coordinates.
```c#
public class Robot
{
	public void Move(int x, int y, int z)
	{
		//move to the coords...
	}
}
```
Now imagine a sub class called that adds the method `GoBackToBase()`, but does not make use of the move method of the base class.
```c#
public class FasterRobot : Robot
{
	public void GoBackToBase()
	{
		//does not implement Move() here, instead creates its own implementation
	}
}
```
This violates the History rule.
>[!warning]
>To be honest, I'm not exactly sure what the history rule is, even Harsha doesn't teach it.
---
##### 5. - Subtypes cannot introduce new exceptions unless they are subtypes of exceptions in the base class
- **New Exceptions Cannot Be Thrown:** A subtype , it should not throw new exceptions that are not already thrown by the corresponding method in the supertype (base class). 
- **Exception Subtypes:** The only exception (pun definitely intended) to the rule above is that the subtype can throw exceptions that are subtypes of the exceptions thrown by the supertype. This means that the exceptions thrown by the subtype's methods can be more specific or specialized versions of the exceptions thrown by the supertype's methods.
Sample:
```c#
public class BaseClass
{
    public virtual void DoSomething()
    {
        throw new Exception("BaseClass exception");
    }
}

public class SubClass : BaseClass
{
    public override void DoSomething()
    {
        // This is valid since InvalidOperationException is a subtype of Exception
        throw new InvalidOperationException("SubClass exception");
    }
}

```
---
##### 6.  [Contravariance](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science) "Covariance and contravariance (computer science)") of method parameter types in the subtype and [Covariance](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science) "Covariance and contravariance (computer science)") of method return types in the subtype.
A base class instantiated cannot be assigned to a derive type reference, because a base type can be anything and its derived type is just one of those things. It would break the code if the base class is so far different than the derive. It violates [[Liskov Substitution Principle (LSP)]]
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

**NOTE**: In all the SOLID principles, this is the one that should be followed religiously, dogmatically. Seriously.