# Node.js Event Loop Assignment

## Question

Consider:

console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C");

Why does Node.js print A, C, and then B instead of A, B, C?

## Answer

Node.js executes synchronous code first.

First, console.log("A") runs immediately, so the output is A.

Then setTimeout() is encountered. Even though the delay is 0 milliseconds, its callback does not execute immediately. The callback is scheduled to run later by the Node.js event loop.

After that, console.log("C") runs synchronously, so the output is C.

Once the synchronous code has finished and the call stack becomes empty, the event loop allows the timer callback to execute. Therefore, console.log("B") runs last.

Hence, the output is:

A
C
B

## Role of the Event Loop

The Node.js event loop allows Node.js to handle asynchronous operations without blocking the main thread.

The basic flow is:

1. Synchronous code runs on the call stack.
2. Asynchronous operations such as timers are scheduled.
3. Node.js continues executing synchronous code.
4. When the call stack becomes empty, the event loop processes eligible callbacks.
5. The setTimeout callback executes and prints B.