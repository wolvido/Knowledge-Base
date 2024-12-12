You can set different configuration for every lifecycle [[Environment]]. 
This is useful if you have specific configurations that should only exist in a specific environment, like for example you want to use a different server for development and for production.

Under appsettings.json you will find the environment specific appsettings.
![[Capture 36.png]]
The environment specific configuration file overrides the appsettings.json if similar key-value exists, if not it will use key-values from appsettings, if there are no override. 

The program will use the Environment Specific Configuration based on what environment is set on [[launchSettings.json]].
Of course you can also create appsettings.Staging.json or appsettings.Production.json, or appsettings.Custom.json.




