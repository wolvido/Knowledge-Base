on your `_layout.tsx`:
simply add:
```tsx
import { Tabs } from 'expo-router';  
  
export default function TabLayout() {  
    return (  
        <Tabs>  
            <Tabs.Screen name="(home)" options={{ title: "Home" }}/>  
            <Tabs.Screen name="settings" />  
        </Tabs>    
        );  
}
```
>[!note]
> `<Tabs.Screen name="(home)" />` the name property is what determines its control, so <`Tabs.Screen name="(home)" />` controls the (home) folder. In the view you can change it's name to "Home" via `options={{ title: "Home" }}`.

it will create two tabs, (home) and settings that will automatically navigate, assuming the file structure is correct:
![[afwwf.png]]