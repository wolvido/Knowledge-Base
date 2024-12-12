#cSharp 
```c#
public class Person  
{  
	private string _name;  
	public string Name  
	{  
		get { return _name; }  
		set { _name = value; }  
	}  
}  
```
**what is the purpose of properties?**
Encapsulation, it should handle the getting and the setting of a field, field should not be exposed. Only Properties should be exposed see: [Why Properties Matter (csharpindepth.com)](https://csharpindepth.com/Articles/PropertiesMatter) for explanation. 
- A property communicates the idea of "I will make a value available to you, or accept a value from you." 

If you only need a simple get set/glorified public field, ditch private and use an auto property or if you need  a temporary property. see [c# - Should I use automatic properties?](https://softwareengineering.stackexchange.com/questions/226450/should-i-use-automatic-properties)
##### auto getter:
```c#
public string Name {get; set;} //auto property
```
this is short for:
```c#
private string _name;
public string Name
{
    get{return this._name;}
    set{this._name = value;}
}
```
Note: you cannot modify the field of an auto property.

for shorter get only:  
```C#
public string Name => _name;  
```

for syntactic sugar use:  
```C#
public string Name  
{  
get => return _name;  
set => _name = value;  
}  
```

to use:  
```C#
var person = new Person();  
var person.Name = "winz"; //set  
var string name = person.Name //get  
Console.WriteLine(person.Name);  
```

More complicated calculated property sample:
```c#
public class CityWeather
{
	public int TemperatureFahrenheit { get; set; }
	
	public string BkgColorByTemperature
	{
		get
		{
			return TemperatureFahrenheit switch
			{
				(< 44) => "bkg-blue",
				(>= 44) and (< 75) => "bkg-green",
				(>= 75) => "bkg-orange"
			};
		}
	}
}
```
Explanation: **`BkgColorByTemperature`** property has no set since it only acquires data from **`TemperatureFahrenheit`**, its get is calculated based on **`TemperatureFahrenheit`**.
#### Notes:  
- if your confused on whether to use/add a property to a field or use a local variable, see: [[fields vs local variables]].
- if you're confused whether a method should expose a field or modify a field, don't worry fields can be exposed and modified directly by a method.
- code snippet:  prop.
- You can add modifiers to your properties for better encapsulation, ex: if you want a property to be set only in initialization you can set it into private like so:  `public string Name { get; private set; } //acts like a read only/get only `
- dont get confused when using underscore camelcase, mosh allows using auto properties along with underscore. In the constructors dont use this on fields with auto properties. see C# intermediate, section 2, vid 13, 16:16.