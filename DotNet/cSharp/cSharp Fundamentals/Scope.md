---
keywords: how encapsulation of scope works in c#
---
#cSharp 
Scope in c# works in cascade.
![[scope 1.png]]
anything declared at the outside of a scope can be accessed/modified by the inside scope and all the smaller scopes, because all the smaller scopes is still a member of the large scope just like the declared variable, the declared variable is considered global-like by the smaller scopes.

Anything declared inside a smaller scope cannot be accessed/modified by anything outside since that member is not member of the outside scope, it is confined to its scope.

anything that encompasses a curly bracket `{}` is a scope, like classes, methods, if else, or just curly brackets/block scopes.
