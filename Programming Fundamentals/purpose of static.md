---
keywords: |-
  static methods
  Purpose of static
  static classes
---

The purpose is for a shareable tool that can be used when needed, it's like a css utility class. It makes no sense to instantiate this since its supposed to be used frequently. It is constant/unchanging.

-Static members
A shared tool for use in any appropriate need, example DateTime.Now or Math.PI or Console.WriteLine().

-Static classes
A static class is like a toolset that contains static members/tools. The purpose of a static class is to provide a convenient way to organize and access utility functions, shared functionalities, constants, aka static members. 
see [[Static class]]

By making the class static, it restricts the creation of instances and ensures that all members are accessible directly through the class itself. This promotes encapsulation, as the static class encapsulates related functionality within a single entity.

Instance vs static:
Instance is instantiated, it can only be called with the object, static is called directly.
