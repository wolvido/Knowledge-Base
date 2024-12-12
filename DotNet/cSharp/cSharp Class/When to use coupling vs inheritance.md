#cSharp 
###### - Does TypeB want to expose the complete interface (all public methods no less) of TypeA such that TypeB can be used where TypeA is expected? Indicates **Inheritance**.
- e.g. A Cessna biplane will expose the complete interface of an airplane, if not more. So that makes it fit to derive from Airplane.

###### - Does TypeB want only some/part of the behavior exposed by TypeA? Indicates need for **Composition.**
- e.g. A Bird may need only the fly behavior of an Airplane. In this case, it makes sense to extract it out as an interface / class / both and make it a member of both classes.

source: https://stackoverflow.com/a/53354/13107848.

also see: [[Liskov Substitution Principle (LSP)]]