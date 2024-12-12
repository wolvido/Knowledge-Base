Razor is the engine that allows c# server side scripting in html, like PHP. 
>[!example] Notes
> - a View contains HTML markup with Razor Markup(c# server side)
> - Razor is the view engine that defines syntax to write c# in the view, **@** is the syntax of Razor.
> - A view should not directly call any business model or any action methods. Its not its responsibility, It should only send requests to the controller. see [[Business Logic vs Presentation Logic]].
> - Reminder, A presentation logic view should not have lots of c# code, it should only concern itself with the logic of presentation a.k.a frontend.
#### Razor Inline Block:
syntax:
```html
//code block
@{
	//C# code here
	string sample = "sample text"
}

//to insert a variable in the html
<div>@sample</div> //just add @ and this will return "sample text"
```
sample:
```html
@{
	//C# code here
	string title = "Title"
	string paragraph = "paragraph"
}
<!DOCTYPE html>
<html>
	<head>
		<title>@title</title>
	</head>
	<p>@paragraph this paragraph sucks</p> //this is how you add text alongside a razor variable
</html>
```
>[!info] 
>see [[Razor Scripting]] for more usage samples

>[!question] 
>**What's the point of having C# code on the frontend? What's the point of a server side scripting in the first place?**
>So you can generate dynamic pages, pages that change based on data. 
>Like for example, in your pipboy frontend only app, instead of adding weapons one by one, you can simply pull weapons data and foreach all of them in a list.
>If you still dont understand see: [Course: Asp.Net Core 7 (.NET 7) - Strongly Typed views part 2](https://www.udemy.com/course/asp-net-core-true-ultimate-guide-real-project/learn/lecture/34514412#overview)
#### Razor Direct Importing From Model Object:
You get the model to the views by using [[Strongly Typed Views]]
