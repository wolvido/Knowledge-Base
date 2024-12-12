---
keywords: |-
  :
  colon
---
#cSharp 
syntax:
```c#
condition ? expression1 : expression2
```
- `condition` is a Boolean expression that evaluates to either `true` or `false`.
- If `condition` is `true`, the result of the expression is `expression1`.
- If `condition` is `false`, the result of the expression is `expression2`.
sample:
```c#
int x = 5;
int y = 10;

int result = (x > y) ? x : y;
```
if `x` is greater than `y`, the `result` will be assigned the value of `x`, which is `5`. If `x` is not greater than `y`, the `result` will be assigned the value of `y`, which is `10`.