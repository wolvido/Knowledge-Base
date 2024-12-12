---
keywords: Hypertext Transfer Protocol Secure and how to implement it in .NET.
---
HTTPS is the secure version of [[HTTP]], the S stands for Secure. Essentially, HTTPS encrypts the data sent between the browser and the website, providing a secure connection and protecting against eavesdropping, tampering, and data theft.
# How does it work?
1. First, the client establishes a TCP connection to the server. Once unsecured TCP is established, they can then communicate.![[Pasted image 20240430052743.png]]
2. Then the client sends a pre-request message and the client sends it's server public key and certificate.![[Pasted image 20240430053141.png]]
   The client will verify the certificate.
3. Then the client sends a "client random" to the server, the server creates it own "server random", then based on the two values, the server will create a session-key. ![[Pasted image 20240430061038.png]]
   Once the client receives the server random, the client creates a session key from the client random and server random numbers. Essentially the client and the server will have generated the same session key once they both receive each others number random.
4. So from now onwards, all messages will be encrypted and decrypted by the session key that is only known by the client and server.![[Pasted image 20240430061710.png]]
# How-To Implement in .NET?
So in `Program.cs`, add:
```c#
if (!app.Environment.IsDevelopment())
{
	app.UseHsts(); //enables HTTP strict transport security
	//only enabled on non-dev environment since it will be inconvenient in testing
}
app.UseHttpsRedirection(); //insert here
```
Make sure `app.UseHsts();` comes first.

If you are manually implementing an HTTPS, then in your [[launchSettings.json]], create a new https profile for testing:
```json
"https": {
  "commandName": "Project",
  "dotnetRunMessages": true,
  "launchBrowser": true,
  "applicationUrl": "https://localhost:7102", //notice it's in https not http
  "environmentVariables": {
    "ASPNETCORE_ENVIRONMENT": "Development"
  }
},
```
You can also change the `iisSettings` URL into an https.

You can skip all this steps if you let visual studio set it up, just edit the HSTS value, since the default HSTS value is 30 days. You may want to change this for production scenarios, see: [Enforce HTTPS in ASP.NET Core | Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-8.0&tabs=visual-studio%2Clinux-ubuntu#http-strict-transport-security-protocol-hsts)
