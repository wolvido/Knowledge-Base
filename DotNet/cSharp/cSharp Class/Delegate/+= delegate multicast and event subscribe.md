---
keywords: what does += mean in terms of method += another method from a different class
---
#cSharp 
the `+=` operator is used for event subscription and delegate combination.  `+=` allows you to add the method in a delegate type field, the field then stores multiple methods which essentially  acts like a list of methods that the event raiser or delegate handler can run all the methods subscribed to that list.

If youre confused about how a method can be subscribed to another method, no you're not subscribing to another method, you are subscribing a method to a **delegate field** which can hold a method, the event raiser or delegate handler will handle it.

This is commonly used for implementing event handlers.
simple example:
```c#
public class Publisher
{
    // Declare an event using EventHandler delegate
    public event EventHandler MyEvent; //EventHandler is a built in of delegate
    
    public void RaiseEvent() //this is the event raiser or delegate handler
    {
        // Check if there are subscribers to the event
        if (MyEvent != null)
        {
            // Raise the event, which will call all subscribed methods
            MyEvent(this, EventArgs.Empty);
        }
    }
}

public class Subscriber
{
    public void HandleEvent(object sender, EventArgs e)
    {
        Console.WriteLine("Event handled by Subscriber");
    }
}

public class Program
{
    public static void Main()
    {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();

        // Subscribe the HandleEvent method to the MyEvent event
        publisher.MyEvent += subscriber.HandleEvent;

        // Raise the event, which will call the HandleEvent method
        publisher.RaiseEvent();
    }
}
```