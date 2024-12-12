#js 

run a function for each array.

syntax:
```js
array.forEach(function(currentValue, index, arr){
//code
}, thisValue)
```
- `array`: The array you want to iterate over.
- `currentValue`: The current element in the index.
- `index`:  The index of the current element.
- `arr`:  The array being traversed.
- `thisValue`: Replace the 'this' context with `thisValue`.
All function parameters are optional and you can run forEach with `//code` only.
###### question:
what is the purpose of `arr` parameter when I can just directly refer the `array` and they are the same? 
So we can access the array when we are making a named callback function, example:
```js
const data = [10, 20, 30, 40, 50];
data.forEach(customCallback);

function customCallback(currentValue, index, arr) {
  // Here, we use the 'arr' parameter so the named callback function knows the array
  console.log(`Value: ${currentValue}, Index: ${index}`);
  console.log('Array:', arr);
}
```
