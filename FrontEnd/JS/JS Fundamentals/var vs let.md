**Scope:**
- **`let`:** Creates variables with **block scope**. This means the variable is only accessible within the code block where it's declared (like an `if` statement or a loop). This helps prevent accidental modification from outside that block.
- **`var`:** Creates variables with **function scope**. The variable is accessible throughout the entire function it's declared in, regardless of code blocks. This can lead to unintended consequences if you're not careful.

**Hoisting:**
- **`let`:** Variables declared with `let` are not hoisted. You can't access them before they are declared in the code. This helps avoid errors.
- **`var`:** Variables declared with `var` are hoisted to the top of their function scope. This means you can potentially access them before they are declared, which can lead to unexpected behavior.

**Best Practices:**
In modern JavaScript, it's generally recommended to use `let` for variable declaration. This promotes cleaner, more predictable code due to its block scope and lack of hoisting. var is somewhat crazy.

You might encounter `var` in older code, but for new projects, stick with `let` (and `const` for constants) for better maintainability and fewer bugs.

###### Questions:
- what if a let is declared outside an if else and the if else is modifying the let, will the let be accessible?
	- Yes, as long as the let and the if else is inside the same block.