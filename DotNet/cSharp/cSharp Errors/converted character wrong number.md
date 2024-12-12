#cSharp 
keywords:
	# char converted to integer wrong number
[https://stackoverflow.com/questions/50294231/incorrect-values-when-converting-char-digits-to-int](https://stackoverflow.com/questions/50294231/incorrect-values-when-converting-char-digits-to-int)

minus it with char '0', because char '0' is the first of the number values in ACII index. In ASCII index there 47 entries before the numbers. 48th is '0', by subtracting with '0' the char integer values start at 0 Equal to their representation.

like this:
```c#
char wrong = '2';  
int correct = wrong - '0';
```