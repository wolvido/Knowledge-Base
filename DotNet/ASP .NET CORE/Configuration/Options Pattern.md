the key value pairs of `appsettings.json` can be read and manipulated OOP style by bounding it to a model. 
![[configAsModel.png]]
The advantage of this is you can use the many key-value pairs easier because it is an object. If you only need 1 or 2 key value pairs it is easier to use method style being used here: [[Configurations]]
# How?
create a model based on the key value pairs, for example:
```json
"WeatherApi": {
  "BaseUrl": "http://api.openweathermap.org/data/2.5/", 
  "AppId": "b6907d289e10d714a6e88b30761fae22"
}
//"WeatherApi" is the master key.
```
for this appsetting you can create the model:
```c#
public class WeatherApiOptions
{
    public string? BaseUrl { get; set; }
    public string? AppId { get; set; }
}
```
#### Naming Convention
There is no set popular naming convention for the model, it may differ. But Harsha adds suffix "Option".
#### Binding
You can Bind them using Get<> or Bind().
>[!Warning]
><mark style="background: #FF5582A6;">DO NOT USE BINDING IN A CONTROLLER.</mark>
>It is better to inject it as a service in a controller, see [[Configuration in Controller or Service]].
###### Skip the parts below if you are using this in a controller
But there may be special cases when you need to use binding, So the info is below. In most cases **inject it as a service** see here [[Configuration in Controller or Service]].
##### Using Get<>
```c#
WeatherApiOptions? weatherApiOptions = app.Configuration.GetSection("WeatherApiOptions").Get<WeatherApiOptions>();
//or in the controller
WeatherApiOptions? weatherApiOptions = _configuration.GetSection("WeatherApiOptions").Get<WeatherApiOptions>();

//you can then use it as you would an object
var baseUrl = weatherApiOptions.BaseUrl;
ViewBag.AppId = weatherApiOptions.AppId;
```
##### Using Bind()
```c#
WeatherApiOptions weatherApiOptions = new WeatherApiOptions();

builder.Configuration.Bind("WeatherApi", weatherApiOptions);
//or in controller the controller
_configuration.Bind("WeatherApi", weatherApiOptions);

//in use
var baseUrl = weatherApiOptions.BaseUrl;
ViewBag.AppId = weatherApiOptions.AppId;
```

In my opinion get is easier to use, because Get<> because you don't have to create a new object.