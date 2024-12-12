
```typescript
  @defer (on trigger){
	<comments />
  }@placeholder{
	<p> placeholder zone</p>  
  }@loading{
	  <p>loading...</p>
  }
```
By default `@defer` will load the `comments` component when the browser is idle.
The `@placeholder` block is where you put html that will show before the deferred loading starts.
The `@loading` block is where you put html that will show _while_ the deferred content is actively being fetched, but hasn't finished yet.
