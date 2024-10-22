Angular: Everything You Need To Know About Handling Errors
==========================================================

Reliability is one of the core principles of any system design and an Angular application is no exception. An application can face many errors such as logical, runtime, network, etc. Things can go wrong at any time and are called faults in an application. And, the system that can handle these faults is fault-tolerant. This article aims to explain everything about handling errors in an Angular application to make it reliable.

Without any more words, let's face errors.

### Expected Errors --- Synchronous

Using try-catch on a code is our first line of defense where we know errors can come. The try/catch block allows you to capture any errors that can come in a certain piece of code.

```javascript
try {
  // Error prone code
} catch(e) {
  // Do something with the error
}
```

This will capture the error immediately and will save our application from crashing.

However, we should be careful as it might not work as expected for asynchronous code.

```
try {
  setTimeout(() => {
    // Code that might throw an error
    throw new Error("Something went wrong!");
  }, 1000);
} catch(e) {
  console.log(e); // This will not work
}
```

The catch block will not capture the error in the above code because setTimeout is asynchronous. The try/catch block should be on the synchronous code.

```typescript
setTimeout(() => {
  try {
  // Code that might throw an error
      throw new Error("Something went wrong!");
  } catch(e) {
    console.log(e); // This will work
  }
}, 1000);
``V`

We know that in a bigger application, it is hard to capture every kind of error using a try/catch block as there are many edge cases. Then how to avoid a crash in this case?

### Global Error Handler

All application errors that are not captured by a try/catch block move up and are captured by the Angular [Error Handler](https://angular.io/api/core/ErrorHandler). By default, this error handler will simply log the error to the console.

> The error handler is a centralized place to handle all application exceptions.

But let's say we don't the user to continue when the application is no longer in a working state. We want to take the user to an error page after logging the error. To achieve this, we can replace the default error handler with our custom error handler.

We need to implement the ErrorHandler interface to create an error handler.

```typescript
import { ErrorHandler, Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: Error): void {
    // Implement this method
  }
}
```

This interface will force us to implement the handleError method which will get called on an error. Now we will simply after logging move the user to the error page in this method.

```typescript
import { ErrorHandler, Injectable, inject } from '@angular/core';
import { Router } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class GlobalErrorHandler implements ErrorHandler {
  router = inject(Router); // Inject Router
  handleError(error: Error): void {
     console.error(error);
     this.router.navigateByUrl('/error');
  }
}
```

Now as a final step, we need to override the Angular error handler with our handler. To do so, we need to provide it in our application module.

```typescript
@NgModule({
  ...
  providers: [
    {
      provide: ErrorHandler,
      useClass: GlobalErrorHandler
    },
  ],
  ...
})
export class AppModule { }
```

### Expected Errors --- Asynchronous

We know that Angular heavily uses RxJS observables for asynchronous behavior. Similar to try/catch, we can also capture errors for observables.

Let's say one of our observables is throwing an error as follows. If we don't capture it, then it will go to the global error handler as we have seen previously.

```typescript
ngOnInit(): void {
  of(true)
    .pipe(
      tap(() => {
        throw new Error('SOMETHING');
      })
    )
    .subscribe();
}
```

One way to capture this error is using the RxJS [catchError](https://rxjs.dev/api/operators/catchError) operator. This operator returns another error observable, which can be the same error, a modified one, or an [empty observable](https://rxjs.dev/api/index/const/EMPTY) to stop propagating the error.

```typescript
of(true)
  .pipe(
    tap(() => {
      throw new Error('Error');
    }),
    catchError((error) => {
      console.log("CAPTURED");
      return EMPTY; // RxJS empty obserable
    })
  )
  .subscribe();
```

For example, if we don't want to take the user to an error page for some specific errors, we can return EMPTY observable, so that the error will not reach the global error handler.

We can capture it inside the subscribe block as well. We just need to use the error callback function.

```typescript
of(true)
  .pipe(
    tap(() => {
      throw new Error('Error');
    })
  )
  .subscribe({
    next: () => console.log("Success"),
    error: (e) => console.log("CAPTURED", e)
  });
```

### Global API Failures

In the final case, we will capture the HTTP call failures. As Angular uses observables for HTTP calls as well, we can capture these using the above-mentioned methods by using the catchError operator or inside the subscribe.

However, it is better to handle these errors centrally similar to the global error handler. For example, if we want to take the user to a new "server-error" page for any HTTP call failure.

We can use [HTTP Interceptor](https://angular.io/api/common/http/HttpInterceptor) for that where an interceptor intercepts all HTTP calls going out of the application. We have access to the HttpRequest and HttpResponse inside this interceptor.

To create an interceptor, we need to implement the HttpInterceptor interface and implement the intercept method.

```typescript
@Injectable()
export class ErrorResponseInterceptor implements HttpInterceptor {

  // Implement the intercept method
  intercept(req: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    // Continue with the request and capture the error
    return next.handle(req).pipe(
      catchError((err: unknown) => {
        this.router.navigateToUrl('/server-error');
        return EMPTY;
      })
    );
  }
```