---
keywords: Aync that returns void
---
If you have a void method you want to convert asynchronous, in general usually you can just replace `void` with `Task`:
```c#
static async Task g()
{
    await h();
}
```
It will essentially be equal to returning a void, but you can also use void on special cases, read below.

A method marked as `async` can return `void`, `Task` or `Task<T>`.

A `Task<T>` returning async method can be awaited, and when the task completes it will proffer up a T.

A `Task` returning async method can be awaited, and when the task completes, the continuation of the task is scheduled to run. 
sample:
```c#
static async Task g()
{
    await h();
}
```

A `void` returning async method cannot be awaited; it is a "fire and forget" method. It does work asynchronously, and you have no way of telling when it is done. This is more than a little bit weird, normally you would only do that when making an asynchronous event handler. The event fires, the handler executes; no one is going to "await" the task returned by the event handler because event handlers do not return tasks, and even if they did, what code would use the Task for something? It's usually not user code that transfers control to the handler in the first place.
[c# - What's the difference between returning void and returning a Task? - Stack Overflow](https://stackoverflow.com/questions/8043296/whats-the-difference-between-returning-void-and-returning-a-task)
sample:
```c#
static async void f()
{
    await h();
}
```

also see: [c# - async/await - when to return a Task vs void? - Stack Overflow](https://stackoverflow.com/questions/12144077/async-await-when-to-return-a-task-vs-void)