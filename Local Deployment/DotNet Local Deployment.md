first build a server and copy the connection string. Make sure to add the allow code in the connection string.

setup the 0.0.0.0 links on launch settings.

the configure kestrel with the same.
```c#
builder.WebHost.ConfigureKestrel(options =>
{
    options.ListenAnyIP(7215, listenOptions =>
    {
        listenOptions.UseHttps(); // For HTTPS on 7215
    });
    options.ListenAnyIP(5191); // For HTTP on 5191
});
builder.WebHost.UseUrls("https://0.0.0.0:7215", "http://0.0.0.0:5191");
```