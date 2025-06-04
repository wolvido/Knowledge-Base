useEffect is primarily used for side effects.
syntax:
```tsx
useEffect(() => {
  // This code runs after the component renders or after specific dependencies change.
}, [dependencies]);
```
so essentially it just runs code if it detects changes in dependencies, or without dependencies it runs code after the component renders.