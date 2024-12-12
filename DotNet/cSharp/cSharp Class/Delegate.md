---
keywords: like interface but not interface
---
#cSharp 
Delegate are basically method data types, where you can store a method in a delegate variable as long as that method follows the contract, meaning same return type, same parameters.
Syntax:
```c#
[access modifier] delegate [return type] [delegate name]([parameters])
```
Sample:
```c#
// Define a delegate type for text processing methods
public delegate string TextProcessor(string input);

class TextProcessingTool
{
	// you can also declare a delegate inside the class like:
	// public delegate string TextProcessor(string input);
	// but is not recommeded since its suppose to be used by others
	// only do this if your sure the delegate is only going to be used by the class

    private TextProcessor _textProcessor; //delegate instance field
    
    public TextProcessingTool(TextProcessor processor) // constructor assigning the delegate injection to the field
    {
        _textProcessor = processor;
    }
    
    public void ProcessText(string input) //delegate handler
    {
        string result = _textProcessor(input); //delegate contract
        Console.WriteLine("Processed Text: " + result);
    }
    
	// using delegate instead of adding algorithms like:
	// public string Uppercase(string text)
	// {
		 // code
	// }
	// or
	// static string Reverse(string text)
	// {
		// something
	// }
	// instead of delegate, everytime you need to add a new process algo you have to modify the class
	// delegate instead allows extensibility you can easily just add whatever like an interface. see below:
}

class Program
{
    // Sample text processing methods
    static string Uppercase(string text)
    {
        return text.ToUpper();
    }
    
    static string Reverse(string text)
    {
        char[] charArray = text.ToCharArray();
        Array.Reverse(charArray);
        return new string(charArray);
    }
    
    static void Main()
    {
        // you can just add the algos here like an interface
        TextProcessingTool uppercaseTool = new TextProcessingTool(Uppercase);
        TextProcessingTool reverseTool = new TextProcessingTool(Reverse);
        
        // Process text using the different processors
        uppercaseTool.ProcessText("Hello, World!"); //Processed Text: HELLO, WORLD!
        reverseTool.ProcessText("C# Delegates"); //Processed Text: setagel eD #C
        
        // You can easily add more text processing methods without modifying the TextProcessingTool class.
    }
}
```
see [[Interface]] if youre confused. its basically just like interface.
**Note:** Delegates can also be created outside a class just like an interface, difference is you cant make an interface inside a class, see sample below.
```c#
// Define a delegate type for handling events.
public delegate void EventHandler(string message);

class EventPublisher
{
    // Declare an event using the delegate type.
    public event EventHandler MyEvent;
    
    // Method to raise the event.
    public void RaiseEvent(string message)
    {
        if (MyEvent != null)
        {
            MyEvent(message);
        }
    }
}

class Program
{
    static void Main()
    {
        EventPublisher publisher = new EventPublisher();
        
        // Subscribe multiple event handlers, this is called multicasting.
        publisher.MyEvent += EventSubscriber1;
        publisher.MyEvent += EventSubscriber2;
        
        // Raise the event, which will invoke both subscribed handlers.
        publisher.RaiseEvent("Hello, World!");
        //output: 
        // EventSubscriber1: Hello, World! 
        // EventSubscriber2: Hello, World!
        
        Console.WriteLine("\nRemoving EventSubscriber2 from the event...\n");
        
        // Unsubscribe one of the event handlers (extensibility).
        publisher.MyEvent -= EventSubscriber2; //removing EventSubscriber2 will only output EventSubscriber1
        
        // Raise the event again after unsubscribing EventSubscriber2.
        publisher.RaiseEvent("Hello again, World!");
        //output: EventSubscriber1: Hello again, World!
    }
    
    static void EventSubscriber1(string message)
    {
        Console.WriteLine("EventSubscriber1: " + message);
    }
    
    static void EventSubscriber2(string message)
    {
        Console.WriteLine("EventSubscriber2: " + message);
    }
}
```
The last example demonstrated multicasting.
if you're confused about `+=` see [[+= delegate multicast and event subscribe]]

---
## Why use delegates?
**For extensibility and flexibility just like interfaces. Which begs the question:**
##### [[When to use Delegates vs Interfaces]]

---
_**Sometimes for best practices you don't need to make your own delegate, there are built ins that are easy to use and more semantic see:_
#### [[Delegate Built-ins]]

