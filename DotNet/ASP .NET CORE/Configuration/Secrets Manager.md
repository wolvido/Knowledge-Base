Sensitive information like api keys, or passwords, cannot be stored as plain and be seen by others in github. Like what you did with the twitter api.
You need to use Secrets Manager.
# How?
#### First Open the terminal
not just any terminal, open the developer PowerShell in vs studio, by pressing the view tab, then click terminal. then cd to the project folder, currently the terminal path is in the solutions folder not the project folder. The project folder is usually the same name as the solutions folder.
#### Initialize
Enter command: **`dotnet user-secrets init`**. This will initialize the user-secrets. 
Once it is initialized, it will generete a UserSecretsId, this UserSecretsId wil be stored in you main .csproj file, this Id will be your projects key to be able to access the secrets manager stored in your device. 
#### Set key-value
In order to add secret key-value pairs:
**`dotnet user-secrets set "key" "value"`**
If the config is nested, the you can use: **`dotnet user-secrets set "parentKey:childKey" "value"`**
You can view all your secret keys using: `dotnet user-secrets list`
#### Reading the value of secrets
It can be read the same way as non secrets once the values are registered. You can read it method style, or service injection into a controller or service etc. See: [[Configurations]]. see [[Configuration in Controller or Service]]
#### What about production servers?
Secrets manager is only stored in your device, which is in a development environment. 
*So how do you store sensitive information in production servers?*
You set it in the environment variables(aka launchsettings.json) manually in the production server terminal, this is called the [[Process Level Environment]].
###### How?
- open the terminal powershell or developer powershell in vs studio.
- Navigate to the project folder (not the solutions folder).
- Set the key-value pairs by using command: **`$Env:key "value"`** (case sensitive).
- If the config is nested you use double underscore: **`$Env:parentKey__childKey "value"`**
- Then run the server. If youre going to test run it, **you should** disable the launchsettings.json, see:[[Process Level Environment]] on how to do disable.



