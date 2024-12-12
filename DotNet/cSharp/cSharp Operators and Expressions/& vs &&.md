#cSharp 
& is a bitwise AND, meaning that it works at the bit level. && is a logical AND, meaning that it works at the boolean (true/false) level. 

Logical AND uses short-circuiting (if the first part is false, there's no use checking the second part) to prevent running excess code, whereas bitwise AND needs to operate on every bit to determine the result.

[https://stackoverflow.com/questions/5537607/usage-of-versus](https://stackoverflow.com/questions/5537607/usage-of-versus)