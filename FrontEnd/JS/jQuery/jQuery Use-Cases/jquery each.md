#jQuery 
Iterate over a list or collection and apply a callback. example:
```js
var colors = ['red', 'green', 'blue'];

$.each(colors, function(index, color) {
  console.log(index + ': ' + color);
});
```
syntax:
```js
$.each(collection, function(index, value) {
  // Function body
});
```
- `collection`: The collection (array, object, etc.) over which you want to iterate.
- `index`: The index or key of the current element in the collection.
- `value`: The value of the current element in the collection.

another example:
```js
var person = {
  name: 'John',
  age: 30,
  occupation: 'Developer'
};

$.each(person, function(key, value) {
  console.log(key + ': ' + value);
});
```