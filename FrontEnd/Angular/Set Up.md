#### How to setup angular in visual studio alongside the server code
##### Single Visual Studio Way (not recommended)
1. First create a project using the web API template.
2. create a server app folder, usually named "ServerApp".
3. Then if using [[Clean Architecture]] arrange it in clean arch style. Create src and tests folder inside ServerApp, and move the web api project in src.
4. Were not going to use the visual studio angular template because that shit is broken, so were going to create using npm. 
	- right click on solution and open terminal 
	- then simply follow instructions here [Installation • Angular](https://angular.dev/installation) not to mention, make sure you have node installed.
5. Then on your solution right click and add existing website. Navigate to your solution repo and click on the angular app folder you made. 
Really it doesn't matter where the angular app is located as long as the API can communicate, the guide above is for when you want to combine both in a single folder and VS solution.

#### Recommended Way
The above way is a shitty hassle and is extremely slow when run in visual studio.
The reddit recommendation is to just use VS code on angular and the Web API on VS. They can still be in the same folder and same git, just not the same IDE.
Also remove the "ServerApp" folder and just do it the clean arch way.




  