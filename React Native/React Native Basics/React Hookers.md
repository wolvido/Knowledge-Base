Prerequisite understanding:
[[state]]

Sample Hooker:
```ts
// hooks/useInput.js
import { SetStateAction, useState } from 'react';

export function useInput(initialValue = '') {

    const [value, setValue] = useState(initialValue); //refer to state note for info
    
    const handleChange = (text: string) => {
        setValue(text);
    };

    const handleSubmit = () => {
        console.log("Input value:", value);
    };
   
    return {
        value,
        handleChange,
        handleSubmit
    };
}
```

Sample jsx:
```jsx
import { useInput } from '../../../hooks/index-hook'; // Import the custom hook

//react component
export default function HomeScreen() {
    const { value: inputValue, handleChange, handleSubmit } = useInput(""); //custom hook
    return (
        <View style={styles.container}>
            <TextInput
                style={styles.input}
                placeholder="Enter something..."
                value={inputValue}
                onChangeText={handleChange}
            />
            <Button title="Submit" onPress={handleSubmit} />
        </View>
    );
}
```

So how does it work?
So the component essentially "borrows" the hook function with this code: 
```jsx
const { value: inputValue, handleChange, handleSubmit } = useInput("");
```
so when we say it "borrows", it essentially allows the component to access the parts that the hook function exposes.
So the component is able to access the variables and sort of methods of the hook, like the `inputValue`, `handleChange`, `handleSubmit`.
```jsx
        <View style={styles.container}>
            <TextInput
                style={styles.input}
                placeholder="Enter something..."
                value={inputValue} //access here
                onChangeText={handleChange} //here
            />
            <Button title="Submit" onPress={handleSubmit} /> //and here
        </View>
```

so  `inputValue`, `handleChange`, `handleSubmit` are written in the hook like so:
```ts
export function useInput(initialValue = '') {
    const [value, setValue] = useState(initialValue);
    const handleChange = (text: string) => {
        setValue(text);
    };
    
    const handleSubmit = () => {
        console.log("Input value:", value);
    };

    return {
        value,
        handleChange,
        handleSubmit
    };
}
```
Essentially its just a way to give function to the view, like a sort of view model in a mvvm style.
