# How to reload/refresh the data when navigate to same route in Angular 9

I have an issue with the route
**Routing File**

```

const routes = [
  {
    path: '',  // base route is `setting`
    component: SettingViewComponent,
    children: [
      {
        path: 'services',
        component: ServiceListComponent
      },
      {
        path: 'general',
        component: GeneralSettingsComponent
      },
    ]
 }
];
```

When I am on /setting/services and hits the /setting route the `SettingViewComponent` code doesn’t get initiate again.\
I have a redirection logic in `SettingViewComponent` which needs to be re-initiate.

You can use the `Router` and override the `shouldReuseRoute` from the `routeReuseStrategy`\
method which returns false statement.

```

import { Router } from '@angular/router';
...
export class SettingViewComponent implements OnInit {

 constructor(
   private router: Router
 ) { }

 public ngOnInit(): void {
    this.router.routeReuseStrategy.shouldReuseRoute = () => false;
}
```

this might solve your problem.
