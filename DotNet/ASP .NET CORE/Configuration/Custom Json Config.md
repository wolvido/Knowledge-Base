On large projects, sooner or later your appsettings.json will bloat from too many config key-value, as per good coding practice; some thematically configs need to be separated into a separate custom config file.
For example, you have this appsettings:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  
 // you want to separate the WeatherApi to its appropriate custom json
  "WeatherApi": {
    "BaseUrl": "http://api.openweathermap.org/data/2.5/", 
    "AppId": "b6907d289e10d714a6e88b30761fae22"
  }
}
```
You want to create a separate custom json for weather api.
#### First create a the json file
- right click on the project name, not the solution, then add a new json file
- Name it appropriately as per the separated config, there is no convention.
- then cut and paste the `"WeatherApi"` section:
```json
{
  "WeatherApi": {
    "BaseUrl": "http://api.openweathermap.org/data/2.5/", 
    "AppId": "b6907d289e10d714a6e88b30761fae22"
  }
}
```
#### Then register as a config source
- in program.cs:
```c#
builder.Configuration.AddJsonFile("CustomConfig.json", optional: true, reloadOnChange: true);
//optional means that if the file is not found, the application will still run
//reloadOnChange means that if the file is changed, the application will restart
//optional and reloadOnChange is optional of course, depending on the requirements
```
that's it, you don't need to change anything in the controller or anywhere else, the configs will work the same as if "WeatherApi" is in appsettings.json.

---
>[!tip]
>maybe, just maybe, very rare it happens, the sample above wont work, try this:
```c#
//this is the "old" way
builder.Host.ConfigureAppConfiguration((hostingContext, config) =>
{
    config.AddJsonFile("CustomConfig.json", optional: true, reloadOnChange:true);
});
```


