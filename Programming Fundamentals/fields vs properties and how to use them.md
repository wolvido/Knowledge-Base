Imagine a car. The volume of petrol in the tank would be stored as a field - your car doesn't indicate how many liters are actually available. You may have a Car with two private fields - fuelTankSize and remainingFuel -, this info is important to the car to function, but not important to you as a consumer/driver. 

For you to know the remaining fuel, it would have a property of PercentageFuelRemaining - this would be a calculation of remainingFuel / fuelTankSize.  Properties are aspects of your object interesting to those consuming it. Fields are aspects of your object that it requires to function.  

Fields are also often initialized in the constructor, in the sense that the Object you're creating wouldn't meet the criteria of being that object without these parameters (fields).  
  
People use properties, especially mutable ones, too much, and should consider exposing methods to modify fields rather than just exposing a property.