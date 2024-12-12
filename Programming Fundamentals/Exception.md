---
keywords: What is an Exception
---
Exception is an abnormal unexpected phenomenon. 
For example if the user was able to login even if the password is incorrect.

If a user failed a login due to an incorrect password, then that is not an exception, that is working as intended.
If an Exception does occur, the user is not suppose to be informed of everything about it, it needs to be handled by try catch gracefully. 

#### Like Harsha says; **Don't confuse**
**The question is, what are exceptions for? Does every piece of code need an exception?**
No, you use exceptions on pieces of code that you know will definitely cause an error in the future or has a good chance of throwing an error due to circumstances you cannot control like:
- **User actions** (e.g., entering incorrect data, or hacker injections)
- **External factors** (e.g., network connectivity issues, unavailable files, exceeded API use)
- **System conditions** (e.g., disk space running out, permissions changes)
**Exceptions are not meant to alert the dev of a bug. If you find a bug, you fix it.**
