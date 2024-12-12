---
keywords: how await works
---
#cSharp 
Async allows you to continue running code while some intensive code runs in the background without waiting for it. 
For example you can read comments in YouTube while the video buffers.
#### How the hell does await and async mean, how does it work?
- Async means the method can hold an await code and will run in parallel if its code reaches an await.
- Await means, when the controller encounters an await, the control returns to the caller, meaning outside the async method and would execute something else in parallel of the awaited.
- Anything above the await is executed synchronously. Anything below the await will wait for the await to finish before executing.
- When the await is finished, the controller returns back to it, then continues on the codes below the await.
**Note**:
An Async method retuns a type Task, [[Why is task the return of Async]], read first if youre confused. So You cannot access the properties of an async method directly because it is a task callback, to get the real method it is extracted by adding await. Await executes the task and returns its real method.
###### syntax:
```c#
public async Task MyAsyncMethodAsync()
{
    // Asynchronous code here
}
//or with a concrete result/return
public async Task<int> MyAsyncMethodWithResultAsync()
{
    // Asynchronous code here
    return 42;
}
```
convention is to add Async to the last of an Async.
if your wondering what the difference with with generic and without see: [[Why is task the return of Async]]
###### Basic sample:
```c#
static void Main()
{
    DoSomethingAsynchronous();
    DoSomethingSynchronous();
    Console.ReadLine();
}
 
static void DoSomethingSynchronous()
{
    Task.Delay(1000).Wait(); //simulate a synchronous operation
    Console.WriteLine("synchronous method done");
}
 
static async Task DoSomethingAsynchronous()
{
    Console.WriteLine("above await");
    await Task.Delay(2000); // Simulate an awaited operation
    Console.WriteLine("below await");
}
```
###### Real sample:
```c#
namespace WebApp.Controllers
{
    public class UserController : Controller
    {
        public async Task<IActionResult> GetUserAsync(int userId)
        {
			// Simulate an asynchronous operation (e.g., fetching user data from a database or external service)
			var user = await FetchUserDataAsync(userId);
			
			View("UserProfile", user);
        }
        
        // Simulated asynchronous method to fetch user data
        private async Task<User> FetchUserDataAsync(int userId)
        {
        	// can also add a non async code here in the middle so you dont have to wait 
		    // and be able to utilize the thread to its fullest
            await Task.Delay(1000); // Simulate an asynchronous delay
            
            // Simulated user data retrieval
            var user = new User
            {
                Id = userId,
                Username = "john_doe",
                Email = "john.doe@example.com"
                // Other user properties
            };
		    

		    Console.Writeline("sample non async code. Waiting for the task to complete");
            
            return user;
        }
    }
    
    public class User
    {
        public int Id { get; set; }
        public string Username { get; set; }
        public string Email { get; set; }
        // Other user properties
    }
}
```
if youre wondering what if `var user = await FetchUserDataAsync(userId);` is  `Task<user> user = await FetchUserDataAsync(userId);` see: [[Why is task the return of Async]] at the bottom part.
###### How to convert void methods into asynchronous? see:[[Async void]].
## How it works:
#### `async` Method Declaration
- To define an asynchronous method, you use the `async` keyword in the method signature. For example:
```c#
async Task MyAsyncMethodAsync()
{
    // Asynchronous code goes here
}
```
####  `await` Keyword
Inside an asynchronous method, you can use the `await` keyword before an asynchronous operation. The `await` keyword tells the compiler to pause the execution of the method until the awaited operation is completed, but it doesn't block the calling thread. Instead, it allows other work to be done on that thread while waiting for the operation to complete. For example, you can use `await` with asynchronous methods that return a `Task`:
```c#
async Task MyAsyncMethod()
{
    // Await an asynchronous operation
    var result = await SomeAsyncOperationAsync();
    
    // Continue with the code after the operation is complete
    Console.WriteLine(result);
}
```
#### Calling an Async Method
When calling an asynchronous method, you typically use `await` as well, if you're calling it from another asynchronous method. This ensures that you don't block the calling thread.
```c#
async Task AnotherAsyncMethod()
{
    // Call the async method using await
    await MyAsyncMethodAsync();
    
    // Continue with other code
}
```
#### Task and Result Types
- Asynchronous methods typically return a `Task` or `Task<T>`. The `Task` represents the ongoing operation, if its declared in an await you will get the result or return when done. If the method has a return value, you can access it after awaiting the task.
```c#
async Task<int> AddAsync(int a, int b)
{
    await Task.Delay(1000); // Simulate a time-consuming operation
    return a + b;
}

async Task DoWork()
{
    int result = await AddAsync(2, 3);
    Console.WriteLine(result); // Prints 5 after waiting for 1 second
}
```
#### Exception Handling
- You can use try-catch blocks to handle exceptions thrown by asynchronous operations, just like with synchronous code.
```c#
async Task HandleExceptionAsync()
{
    try
    {
        await SomeAsyncOperationAsync();
    }
    catch (Exception ex)
    {
        Console.WriteLine($"An error occurred: {ex.Message}");
    }
}
```


try this : https://stackoverflow.com/a/40839752