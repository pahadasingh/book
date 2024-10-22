Let's be honest, Angular isn't the easiest thing to pick up. It's a framework after all, so there are things you need to adhere to for anything to work.

But Angular still has its perks.

### The Perks of Angular

For the uninitiated, Angular appears cumbersome, with large swathes of knowledge required before you can even get started with the framework.

But let's get real. That's with anything in general. When we're required to learn new things, some of us have an automatic resistor in our brains that feels the Dunning-Krueger effect most acutely.

Learning new things becomes more annoying over time when we've become accustomed to our comfort zone, especially when we're supposed to be the expert.

But we're all noobs, at some level, and the more general concept knowledge you can transfer between frameworks, libraries, and ideas, the easier it is to get over that feeling when climbing the learning curve for something new.

![None](https://miro.medium.com/v2/resize:fit:700/0*dUugyn0FI4YGY7bA.jpg)

[Why We're Ignorant of Our Own Ignorance](https://www.safalniveshak.com/ignorant-of-our-own-ignorance/)

I'm digressing. So why do people use Angular?

Angular uses a component-based architecture that makes organizing code into bite-sized blocks easier with a clear separation of concerns. Modularity is the foundation of Angular's framework.

You can say the same thing for React and Vue, but how it's implemented is what separates Angular from the pack.

Angular is strongly opinionated. This means that if you want to do something, you must do it a certain way. There's no negotiation over it. Meanwhile, React is a library, which means there is flexibility in how things are implemented, but it can also lead to variability.

For small projects, React is great because you can just do whatever you want and how you want it. But as the project grows and different opinions clash in teams, this can lead to conflicts over what certain patterns and implementations should look like.

One person's version of best practices might not align with another opinionated team member. We're human. It happens. React and Vue are used for large projects, so it's not the end of the world --- just more negotiations and standardization required by the team.

Angular eliminates this by providing the blueprint for how things need to be done.

#### But surely, there's more to it than just enforced modularity?

Yes. Yes, there is.

Dependency injection is another feature that makes Angular great. Although React has caught up in recent years (sort of), the way Angular handles dependency injections makes the process of working with dependencies seamless.

But what is dependency injection?

Dependency Injection (DI) is a design pattern used in software development that helps to decouple components and their dependencies. In simple terms, DI is a way to provide a component or class with the dependencies it needs to function rather than having the component instantiate or create those dependencies itself.

In Angular, Dependency Injection is a core feature that simplifies the process of managing dependencies in an application. Angular's DI system is built around the concept of injectors and providers. An injector is responsible for creating and managing instances of dependencies, while providers are used to configure how those dependencies should be created.

#### Here's why Dependency Injection matters

Decoupling: DI promotes loose coupling between components and their dependencies, making it easier to modify, test, and maintain the code. By injecting dependencies, components are not tightly bound to specific implementations, which allows for greater flexibility when making changes.

Reusability: With DI, you can easily reuse and share instances of services or other dependencies across different parts of your application. This reduces code duplication and leads to a cleaner, more organized codebase.

Testability: DI makes writing unit tests for components or classes easier, as you can easily substitute real dependencies with mock objects. This allows you to isolate the component or class being tested and focus on its functionality rather than worrying about the behavior of its dependencies.

Here's a simple example illustrating Dependency Injection in Angular:

```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class UserService {
  getUsers() {
    // Logic to fetch users from an API or other data source
  }
}
```

In this example, we define a `UserService` class with a `getUsers` method. The `@Injectable` decorator tells Angular that this class can be used as a dependency and should be managed by the DI system.

Now, let's create a component that needs the `UserService` to fetch user data:

```
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-users',
  template: `
    <ul>
      <li *ngFor="let user of users">{{ user.name }}</li>
    </ul>
  `,
})
export class UsersComponent implements OnInit {
  users = [];

  constructor(private userService: UserService) {}

  ngOnInit() {
    this.users = this.userService.getUsers();
  }
}
```

In this `UsersComponent`, we inject the `UserService` by adding it as a parameter in the constructor. Angular's DI system automatically handles creating an instance of the `UserService` and provides it to the component. This way, we can use the `userService` instance to fetch users when the component initializes without worrying about manually instantiating or managing the `UserService`.

By using Dependency Injection in Angular, you can create cleaner, more maintainable, and testable code, ultimately leading to more robust and scalable applications.

In contrast, React and Vue handle dependency injection differently than Angular. They are more lightweight and less opinionated, so they don't provide a built-in dependency injection system as Angular does. However, developers can still achieve dependency injection in React and Vue applications using different techniques and libraries.

React use "props" to pass data and dependencies down the component tree. While this can work for simple applications, it becomes less manageable as the application grows. To handle dependency injection in larger React applications, developers can use third-party libraries such as InversifyJS or rely on React's context API, which allows sharing values across the component tree without passing them through props.

```
// createContext
import React, { createContext, useContext } from 'react';
import UserService from './UserService';

const UserServiceContext = createContext(new UserService());

function Users() {
  const userService = useContext(UserServiceContext);
  // Use userService to fetch user data
}
```

Meanwhile, Vue has a built-in mechanism called "provide/inject" for handling dependency injection. While it is not as robust as Angular's DI system, it allows for sharing data and dependencies between components without passing them through props.

```
// In a parent component or Vue instance
import UserService from './UserService';

export default {
  provide: {
    userService: new UserService(),
  },
};

// In a child component
export default {
  inject: ['userService'],
  // Use userService to fetch user data
};
```

Angular's dependency injection system is more advanced and opinionated than React and Vue. It is built into the framework, making it easy to manage dependencies consistently throughout the application. Angular's DI system uses decorators, hierarchical injectors, and providers, providing more flexibility and control over creating and managing dependencies.

### Getting Back to the Point: Who's Still Using Angular?

According to [Stack Overflow's 2022 Developer Survey](https://survey.stackoverflow.co/2022/), Angular takes 20.39% of the web frameworks and technologies pie. While React sits at 42.62%, it should be noted that Stack Overflow makes it a point to say that Angular is *"used more by professional developers than those learning to code."*

This suggests that while React is popular, its popularity might be fueled by it being a gateway into building single-page apps for the web. Meanwhile, Vue, the love child of Angular's predecessor (**ahem** Angular.js, which is completely different from Angular as we know it today), comes in at a solid 18.82% in the popularity vote.

According to the [State of JS 2021](https://2021.stateofjs.com/en-US/libraries/front-end-frameworks/), the number of frameworks and libraries mixed and matched has splintered over time.

![None](https://miro.medium.com/v2/resize:fit:700/1*j8oj28iQqBi1d_YxFJerNQ.png)

The numbers don't add to 100 because they never will. The standardizing of portability and modularity of JS, in general, means that frameworks and libraries are not used in isolation.

Regarding Google trends, React is the clear winner, but it doesn't account for the different types and levels of developers working with the library or framework.

![None](https://miro.medium.com/v2/resize:fit:700/1*RkNGu3nwizZ6l7Jv5PUQmA.png)

In my research, there is an emphasis on Angular being used by enterprises more than startups.

So I got curious about the pay differences.

According to [Arc](https://arc.dev/salaries), Remote Angular Developers make a global average of $71,326 per year. In contrast, Remote React Developers make a global average of $72,342 annually.

![None](https://miro.medium.com/v2/resize:fit:700/1*jBQhVRFFuurvByEXoUg48A.png)

![None](https://miro.medium.com/v2/resize:fit:700/1*a4wN7AccVpOPUfNpdeJ_zQ.png)

However, the stats at [Glassdoor](https://www.glassdoor.com/Salaries/new-york-angular-developer-salary-SRCH_IL.0,8_IC1132348_KO9,26.htm) paints a different picture.

![None](https://miro.medium.com/v2/resize:fit:700/1*DvfXE38RjUx0aKV0XBuN9A.png)

![None](https://miro.medium.com/v2/resize:fit:700/1*JhYP91eAeO1HG67TqWg_Iw.png)

### Is Angular Still Worth Learning? Keeping?

All in all, it doesn't really matter much which framework or library you specialize in. It's the ability to meet the needs and expectations of your project or client that matters the most.

At the end of it all, non-tech people don't really care about the intricacies of how modular or clean your code is --- what matters is that the digital real estate they're asking you to build is working and won't break at the first signs of high volume traffic --- which is more infrastructure scaling than the framework or library itself.

Don't get me wrong, the ideas enforced by Angular are good and can teach you fantastic habits for keeping things clean and tidy. It's good to have a general knowledge of everything than just pigeonhole yourself to one thing.

Being a master of something helps with advertising yourself, but when it comes to the real work of coding, it's an ad-hoc space of stringing together pieces that you know from your previous projects to make things work.