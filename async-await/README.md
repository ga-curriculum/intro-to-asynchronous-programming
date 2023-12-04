# ![Intro to Asynchronous Programming - Async/Await](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to use the async/await syntax applies to asynchronous operations in JavaScript.

## What is Async/Await? 

*Async/Await syntax* is an approach to handling operations that don't happen instantaneously, like fetching data from a database or an API. Async/Await syntax makes the handling of asynchronous operations more straightforward and readable. Async/Await is essentially "syntactic sugar" built on top of promises, in that it doesn't add new functionality but simplifies existing patterns.  

*`async`*
When the `async` keyword is placed before a function declaration, it makes the function asynchronous, meaning the function will now return a promise that resolves into the actual value the function returns.

*`await`*
The `await` operator is used to pause the execution of code until a promise is resolved. The  `await` operator can only be used inside an `async` function.

Check [**MDN - async and await**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await) for more information on async and await. 

## Anatomy of an `async` function

Let's take a moment to get a sense of how an `async` function is defined. Take a look at the hypothetical example below:

```javascript
async function index() {
  const response = todoDB.find();
  console.log(response);
};
```

Notice how this syntax is quite similar to standard function declarations. The key difference is the addition of the `async` keyword. In this example, the `find()` method of our `todoDB` will take time to complete its task. As a result, the operation will return a promise.

If we were to run this code, the `console.log()` would print out the following:

```javascript
Promise { <pending> }
```

The `response` variable holds a `pending` `Promise`. To access the actual data returned from the `find()` method, we need to use the `await` operator.

## Using `await` in `async` functions

The `await` operator allows us to pause the function execution until a promise resolves.

Take a look at the updated code below:

```javascript
async function index() {
  const response = await todoDB.find(); // Waits for the Promise to resolve
  console.log(response);
};
```

After adding the `await` operator, running this code would display the resolved promise, i.e., the actual data returned from `todoDB.find()`:

```javascript
[
  { id: 1, task: 'Learn React', completed: false },
  { id: 2, task: 'Learn Express', completed: false },
  { id: 3, task: 'Build Tic-Tac-Toe', completed: false }
]
```

Notice how the `await` keyword transforms the way we handle asynchronous operations. It waits for `todoDB.find()` to complete and then stores the resolved data in `response`. This makes our asynchronous code more readable and easier to follow.