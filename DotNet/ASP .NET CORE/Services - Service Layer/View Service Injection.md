---
keyword: Inject service into view
---
Just like how you can inject the services into the controller or other service, You can inject the service into a view as well.
>[!question]
>###### What's the Point of this? Why not just inject it to the controller?
>In case you need a Service that is not provided by the controller, so the views have an option of injecting whatever service it wants. 
>Most of the time the controller handles it but there are special services that might be specific only to the view. Like for example; configuration for the view.
# How to do it?
#### Import the Service Contract
First import the class library of your service Interface into your `_ViewImports.cshtml`:
```cshtml
@using ServiceContracts
```
Do not import the class library of the service. It should be the class library of the service interface.
see: [[Services - Service layer]] for more info.
#### Inject to the View
This is the view where you want to inject the service.
```html
@inject ISampleService sampleSeviceInView

<h1>Home</h1>
<p>sampleSeviceInView.GetMessage();</p>
```
Just like how you inject a service in a controller constructor.