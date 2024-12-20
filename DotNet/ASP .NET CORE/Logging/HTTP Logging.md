Log details of HTTP request and response.
![[Pasted image 20240223173407.png]]
#### Request ID
Every http request log will have a request ID generated by asp.net, it is also called the trace identifier.
# How-To:
###### To enable Http logging, we add it to the request pipeline.
In program.cs, after app has been built you add:
```c#
app.UseHttpLogging();
```
###### Then you have to set the level of logging in the [[Configurations]] aka appsettings:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Information" //here we set it to the lowest level of logging
	      //we're setting it in AspNetCore because Logging is built in to NetCore
    }
  }
}
```
This does not log response body or request body, you can enable it of course but that is insane, that would drain a lot of resources. It is only enabled in very unique circumstances. Only some things must be enabled in the configuration.
#### Http Logging Configuration
By Default only RequestProperties, RequestHeaders, ResponsePropertiesAndHeaders are logged.
To enable or disable other http logging features, you will enable **`AddHttpLogging()`** before the app is built in program.cs.
###### So for example, I want to enable only **`RequestProperties`** and **`ResponsePropertiesAndHeaders`**:
```c#
builder.Services.AddHttpLogging(options =>
{
    options.LoggingFields =
        Microsoft.AspNetCore.HttpLogging.HttpLoggingFields.RequestProperties |
        Microsoft.AspNetCore.HttpLogging.HttpLoggingFields.ResponsePropertiesAndHeaders;
        // add more features as necessary just use `|` symbol in between.
});
```
##### Below is the list of all features
###### Requests Logging Features
| Request | Flag for logging the entire HTTP Request. Includes [RequestPropertiesAndHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestpropertiesandheaders) and [RequestBody](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestbody). Logging the request body has performance implications, as it requires buffering the entire request body up to [RequestBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.requestbodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-requestbodyloglimit). |
| ---- | ---- |
| RequestBody | Flag for logging the HTTP Request [Body](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.body?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-body). Logging the request body has performance implications, as it requires buffering the entire request body up to [RequestBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.requestbodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-requestbodyloglimit). |
| RequestHeaders | Flag for logging the HTTP Request [Headers](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.headers?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-headers). Request Headers are logged as soon as the middleware is invoked. Headers are redacted by default with the character '[Redacted]' unless specified in the [RequestHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.requestheaders?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-requestheaders).<br><br>For example: Connection: keep-alive My-Custom-Request-Header: [Redacted] |
| RequestMethod | Flag for logging the HTTP Request [Method](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.method?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-method).<br><br>For example: Method: GET |
| RequestPath | Flag for logging the HTTP Request Path, which includes both the [Path](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.path?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-path) and [PathBase](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.pathbase?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-pathbase).<br><br>For example: Path: /index PathBase: /app |
| RequestProperties | Flag for logging a collection of HTTP Request properties, including [RequestPath](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestpath), [RequestProtocol](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestprotocol), [RequestMethod](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestmethod), and [RequestScheme](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestscheme). |
| RequestPropertiesAndHeaders | Flag for logging HTTP Request properties and headers. Includes [RequestProperties](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestproperties) and [RequestHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-requestheaders) |
| RequestProtocol | Flag for logging the HTTP Request [Protocol](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.protocol?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-protocol).<br><br>For example: Protocol: HTTP/1.1 |
| RequestQuery | Flag for logging the HTTP Request [QueryString](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.querystring?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-querystring).<br><br>For example: Query: ?index=1<br><br>RequestQuery contents can contain private information which may have regulatory concerns under GDPR and other laws. RequestQuery should not be logged unless logs are secure and access controlled and the privacy impact assessed. |
| RequestScheme | Flag for logging the HTTP Request [Scheme](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest.scheme?view=aspnetcore-8.0#microsoft-aspnetcore-http-httprequest-scheme).<br><br>For example: Scheme: https |
| RequestTrailers | Flag for logging the HTTP Request [Trailers](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.features.ihttprequesttrailersfeature.trailers?view=aspnetcore-8.0#microsoft-aspnetcore-http-features-ihttprequesttrailersfeature-trailers). Request Trailers are currently not logged. |
###### Response Logging Features
| Response | Flag for logging the entire HTTP Response. Includes [ResponsePropertiesAndHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-responsepropertiesandheaders) and [ResponseBody](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-responsebody). Logging the response body has performance implications, as it requires buffering the entire response body up to [ResponseBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.responsebodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-responsebodyloglimit). |
| ---- | ---- |
| ResponseBody | Flag for logging the HTTP Response [Body](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse.body?view=aspnetcore-8.0#microsoft-aspnetcore-http-httpresponse-body). Logging the response body has performance implications, as it requires buffering the entire response body up to [ResponseBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.responsebodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-responsebodyloglimit). |
| ResponseHeaders | Flag for logging the HTTP Response [Headers](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse.headers?view=aspnetcore-8.0#microsoft-aspnetcore-http-httpresponse-headers). Response Headers are logged when the [Body](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse.body?view=aspnetcore-8.0#microsoft-aspnetcore-http-httpresponse-body) is written to or when [StartAsync(CancellationToken)](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsebodyfeature.startasync?view=aspnetcore-8.0#microsoft-aspnetcore-http-features-ihttpresponsebodyfeature-startasync(system-threading-cancellationtoken)) is called.<br><br>Headers are redacted by default with the character '[Redacted]' unless specified in the [ResponseHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.responseheaders?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-responseheaders).<br><br>For example: Content-Length: 16 My-Custom-Response-Header: [Redacted] |
| ResponsePropertiesAndHeaders | Flag for logging HTTP Response properties and headers. Includes [ResponseStatusCode](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-responsestatuscode) and [ResponseHeaders](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-responseheaders). |
| ResponseStatusCode | Flag for logging the HTTP Response [StatusCode](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse.statuscode?view=aspnetcore-8.0#microsoft-aspnetcore-http-httpresponse-statuscode).<br><br>For example: StatusCode: 200 |
| ResponseTrailers | Flag for logging the HTTP Response [Trailers](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsetrailersfeature.trailers?view=aspnetcore-8.0#microsoft-aspnetcore-http-features-ihttpresponsetrailersfeature-trailers). Response Trailers are currently not logged. |
###### For Response and Request Features
| All | Flag for logging both the HTTP Request and Response. Includes [Request](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-request), [Response](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-response), and [Duration](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingfields-duration). Logging the request and response body has performance implications, as it requires buffering the entire request and response body up to the [RequestBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.requestbodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-requestbodyloglimit) and [ResponseBodyLogLimit](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingoptions.responsebodyloglimit?view=aspnetcore-8.0#microsoft-aspnetcore-httplogging-httploggingoptions-responsebodyloglimit). |  |
| ---- | ---- | ---- |
| Duration | 4096 | Flag for logging how long it took to process the request and response in milliseconds. |
| None | 0 | No logging. |
|  |  |  |

see: [HttpLoggingFields Enum (Microsoft.AspNetCore.HttpLogging) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.httplogging.httploggingfields?view=aspnetcore-8.0)
for all the info