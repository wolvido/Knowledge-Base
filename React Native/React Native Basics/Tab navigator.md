on your `_layout.tsx`:
simply add:
```tsx
import { Tabs } from 'expo-router';  
  
export default function TabLayout() {  
    return (  
        <Tabs>  
            <Tabs.Screen name="(home)" />  
            <Tabs.Screen name="settings" />  
        </Tabs>    );  
}
```
it will create two tabs, (home) and settings that will automatically navigate, assuming the file structure is correct:
![[afwwf.png]]