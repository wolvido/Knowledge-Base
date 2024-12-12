---
keyword: what is event
---
#cSharp 
**Important Note**: don't be confused with `event` event is not a data type or an access modifier, it is set alongside access modifiers but is not an modifier, it acts differently, it is a specially made keyword for events.
###### rundown sample:
```c#
public class Publisher
{
    // Declare an event field
    public event EventHandler MyEvent; //EventHandler is a built-in delegate, see Delegate Built-ins note
    
    protected virtual void RaiseEvent() //event raiser method
    {
        if (MyEvent != null) // Check if there are subscribers to the event field
        {
	        // Raise the event, which will call all subscribed methods
            MyEvent(this, EventArgs.Empty); //Event args is just empty for this sample
            //`this` is this class of course, the source of the event
        }
    }
}

public class Subscriber
{
	//the event handler method to be injected in the event raiser through the EventHandler delegate
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
        
	    // inject the event handler to the delegate field, essentially subscribing so the event raiser can execute it
        publisher.MyEvent += subscriber.HandleEvent;
        
        // Raise the event, which will call all the subscribed event handling method injected in the field.
        publisher.RaiseEvent();
    }
}
```
if youre confused with the += see [[+= delegate multicast and event subscribe]].
#### Conventions:
event publisher/ raiser should be protected virtual and void, and the name should start with On
```c#
protected virtual void OnPublished()
{
}
```
###### Naming:
- name the event past tense to indicate it has finished
- name the event present tense to indicate the event should be fired before it is started
---
### **What is EventArgs?**
is a class that serves as the base class for all classes that represent event data. Its a convention, it contains nothing. 
You will need to replace `EventArgs.Empty` with a real custom event data deriving from EventArgs.

To create a custom event data class, create a class that derives(via inheritance) from the [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/system.eventargs?view=net-7.0) class and provide the properties to store the necessary data. The name of your custom event data class should end with `EventArgs` as per convention.

Sample:
```c#
// in previous sample we used `EventArgs.Empty` for the event data since we didnt have an event data
// now we make a custom event data class to pass a data to the event
// its is a specialized custom event data, so it derives from EventArgs as convention
public class VideoEncodingEventArgs : EventArgs //custom event data class
{
    public string VideoName { get; private set; }

    public VideoEncodingEventArgs(string videoName)
    {
        VideoName = videoName;
    }
}

// Publisher class that represents a video encoder
public class VideoEncoder
{
    // Declare an event for video encoding completion
    public event EventHandler<VideoEncodingEventArgs> VideoEncoded;
    // VideoEncodingArgs is the type of data to be passed to the handler
    
    public void EncodeVideo(string videoName)
    {
        Console.WriteLine($"Encoding video: {videoName}");
        
        // Simulate video encoding process
        Thread.Sleep(5000); // Simulate encoding taking 5 seconds
        
        Console.WriteLine($"Video encoding completed: {videoName}");
        
        // Raise the VideoEncoded event
        OnVideoEncoded(videoName);
    }
    
	protected virtual void OnVideoEncoded(string videoName)
	{
	    // Check if there are subscribers to the event
	    if (VideoEncoded != null)
	    {
		    // in previous sample we used `EventArgs.Empty` since we didnt need any event data
			//now we need set the event raiser to use our custom event data class along with data `videoName`
	        VideoEncoded(this, new VideoEncodingEventArgs(videoName)); //
	    }
	}
}

// Subscriber class that represents a video upload service
public class VideoUploadService
{
	//the event handler will also use the custom event data class
    public void UploadVideo(object sender, VideoEncodingEventArgs e)
    {
        Console.WriteLine($"Uploading video: {e.VideoName} to the cloud storage");
    }
}

public class Program
{
    public static void Main()
    {
        VideoEncoder encoder = new VideoEncoder();
        VideoUploadService uploader = new VideoUploadService();
        
        // Subscribe the UploadVideo method to the VideoEncoded event
        encoder.VideoEncoded += uploader.UploadVideo;
        
        // Encode a video, which will trigger the VideoEncoded event
        encoder.EncodeVideo("example_video.mp4");
    }
}
```
---
To know when to use Event Handling see:
### [[When to Use Event Handling]]