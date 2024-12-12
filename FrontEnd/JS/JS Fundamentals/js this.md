#js 
Essentially, it refers to the object of the current execution. 

#### Examples:
- in an **event handler**, this refers to the element:
```js
button.addEventListener('click', function() {
  // Inside this event handler, 'this' refers to the button element that was clicked
  console.log(this); // returns the element
  this.style.backgroundColor = 'blue'; // Changes the button's background color
});
```

- Inside a method of an object, `this` refers to the object that contains the method.
```js
var person = {
  name: 'John',
  sayName: function() {
    console.log(this.name);
  }
};
person.sayName(); // Outputs 'John'
```

Note: Arrow functions does not have their own `this` see [[js arrow]] for more details.