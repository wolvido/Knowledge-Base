---
keywords: |-
  where to put static files
  where to put files in a mvc
  where to put frontend files of mvc
  where to put css files in mvc
---
The whole idea is to serve the static files based on the incoming url.

All static files eg. images, javascript, css, must be put into web root folder named "wwwroot" this is for security purposes. Any static files outside wwwroot folder cannot be accessed by the client. 

In order for wwwroot files, files to be accessed, you need to run `app.UseStaticFiles();` into `program.cs`.
To serve static files in a middleware, use `UseStaticFiles()` middleware.
**Note** that if you test this on a browser with cache enabled, it will still work even if files have been removed or changes is applied.

By default, ASP.NET Core looks for static files in the `wwwroot` folder in your project. 
You can also add a custom root directory and other options when calling `app.UseStaticFiles()` if needed. sample:
```c#
app.UseStaticFiles(new StaticFileOptions
{
    FileProvider = new PhysicalFileProvider(Path.Combine(builder.Environment.ContentRootPath,"MyRoot"))
});
```
If your just going to use wwwroot folder,  just adding `app.UseStaticFiles();` is already configured for that.
If you want multiple root folders, just add another custom `app.UseStaticFiles(...)` like the code sample above.
**Note**: If you decide to create a custom root folder, you still need to have an empty wwwroot folder, because for some reason it will throw an error.

UseStaticFiles() middleware is used for serving static resources like stylesheets, scripts, and images in web applications. It eliminates the need to create custom controllers or routes for handling these resources, making it more efficient and straightforward.





