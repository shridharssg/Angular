### Table of Contents

| No. | Questions |
|---- | ---------
|1| [What is Angular Router?](#what-is-angular-router)|
|2| [What is the purpose of base href tag?](#what-is-the-purpose-of-base-href-tag)|
|3| [What are the router imports?](#what-are-the-router-imports)|
|4| [What is router outlet?](#what-is-router-outlet)|
|5| [What are router links?](#what-are-router-links)|
|6| [What are active router links?](#what-are-active-router-links)|
|7| [What is router state?](#what-is-router-state)|
|8| [What are router events?](#what-are-router-events)|
|9| [What is activated route?](#what-is-activated-route)|
|10| [How do you define routes?](#how-do-you-define-routes)|
|11| [What is the purpose of Wildcard route?](#what-is-the-purpose-of-wildcard-route)|
|12| [Do I need a Routing Module always?](#do-i-need-a-routing-module-always)|
|13| [What are the Route Parameters? Could you explain each of them?](#what-are-the-route-parameters-could-you-explain-each-of-them)
|14| [What is safe navigation operator?](#what-is-safe-navigation-operator)|

1. ### What is Angular Router?
    Angular Router is a mechanism in which navigation happens from one view to the next as users perform application tasks. It enables developers to build Single Page Applications with multiple views and allow navigation between these views.

  **[⬆ Back to Top](#table-of-contents)**

2. ### What is the purpose of base href tag?
    The routing application should add <base> element to the index.html as the first child in the <head> tag in order to indicate how to compose navigation URLs. If app folder is the application root then you can set the href value as below

    ```html
    <base href="/">
    ```

  **[⬆ Back to Top](#table-of-contents)**

3. ### What are the router imports?
    The Angular Router is not part of Angular Core. It is available in library named `@angular/router` so need to import required router components. For example, we import them in app module as below,

    ```javascript
    import { RouterModule, Routes } from '@angular/router';
    ```

  **[⬆ Back to Top](#table-of-contents)**

4. ### What is router outlet?
    To render components associated with routes, you need to add a <router-outlet></router-outlet> element in your main app component's template. This is where the activated component will be displayed.
   Router outlet is used like a component,

    ```html
    <router-outlet></router-outlet>
    <!-- Routed components go here -->
    ```

  **[⬆ Back to Top](#table-of-contents)**

5. ### What are router links?
   You can navigate to different routes using the RouterLink directive in your templates. The RouterLink is a directive on the anchor tags.

    ```html
    <h1>Angular Router</h1>
    <nav>
      <a routerLink="/todosList" >List of todos</a>
      <a routerLink="/completed" >Completed todos</a>
    </nav>
    <router-outlet></router-outlet>
    ```

    Programmatically, you can use the Router service for navigation in component code.

    ```javascript
    import { Router } from '@angular/router';
    constructor(private router: Router) {}
    navigateToProducts() {
      this.router.navigate(['/products']);
    }
    ```

  **[⬆ Back to Top](#table-of-contents)**

6. ### What are active router links?
    RouterLinkActive is a directive that toggles css classes for active RouterLink bindings based on the current RouterState. i.e, The Router will add CSS classes when this link is active and remove when the link is inactive. For example, you can add them to RouterLinks as below.

    ```html
    <h1>Angular Router</h1>
    <nav>
      <a routerLink="/todosList" routerLinkActive="active">List of todos</a>
      <a routerLink="/completed" routerLinkActive="active">Completed todos</a>
    </nav>
    <router-outlet></router-outlet>
    ```

  **[⬆ Back to Top](#table-of-contents)**

7. ### What is router state?
    RouterState is a tree of activated routes. Every node in this tree knows about the "consumed" URL segments, the extracted parameters, and the resolved data. You can access the current RouterState from anywhere in the application using the `Router service` and the `routerState` property.

    ```javascript
    @Component({templateUrl:'template.html'})
    class MyComponent {
      constructor(router: Router) {
        const state: RouterState = router.routerState;
        const root: ActivatedRoute = state.root;
        const child = root.firstChild;
        const id: Observable<string> = child.params.map(p => p.id);
        //...
      }
    }
    ```

  **[⬆ Back to Top](#table-of-contents)**

8. ### What are router events?
    During each navigation, the Router emits navigation events through the Router.events property allowing you to track the lifecycle of the route.

    The sequence of router events is as below,

    1. NavigationStart,
    2. RouteConfigLoadStart,
    3. RouteConfigLoadEnd,
    4. RoutesRecognized,
    5. GuardsCheckStart,
    6. ChildActivationStart,
    7. ActivationStart,
    8. GuardsCheckEnd,
    9. ResolveStart,
    10. ResolveEnd,
    11. ActivationEnd
    12. ChildActivationEnd
    13. NavigationEnd,
    14. NavigationCancel,
    15. NavigationError
    16. Scroll

  **[⬆ Back to Top](#table-of-contents)**

9. ### What is activated route?
    ActivatedRoute contains the information about a route associated with a component loaded in an outlet. It can also be used to traverse the router state tree. The ActivatedRoute will be injected as a router service to access the information. In the below example, you can access route path and parameters,

    ```javascript
    @Component({...})
    class MyComponent {
      constructor(route: ActivatedRoute) {
        const id: Observable<string> = route.params.pipe(map(p => p.id));
        const url: Observable<string> = route.url.pipe(map(segments => segments.join('')));
        // route.data includes both `data` and `resolve`
        const user = route.data.pipe(map(d => d.user));
      }
    }
    ```

  **[⬆ Back to Top](#table-of-contents)**

10. ### How do you define routes?
     A router must be configured with a list of route definitions. You configures the router with routes via the `RouterModule.forRoot()` method, and adds the result to the AppModule's `imports` array.

    ```javascript
     const appRoutes: Routes = [
      { path: 'todo/:id',      component: TodoDetailComponent },
      {
        path: 'todos',
        component: TodosListComponent,
        data: { title: 'Todos List' }
      },
      { path: '',
        redirectTo: '/todos',
        pathMatch: 'full'
      },
      { path: '**', component: PageNotFoundComponent }
    ];

    @NgModule({
      imports: [
        RouterModule.forRoot(
          appRoutes,
          { enableTracing: true } // <-- debugging purposes only
        )
        // other imports here
      ],
      ...
    })
    export class AppModule { }
    ```

   **[⬆ Back to Top](#table-of-contents)**

11. ### What is the purpose of Wildcard route?
    If the URL doesn't match any predefined routes then it causes the router to throw an error and crash the app. In this case, you can use wildcard route. A wildcard route has a path consisting of two asterisks to match every URL.

    For example, you can define PageNotFoundComponent for wildcard route as below
    ```javascript
    { path: '**', component: PageNotFoundComponent }
    ```

  **[⬆ Back to Top](#table-of-contents)**

12. ### Do I need a Routing Module always?
    No, the Routing Module is a design choice. You can skip routing Module (for example, AppRoutingModule) when the configuration is simple and merge the routing configuration directly into the companion module (for example, AppModule). But it is recommended when the configuration is complex and includes specialized guard and resolver services.

  **[⬆ Back to Top](#table-of-contents)**


13. ### What are the Route Parameters? Could you explain each of them?.
      Route parameters are used to pass dynamic values in the URL of a route. They allow you to define variable segments in the route path, which can be accessed and used by components and services. Path parameters are represented by a colon (":") followed by the parameter name.

      There are three types of route parameters in Angular:

      **Path parameters:** Path parameters are used to define dynamic segments in the URL path. They are specified as part of the route's path and are extracted from the actual URL when navigating to that route. Path parameters are represented by a colon (":") followed by the parameter name. For example:

      ```typescript
      { path: 'users/:id', component: UserComponent }
      ```

      In this example, ":id" is the path parameter. When navigating to a URL like "/users/123", the value "123" will be extracted and can be accessed in the UserComponent.

      **Query parameters:** Query parameters are used to pass additional information in the URL as key-value pairs. They are appended to the URL after a question mark ("?") and can be accessed by components and services. Query parameters are not part of the route path, but they provide additional data to the route. For example:

      ```typescript
      { path: 'search', component: SearchComponent }
      ```

      In this example, a URL like "/search?query=angular" contains a query parameter "query" with the value "angular". The SearchComponent can retrieve the value of the query parameter and use it for searching.

      **Optional parameters:** Optional parameters are used when you want to make a route parameter optional. They are represented by placing a question mark ("?") after the parameter name. Optional parameters can be useful when you have routes with varying parameters. For example:

      ```typescript
      { path: 'products/:id/:category?', component: ProductComponent }
      ```

      In this example, the ":category" parameter is optional. The ProductComponent can be accessed with URLs like "/products/123" or "/products/123/electronics". If the ":category" parameter is present in the URL, it will be available in the component, otherwise, it will be undefined.

      Route parameters provide a flexible way to handle dynamic data in your Angular application. They allow you to create routes that can be easily customized and provide a seamless user experience by reflecting the current state of the application in the URL.

      **[⬆ Back to Top](#table-of-contents)**



14. ### What is safe navigation operator?
     The safe navigation operator(?)(or known as Elvis Operator) is used to guard against `null` and `undefined` values in property paths when you are not aware whether a path exists or not. i.e. It returns value of the object path if it exists, else it returns the null value.

     For example, you can access nested properties of a user profile easily without null reference errors as below,
     ```javascript
     <p>The user firstName is: {{user?.fullName.firstName}}</p>
     ```
     Using this safe navigation operator, Angular framework stops evaluating the expression when it hits the first null value and renders the view without any errors.


 15. ### Route Parameters

    Routes can have parameters to pass data between components. You define route parameters in the route configuration.

    ```javascript
    const routes: Routes = [
      { path: 'products/:id', component: ProductDetailComponent },
    ];
    
    ```

    Access route parameters in a component using ActivatedRoute.

    ```javascript    
        import { ActivatedRoute } from '@angular/router';
        constructor(private route: ActivatedRoute) {
          this.route.params.subscribe(params => {
            this.productId = params['id'];
          });
        }
    ```
    
    ---

 16. ### Child Routes:
     
    You can create nested or child routes to organize your application’s routes hierarchically.
    
    ```javascript    
    const routes: Routes = [
      {
        path: 'products',
        component: ProductsComponent,
        children: [
            { path: 'list', component: ProductListComponent },
          { path: 'detail/:id', component: ProductDetailComponent },
        ],
      },
    ];
    ```
    
17. ### Lazy Loading:

Lazy loading allows you to load parts of your application on-demand, reducing initial loading times. You configure lazy-loaded routes using the loadChildren property. 

```
    const routes: Routes = [
      {
        path: 'admin',
        loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule),
      },
    ];
```
