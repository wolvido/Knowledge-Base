asp.net core has a system called configuration settings to store the constant key value pairs that can be read from anywhere from any file within the same application, it is stored in the appsettings.json.
It is used to store various parameters such as API keys, connection strings, and other application-specific settings.
- For example you should never hardcode API keys, you can store it in configurations.
- You can configure logging settings, such as log levels, log output locations, and log formats, using the configuration system. This allows you to adjust logging behavior without modifying the application code.
- Configuration settings are often used to enable or disable certain features in an application. This is commonly known as feature toggling or feature flags, and it allows you to control the availability of features without changing the code.
>[!warning]
>The samples below use method style of manipulating the key-value pairs of appsettings.json, it is ok if you are manipulating one or two key-value pairs, but if there are many, it is suggested to bind them to a model using [[Options Pattern]] and if you use them in a controller, it must be injected as a service see: [[Configuration in Controller or Service]].
#### appsettings.json
sample:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  
  //sample Api key-value pairs
  "WeatherApi": {
    "BaseUrl": "http://api.openweathermap.org/data/2.5/", 
    "AppId": "b6907d289e10d714a6e88b30761fae22"
  }
}
```
The key-value pairs are stored in **appsettings.json**.
To access the values in **`program.cs`** you can call **`IConfiguration`** using **`app.Configuration`** just like how you call **`app.Environment`** from **`IWebHostEnvironment`**. see [[Environment]] to see sample and apply it here.
Based on the appsettings above:
```c#
//getting value
var test = app.GetValue["WeatherApi:BaseUrl"];
//test is equal to "http://api.openweathermap.org/data/2.5/"

//getting value from key, and having a default value if value does not exist on original key
var key = app.Configuration.GetValue<string>("key", "default value");

//setting the value
app.Configuration["WeatherApi:AppId"] = "1234";
//AppId in appsettings.json will become "AppId": "1234"
```
#### How to Read Hierarchal Key
Hierarchal keys are master keys with key-value pairs as value, for example:
```json
//normal key-value
"Key": "Value"

//Hierarchal keys
"MasterKey": {
	"Key1": "Value1", 
	"Key2": "Value2"
}
```
To read "Value1":
```c#
var keyValue = app.Configuration["MasterKey:Key1"];
//or
var keyValue = app.Configuration.GetValue<string>("MasterKey:Key1");
```
You can also use **`GetSection()`** of IConfiguration to read Hierarchal keys:
```c#
var keyValue = app.Configuration.GetSection("MasterKey")["Key1"];
```

**`GetSection()`** returns a type of **`IConfigurationSection`**, so you can store it in a type **`IConfigurationSection`** and use it DRYly like this:
```c#
IConfigurationSection masterKeySection = app.Configuration.GetSection("MasterKey");
var keyValue = masterKeySection["Key1"]; 
var keyValue2 = masterKeySection["Key2"]; //DRY usage
```
>[!warning]
>The samples above use method style of manipulating the key-value pairs of appsettings.json, it is ok if you are manipulating one or two key-value pairs, but if there are many, it is suggested to bind them to a model using [[Options Pattern]] and if you use them in a controller, it must be injected as a service see:[[Configuration in Controller or Service]].
# What next?
- Reading and manipulating key value pairs using `IConfiguration` methods is somewhat not OOP, and tedious If there is too many keys. The key-value pairs of `appsettings.json` can be bound to a model, so we can manipulate the appsettings key's like you would an object. see: [[Options Pattern]]. 
- If you need configuration access in the controller or in a service see: [[Configuration in Controller or Service]].
- What if you need different configurations for different lifecycle [[Environment]]s? like if you want to use a different server for development and production. see: [[Environment Specific Config]].
- Sensitive information like api keys, or passwords, cannot be stored as plain and be seen by others in github. use: [[Secrets Manager]].
- on large projects, sooner or later your appsettings.json will bloat from too many config key-value, as per good coding practice; some thematically configs need to be separated into a separate custom config file. see: [[Custom Json Config]].