simply use: 
```tsx
<Link href="/details">View details</Link>
```
###### If you need to navigate in code:
- import `import { useRouter } from "expo-router";`
- then call:
```tsx
const router = useRouter();

router.push("/the-other-view");
```
