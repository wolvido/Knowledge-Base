~~grabbing data from a react state after that state has been set, might still end up with grabbing a stale state.~~

~~it might be better to grab data from a previous state inside a setState.~~ 

~~just like in cart context of react orders project.~~


~~or maybe its a closure problem~~
- ~~the function only gets updated if it is run.~~
- ~~doesnt matter how much the state changes in real time, the function only knows its data if its ran.~~
- ~~according to AI, this is because of javascript closures, where the function only knows data of the time it was created. then only updates it when ran. it doesnt get updated when the data changes.~~

==javascript closure shit.==

wait, maybe its because of using useCallback on components, thats why its using old stale data.

==GOD FUCKING DAMMIT==
it was use callback. FUCK.
UseCallback saves a state of everything, even the data inside it, and when its ran, is uses the old data and only updates its data store after.

FUCK UseCallback FUCK AI.

also be carefull with `memo`, if you get delayed data check if you are using memo.