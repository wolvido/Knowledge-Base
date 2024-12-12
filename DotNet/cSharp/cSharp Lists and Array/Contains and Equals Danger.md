---
keywords:
---
Be very careful when using Contains or equals method on reference types, because equals compares the reference not the value that is pointed by the reference, and contains uses equals.
see: [#402 – Value Equality vs. Reference Equality | 2,000 Things You Should Know About C# (2000things.com)](https://csharp.2000things.com/2011/09/01/402-value-equality-vs-reference-equality/) for clarification.