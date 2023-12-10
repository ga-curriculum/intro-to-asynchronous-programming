# ![Intro to Asynchronous Programming - Async/Await](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to use the async/await syntax applies to asynchronous operations in JavaScript.
## The problem with callbacks

Developers will often times nest several callback functions when dealing with asynchronous code. However, when callbacks need to call functions that also accept callbacks, it leads to deeply nested structures. This is also known as "callback hell" or the "pyramid of doom". The resulting code becomes hard to read and debug, as illustrated by the pyramid-like structure in the code below:

```javascript
const loadApplication = () => {
  request('/api/customers', (response) => {
    const customerId = response.customers[0];
    request(`/api/customers/${customerId}`, (response) => {
      const photoId = response.customer.photoId;
      request(`/api/photos/${photoId}`, (response) => {
        console.log('Callback Hell');
      });
    });
  });
}
```

To avoid this pattern, ES6 introduced Async/Await
## What is Async/Await? 

*Async/Await syntax* is an approach to handling operations that don't happen instantaneously, like fetching data from a database or reading a file. Async/Await syntax makes the handling of asynchronous operations more straightforward and readable.  The only downside is that you need to learn two new JavaScript keywords.

*`async`*
When the `async` keyword is placed before a function declaration, it alerts javascript to the fact that there may be asynchronous operations that may need to run synchronously (i.e. line by line)

*`await`*
The `await` operator is used to pause the execution of code until an asynchronous operation has completed. The  `await` operator can only be used inside an `async` function.

Check [**MDN - async and await**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await) for more information on async and await. 
## Anatomy of an `async` function

Let's take a look at the code we previously wrote in `example.js` to read a file using a callback:

```javascript
const fs = require('node:fs');

fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
});

console.log('run this as soon a possible');
```

It's bit confusing because `console.log('run this as soon a possible');` on the line 7 of the code above runs before `console.log(data);` on line 4.  Let's rewrite this using async/await:

```javascript
const fs = require('node:fs/promises');

const example = async () => {
	const data = await fs.readFile('test.txt', { encoding: 'utf8' });
	console.log(data);
	console.log('run this second');
}

example();
```

A couple of things to note:

- `const fs = require('node:fs/promises');` this is a slightly different NodeJS package that we're using which enables `async`/`await` syntax.
- We define and then invoke an `async` function called `example` because lines marked `await` need to occur inside `async` functions and can't occur in global scope.

Once Node has entered the invocation of `example()`, the flow of control runs in an easily readable manner from one line to the next without any need for callbacks.  This is because we have added the `await` keyword in front of `fs.readFile`.  In addition, the `await` keyword allows `fs.readFile` to return the contents of the file as a string, rather than pass it into a callback function as an argument.  This allows us to assign this information to the variable `data`.  The code:

```javascript
const data = await fs.readFile('test.txt', { encoding: 'utf8' });
console.log(data);
```

is much more readable than:

```javascript
fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
});
```