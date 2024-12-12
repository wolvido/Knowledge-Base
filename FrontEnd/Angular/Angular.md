#### The most popular Angular architecture is the Modular Monolithic Architecture
Essentially it works by creating self-contained features with its own behavior, design, and children.
see: [[Component]].
###### Typical Folder Structure:
```
src/
 ├── app/
 │    ├── core/
 │    │    ├── interceptors/
 │    │    ├── guards/
 │    │    ├── services/
 │    │    ├── utils/
 │    │    ├── layout/ //headers, footers, etc..
 │    │
 │    ├── shared/
 │    │    ├── components/
 │    │    ├── directives/
 │    │    ├── pipes/
 │    │    ├── models/
 │    │
 │    ├── features/
 │    │    ├── feature1/
 │    │    │    ├── components/
 │    │    │    ├── services/
 |	  |	   |	├── feature-child/
 │    │    │
 │    │    ├── feature2/
 │    │         ├── components/
 │    │         ├── services/
 │    │
 │    ├── app.component.ts
 │    ├── app.component.html
 │    └── app.component.css
```
for simple apps:
![[simple sample.png]]

check this out: [angular-realworld-example-app/src/app/features/profile at main · gothinkster/angular-realworld-example-app](https://github.com/gothinkster/angular-realworld-example-app/tree/main/src/app/features/profile)