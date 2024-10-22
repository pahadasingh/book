![Preview image](https://miro.medium.com/v2/resize:fit:700/1*dr5OBWrKBLAoiA__9wUP-w.png)

Can You Answer This Senior Level JavaScript Promise Interview Question?
=======================================================================

Most interviewees failed on it.
-------------------------------

What is the output of the following code?

```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1);
  setTimeout(() => {
    console.log("timerStart");
    resolve("success");
    console.log("timerEnd");
  }, 0);
  console.log(2);
});

promise.then((res) => {
  console.log(res);
});

console.log(4);
```

### Analysis

It's not a friendly question for junior JS coders.

The core feature of JavaScript is asynchronous programming. The interpreter always executes synchronous code first and then asynchronous code.

For example, in this code:

```javascript
console.log('start');

const promise1 = new Promise((resolve, reject) => {
  console.log(1)
  resolve(2)
})
promise1.then(res => {
  console.log(res)
})
console.log('end');
```

`promise1.then()` is an asynchronous function call.

![None](https://miro.medium.com/v2/resize:fit:700/1*dr5OBWrKBLAoiA__9wUP-w.png)

So the output is `start` , `1` , `end` and `2` .

But in JavaScript, asynchronous tasks are also divided into micro tasks and macro tasks.

We generally divide vehicles into two categories:

-   General vehicles
-   Vehicles for emergency missions. Such as fire trucks and ambulances.

When passing through crowded intersections, we will allow fire trucks and ambulances to pass first. Emergency vehicles have more priorities than other vehicles. Keywords: priorities.

![None](https://miro.medium.com/v2/resize:fit:700/1*rIR3M1_sq2z0ygVNvFfWSg.png)

In JavaScript EventLoop, there is also the concept of priority.

-   Tasks with higher priority are called microtasks. Includes: `Promise`, `ObjectObserver`, `MutationObserver`, `process.nextTick`, `async/await` .
-   Tasks with lower priority are called macrotasks. Includes: `setTimeout` , `setInterval` and `XHR` .

![None](https://miro.medium.com/v2/resize:fit:700/1*3jL2xPwDt8ERouPhwecd5w.png)

In this code snippet:

```javascript
console.log('start')

setTimeout(() => {
  console.log('setTimeout')
})
Promise.resolve().then(() => {
  console.log('resolve')
})
console.log('end')
```

Although `setTimeout` and `Promise.resolve()` are completed at the same time, and even the code of `setTimeout` is still ahead, but because of its low priority, the callback function belonging to it is executed later.

![None](https://miro.medium.com/v2/resize:fit:700/1*egC76tBMcuRhbJziUqsm8w.png)

OK, now that we have explained the basics, let's go back to our original question.

To solve this question, we just need to do three steps:

1.  Find the synchronization code.
2.  Find the microtask code
3.  Find the macrotask code

First, execute the synchronization code:

First, execute the synchronization code:

![None](https://miro.medium.com/v2/resize:fit:700/1*W9XjtG52Na3sZbz7n9XRCw.png)

Output `1` , `2` and `4` .

Then execute microtask:

![None](https://miro.medium.com/v2/resize:fit:700/1*hZVbY5J0J5Gq8C3vHFHvGQ.png)

But here is a trap: Since the current promise is still in the pending state, the code in this will not be executed at present.

Then execute macrotask:

![None](https://miro.medium.com/v2/resize:fit:700/1*gY5rs_5o8L23ovi0JCStnA.png)

And the state of the `promise` becoming to `fulfilled` .

Then, with Event Loop, execute the microtask again:

![None](https://miro.medium.com/v2/resize:fit:700/1*CXmdTAc4LwHIQVhH5LUznA.png)

And the state of the `promise` becoming to `fulfilled` .

Then, with Event Loop, execute the microtask again:

![None](https://miro.medium.com/v2/resize:fit:700/1*CXmdTAc4LwHIQVhH5LUznA.png)
