[[launchSettings.json]] configurations are only used in development environment. So to set up environment configurations in Staging or Production environment we set up the Process Level Environment.
# How?
- First open powershell or windows terminal. Not command prompt.
- cd to the folder of program.cs
The command: `dotnet run`, will run in development mode using launchSettings.json, so dont run that command.

To test in staging or production environment, disable launchSettings.json by using:
```powershell
dotnet run --no-launch-profile
```
Then in order to set the environment configuration:
```powershell
$Env:Environment="EnvironmentName"
samples:
$Env:ASPNETCORE_ENVIRONMENT="Development"
$Env:ASPNETCORE_ENVIRONMENT="Production"
```
On non powershell you can use
```
set Environment="EnvironmentName"
```