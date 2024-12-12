Result Filter the will always run regardless of short circuit or anything.
Useful for when you have code the needs to run compulsory regardless of whatever happens, like for example you need to clean the cache in the server memory, or remove a cookie, or reset a counter etc..
![[Pasted image 20240308172033.png]]
# How-To:
The file will be located in the "ResultFilters" folder, assuming you know the folder structure of filters.
The syntax is the same as [[Result Filter]] but instead you will inherit from **`IAlwaysRunResultFilter`**.
Sample:
```c#
public class SampleAlwaysRunResultFilter : IAlwaysRunResultFilter
{
	public void OnResultExecuting(ResultExecutingContext context)
	{
		//code that will execute before the response is sent
	}
	public void OnResultExecuted(ResultExecutingContext context)
	{
		//code that will execute after the response is sent
	}
}
```
Can also be async version: [[Asynchronous Filter]].
###### Everything you do in result filter you can do in IAlwaysRunResultFilter, but in most cases, it is very rare to use this.