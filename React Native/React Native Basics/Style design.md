---
keywords: react native styles design
---
```jsx
//react component  
export default function HomeScreen() {  
    return (  
        <View style={styles.container}>  
            <Text>Home</Text>  
            <Text>hello universe 3</Text>  
            <Link href={"/(home)/details"}>View details</Link>  
        </View>    );  
}  

const styles = StyleSheet.create({  
    container: {  
        flex: 1,  
        justifyContent: 'center',  
        alignItems: 'center',  
    },  
});
```
**How does it work?**
Instead of class attributes on the element, we make use of `style={styles.container}` which `container` is the css class.