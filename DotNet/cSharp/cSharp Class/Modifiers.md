---
keywords: class modifiers
---
#cSharp 
###### Access Modifiers:  
- public: The member is accessible from any code.
- private: The member is accessible only within the containing type.
- protected: The member is accessible within the containing type and its derived types.
- internal: The member is accessible within the current assembly. see [[What is Namespace, Assembly or Dynamically Linked Library (DLL)]]
- protected internal: The member is accessible within the current assembly and its derived types.
###### Field Non-Access Modifiers:  
- readonly: The field can only be assigned a value during declaration or in a constructor and cannot be modified afterwards. **Note:** objects of readonly reference types can still be modified but the pointer is immutable. Value types are completely immutable.
- const: The field is a compile-time constant, and its value cannot be changed. 
- volatile: The field is subject to synchronized access in multithreaded scenarios.  
###### Method or Class Non-Access Modifiers:  
- static: The member belongs to the type itself rather than to an instance of the type.  
- <mark style="background: #BBFABBA6;">virtual</mark>: The method can be overridden in derived classes. Use this if you plan on creating derived classes that creates specialized version of the method.
- <mark style="background: #BBFABBA6;">abstract</mark>: The class must be inherited. The method must be overridden. It is like virtual but it has no implementation, it only serves as an interface of sorts to use specialized versions from derived classes. Basically in certain cases(not all) use this instead of virtual if your virtual has no implementation. **note**: when using abstract methods, the class also needs to be abstract.  see [[Abstract class]].
- override: The method overrides a <mark style="background: #BBFABBA6;">virtual</mark> or an <mark style="background: #BBFABBA6;">abstract</mark> method from a base class. see [[Method Overriding]]
- sealed: class or method cannot be inherited or overridden, only works with methods with override. **note**: nobody really uses it, and is considered bad use by mosh, only use if you have a really good reason.
- extern: The method is implemented externally in another programming language.
- new: The member hides a member of the base class with the same name.  
- params: The method accepts a variable number of arguments as a parameter array.  see [[params]]
###### Parameter Non-Access Modifiers:  
- ref: The parameter is passed by reference rather than by value.  
- out: The parameter is used to return a value from a method.
