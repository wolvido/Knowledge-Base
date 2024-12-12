---
keywords: "TypeError: Cannot read properties of null (reading 'classList')    at HTMLDocument.onDocumentLoad (VM5:647:19)"
---
More likely this happens because you are using js `fetch()` to pull a partial view form, what happens here is that fetch will change all `asp-controller and asp-action` routes to whatever route you used in fetch, which more likely is the GET route with the same name as the POST method, that's why it sends post but returns the GET route.
#### Solutions?
- you could change the name of the method your fetching.
- put the form outside the partial initializer in main, so that its not affected.