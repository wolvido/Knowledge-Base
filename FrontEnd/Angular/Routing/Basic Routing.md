on the main app-root html add the navigation
``` html
<h1>Angular Router App</h1>
<nav>
  <ul>
    <li><a routerLink="/first-component" routerLinkActive="active" ariaCurrentWhenActive="page">First Component</a></li>
    <li><a routerLink="/second-component" routerLinkActive="active" ariaCurrentWhenActive="page">Second Component</a></li>
  </ul>
</nav>
<!-- The routed views render in the <router-outlet>-->
<router-outlet></router-outlet> //this is crucial this is where the navigated is rendered
```

on `app.routes.ts` register the routes:
``` typescript
export const routes: Routes = [
    {path: 'first-component', component: first-component},
    {path: 'second-component', component: second-component}
];
```

You also need to add the `RouterLink`, `RouterLinkActive`, and `RouterOutlet` to the `imports` array of `AppComponent`.
```typescript
@Component({
  selector: 'app-root',
  imports: [CommonModule, RouterOutlet, RouterLink, RouterLinkActive],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'routing-app';
}
```
whenever you have a component that renders a `<router-outlet></router-outlet>` you will need to import these above. Change app-root to the component that needs 