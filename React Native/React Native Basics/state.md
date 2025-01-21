why use state?
in function components there is no concept of `this`, so there is no assigning the object a `this.state`. 
So in order to know it's state we call the `useState` function directly in our component.

**What does calling `useState` do?** 
It declares a “state variable”. Our variable is called `count` but we could call it anything else, like `banana`. This is a way to “preserve” some values between the function calls — `useState` is a new way to use the exact same capabilities that `this.state` provides in a class. Normally, variables “disappear” when the function exits but state variables are preserved by React.

**What do we pass to `useState` as an argument?** The only argument to the `useState()` Hook is the initial state. Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need. In our example, we just want a number for how many times the user clicked, so pass `0` as initial state for our variable. (If we wanted to store two different values in state, we would call `useState()` twice.)

**What does `useState` return?**
`const [value, setValue] = useState(initialValue);`
it returns two value in a deconstructed array.
why is it written in a deconstructed array?
- well... would you rather do this?
``` js
  var valueStateVariable = useState(initialValue); // Returns a pair
  var value = fruitStateVariable[0]; // First item in a pair
  var setValue = fruitStateVariable[1]; // Second item in a pair
```