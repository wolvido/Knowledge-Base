#js 
They are custom html markups. This note might be incomplete.

**Custom Element Definition**:
You start by defining a custom element using the `customElements.define` method. You give your custom element a name and associate it with a class that defines its behavior and appearance. Here's an example:
```js
// Define a custom element named "my-element"
customElements.define('my-element', MyElementClass);
```

**HTML Markup**:
Once the custom element is defined, you can use it in your HTML markup just like any other HTML element. For example:
```html
<my-element></my-element>
```

**Custom Element Class**:
In your JavaScript code, you define the class that represents your custom element. This class typically extends the `HTMLElement` class and defines the element's behavior and appearance. Here's a basic example:
```js
class MyElementClass extends HTMLElement {
  constructor() {
    super(); // Call the super constructor

    // Attach a Shadow DOM to encapsulate the element's internal structure
    const shadow = this.attachShadow({ mode: 'open' });

    // Create an element and style it
    const paragraph = document.createElement('p');
    paragraph.textContent = 'Hello, Web Component!';
    shadow.appendChild(paragraph);

    // You can also define event listeners and other functionality here
  }
}
```

**Styling with Shadow DOM**:
You can encapsulate the styling of your custom element using Shadow DOM. The styles defined within the Shadow DOM are scoped to the element and won't affect the rest of the page. For example:
```js
const shadow = this.attachShadow({ mode: 'open' });

// Create a style element and attach it to the shadow DOM
const style = document.createElement('style');
style.textContent = `
  p {
    color: blue;
  }
`;
shadow.appendChild(style);
```

**Attributes and Properties**:
You can define attributes and properties for your custom element to allow interaction with it. For example, you can define a property like this:
```js
class MyElementClass extends HTMLElement {
  // ...
  set message(value) {
    this.setAttribute('message', value);
  }

  get message() {
    return this.getAttribute('message');
  }
  // ...
}
```
You can then interact with your element's properties in HTML and JavaScript.
```html
<my-element message="Hello, Web Component"></my-element>
<script>
  const element = document.querySelector('my-element');
  console.log(element.message); // "Hello, Web Component"
</script>
```
Web components allow you to create encapsulated, reusable UI components that can be used across your web application. They are particularly useful for building complex user interfaces and ensuring code modularity and maintainability.