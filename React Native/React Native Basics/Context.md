Usually, you will pass information from a parent component to a child component via props. But passing props can become verbose and inconvenient if you have to pass them through many components in the middle, or if many components in your app need the same information.
_Context_ lets the parent component make some information available to any component in the tree below it—no matter how deep—without passing it explicitly through props.
#### How it outputs data?
so essentially it outputs props on a jsx element. by returning:
```jsx
  return (
    <SampleContextProvider>
      {children}
    </SampleContextProvider>
  );
```
That JSX return is then wrapped to a layout or the root app so that every children of the root has access to the values, making it shareable to everyone.
#### How to register Context on `_Layout`
you import it directly without `{}`, like so:
```tsx
//do this
import CartContextProvider from '@/context/cart-context';
//not this
import { CartContextProvider } from '@/context/cart-context';
```
#### How to use Context on the component?
simply assign it a variable and call its methods or get its data:
```tsx
import { SampleContext } from '../whatever';
import { useContext } from 'react';

export default function SampleComponentScreen() {
    //assign context
    const SampleContext = useContext(SampleContext);
    
    //get data from context using a context function
    const dataList = cartContext.getData();
	    //this is how you CRUD it essentially, just build functions.
   
    return (
        <View style={styles.main}>
			//here were using the `submitData` function on a button for when you want to sumit data.
            <Button title="Submit Cart" onPress={cartContext.submitData} />
        </View>
    );

}
```
#### A context almost always needs to use `useState`
- I'm not sure why yet, but this is the "react way".
- Not using it causes bugs, I didn't use `useState` on inventory, that's why it caused the weird delay bug.

--- 
another explanation, understanding 2.0:
- so basically context is a component without visual elements.
- its goal is to carry prop and analyze prop. its on top always so that it carries data like a god.
- 