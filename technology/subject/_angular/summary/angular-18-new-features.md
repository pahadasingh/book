## What's New in Angular 18?

- Experimental zoneless support 
- Native async / await 
- Fallback for ng-content 
- New form events Observable 
- Route redirects as functions 
- SSR hydration with replay 
- Angular Material uses Material 3 
- http://angular.dev is the new docs home


The latest version of Angular, Angular 18 release has brought up features that aim for improved performance, better scalability, and rich user experiences. Check these out.

### 1. Zoneless Applications

Angular has traditionally relied on zone.js, but it has incurred various issues in areas of developer experience and performance. As a result, the Angular team has proposed experimental APIs for zoneless change detection.

Developers can now explore this new zoneless support by adding `provideExperimentalZonelessChangeDetection` to their application bootstrap process and eliminating zone.js from polyfills in `angular.json.`

```
bootstrapApplication(App, {
providers: [
    provideExperimentalZonelessChangeDetection()
]
});

```

We have found that signals are the ideal method to employ zoneless in your components.

````
@Component({
    ...
    template: ```
    <h1>Hello from {{ name() }}!</h1>
    <button (click)="handleClick()">Go Zoneless</button>
    ```,
})
export class App {
    protected name = signal('Angular');

    handleClick() {
        this.name.set('Zoneless Angular');
    }
}

````

For components, the transition is seamless, especially for those using `ChangeDetectionStrategy.OnPush`. This marks a significant step towards improving performance and developer experience by reducing dependency on zone.js.

### 2. Route Redirects with Functions

New with Angular 18 is the ability for functions to handle redirects, replacing the static strings in the `redirectTo` property of the Route object. This increases flexibility in routing. The function can parse an object with URL parameters and can return a string or the UrlTree. Thereby increasing the efficiency and navigation with web applications.

```
const routes: Routes = [
{ path: "first-component", component: FirstComponent },
{
    path: "old-user-page",
    redirectTo: ({ queryParams }) => {
        const errorHandler = inject(ErrorHandler);
        const userIdParam = queryParams['userId'];
        if (userIdParam !== undefined) {
            return `/user/${userIdParam}`;
        } else {
            errorHandler.handleError(new Error('Attempted navigation to user page without user ID.'));
            return `/not-found`;
        }
    },
},
{ path: "user/:userId", component: OtherComponent },
];
```

### 3. TypeScript 4.7 Support

Angular 18 offers support for TypeScript 4.7 by introducing several new features and enhancements that are helpful for developers. These features include template literal types, improved `readonly` support, and new Import Types, which help in perfect template typing, better understanding of the `readonly` keyword, and better modularity of the code, respectively.

### 4. Latest ng-template API

With the new `ng-template` API, people do not need to create a new template and use specific selectors all the time. Moreover, the new API is also reusable.

### 5. Upgraded Debugging Tools

Angular 18 comes with new debugging tools that make it easier to debug the applications and test since it provides information on the state of the application, debugging with source maps, component trees, data bindings, and performance profiling.

### 6. New Official Documentation Website

Angular developers now have a new home at Angular with `angular.dev` being declared as the official documentation website. So, from now onwards all the requests to `angular.io` will be automatically forwarded to `angular.dev`. The new website provides a contemporary experience with a WebContainer-based, hands-on tutorial. Moreover, it offers a live playground for developers with examples, an enhanced Algolia-based search, redesigned guides, and streamlined navigation.

![Home page of Angular.dev](https://d2ms8rpfqc4h24.cloudfront.net/ss1_bf13593350.jpg)

### 7. Hydration Support in CDK and Material

All Angular Material and CDK components, along with primitives, are now fully hydration compatible, ensuring consistent rendering behavior.

### 8. Unified Control State Change Events

In the v18 release of Angular, forms introduce a new property called `events` in the `FormControl`, `FormGroup`, and `FormArray` classes. This property enables developers to subscribe to a stream of events for each form control, providing granular tracking of changes in value, touch state, pristine status, and control status. So, with this new feature, you can use the following -

```
const nameControl = new FormControl<string|null>('name', Validators.required);
nameControl.events.subscribe(event => {
// process the individual events
});

```

### 9. Coalescing by Default

In Angular v18, coalescing is now enabled by default for apps using zone.js with coalescing enabled. This change reduces the number of change detection cycles, improving performance for some applications. However, this behavior is only enabled for new applications to avoid potential bugs in existing apps. To opt for event coalescing for existing projects, configure the `NgZone` provider in `bootstrapApplication`.

```
bootstrapApplication(App, {
providers: [
    provideZoneChangeDetection({ eventCoalescing: true })
]
});

```

### 10. Event Replay

![Event Replay Feature in Angular v18](https://d2ms8rpfqc4h24.cloudfront.net/ss2_635ffb8e26.jpg)

Angular v18 introduced the event replay feature as a developer preview, enabled using `withEventReplay()`. This feature, powered by event dispatch, ensures a seamless user experience for hybrid rendering.
What's New in Angular 18?

https://blog.angular.dev/angular-v18-is-now-available-e79d5ac0affe