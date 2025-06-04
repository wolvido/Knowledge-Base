The routing is based on the file location.
For example:
![[Capture 58.png]]To allow navigation between two routes (`/` and `/details`), update the Root layout file and add a `Stack` component to it:
```tsx layout.tsx
import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack
      screenOptions={{
        headerStyle: {
          backgroundColor: '#f4511e',
        },
        headerTintColor: '#fff',
        headerTitleStyle: {
          fontWeight: 'bold',
        },
      }}>
      <Stack.Screen name="index" options={{ title: "Index Page" }} />
      <Stack.Screen name="details" options={{ title: "Details Page" }} /> //insert here
    </Stack>
  );
}
```
I've tested and  `<Stack.Screen name="nameOfFile" />` is not necessary for navigation, you only need it if you need to customize the stack screen with options. The stack screen is at the top.

#### Navigation Links:
simple: `<Link href="/details">View details</Link>` just make sure the `href` is pointing to a correct file.