#js 
**by Id**
``<div id="demo-id"></div> `` 
```js
var elem1 = document.getElementById("demo-id");  
```

 **by Class Name**
``<div class="demo-class"></div>``
```js
var elem2 = document.getElementsByClassName("demo-class");  
```

**by Name**
``<div name="demo-name"></div>``
```js
var elem3 = document.getElementsByName("demo-name");  
```

**by Tag Name**
``<p>Some text</p>``
```js
var elem4 = document.getElementsByTagName("p");  
```

 **by query selector**
``<div id="demo-id"></div>``
```js
var elem1 = document.querySelector("#demo-id"); 
```

**by query selector all**
``<div class="demo-class"></div>``
```js
var elem2 = document.querySelectorAll(".demo-class");  
```

**by query selector all**
``<div name="demo-name"></div>``
```js
var elem3 = document.querySelectorAll('[name="demo-name"]');   
```

**by query selector all**
``<p>Some text</p>``
```js
var elem4 = document.querySelectorAll("p");  
```