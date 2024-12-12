Different cultures have different writing system, the calendar used, the sort order of strings, and formatting for dates and numbers.
Mostly you will use this to set the string format of dates and numbers.

**This is especially important on dates** because by default the server uses the date format of the local culture, and if you develop on a different region to your deployment, youre gonna end up with lots of bugs on your production code. 
In order to set global culture in `program.cs` you can use:
```c#
//build
var app = builder.Build();
 
// Ensure the app uses PH culture
var supportedCultures = new[] { "en-PH" };
var localizationOptions = new RequestLocalizationOptions()
    .SetDefaultCulture(supportedCultures[0])
    .AddSupportedCultures(supportedCultures)
    .AddSupportedUICultures(supportedCultures);
app.UseRequestLocalization(localizationOptions);
```

There are also many ways culture is used in .NET you will encounter them, just keep in mind that various .NET methods and classes might use the local culture and ruin your code.