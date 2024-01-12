# ![Intro to Asynchronous Programming - Async/Await](./assets/hero.png)

**Learning Objective:** By the end of this lesson, students will understand how the async/await syntax applies to asynchronous operations in JavaScript.

## Asynchronous code and the challenge with callbacks

Developers will often times nest several functions when they need to perform multiple async operations that depend on one another. However, when callbacks need to call functions that also accept callbacks, it leads to deeply nested structures. This is known as "callback hell" or the "pyramid of doom". The resulting code becomes hard to read and debug.

To see an example of this, let's create two more files, similar to the `test.txt` file we created before. 

Put the following content in `test2.txt`:

```
hello 2!
```

Repeat the process again, with a `test3.txt` file:

```
hello 3!
```

Now let's update `app.js` to print the contents of both of these files, synchronously:

```javascript
// app.js
const fs = require('node:fs');

fs.readFile('test.txt', 'utf8', (err, data) => {
  console.log(data);
  fs.readFile('test2.txt', 'utf8', (err2, data2) => {
    console.log(data2);
    fs.readFile('test3.txt', 'utf8', (err3, data3) => {
      console.log(data3);
    });
  });
});

console.log('run this as soon as possible');
```

Test the code:

```bash
node app.js
```

**Problem:** Now imagine many more layers of this structure in a larger application. While it works as intended, this code leads to deeply nested functions that become difficult to read and maintain.

## Introducing Async/Await

The *async/await syntax* is an alternate way of handling operations that don't happen instantaneously, like fetching data from a database or reading a file. Async/Await is [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) that makes the handling of asynchronous operations more straightforward and readable - in essence, "sweeter" for human use. The only downside is that you need to learn two new JavaScript keywords.

***`async`*** - When the `async` keyword is placed before a function declaration, it alerts javascript to the fact that there may be asynchronous operations that need to run synchronously (or line by line) in that function.

***`await`*** - The `await` operator is used to pause the execution of code until an asynchronous operation has completed. The `await` operator can only be used inside of an `async` function.

Check the docs on [**MDN - async and await**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await) for more information on the syntax and use of async and await.

### Anatomy of an `async` Function

```javascript
  const index = async () => {
    const data = await someDatabase.find();
    console.log(data);
  };
```
  - **Key Components**:
    - Use the `async` keyword right before the function declaration.
    - Inside an `async` function, use `await` to pause further execution until the asynchronous operation completes.

## Implementing `async/await` syntax

Let's replace the callback-based file reading structure with `async/await` for cleaner code:

```javascript
// app.js
const fs = require('node:fs/promises');

const example = async () => {
  const data = await fs.readFile('test.txt', 'utf8');
  console.log(data);
  const data2 = await fs.readFile('test2.txt', 'utf8');
  console.log(data2);
  const data3 = await fs.readFile('test3.txt', 'utf8');
  console.log(data3);
}

example();

console.log('run this as soon as possible');
```

Test the code:

```bash
node app.js
```

**What changed:**

- We created an `async` function named `example`. This is necessary because the `await` operator can only be used inside `async` functions.

- Inside `example()`, we use `await` before each `fs.readFile` call. This pauses execution of the function until each file reading is complete, allowing the code to run line-by-line in a readable manner, similar to synchronous code.

- With `await`, `fs.readFile` directly returns the contents of the file as a string. This allows us to assign the file's content to variables (`data`, `data2`, `data3`) without using callback functions.

- We've changed the `require` statement to `const fs = require('node:fs/promises');`. This imports the promise-based variant of Node's `fs` module, which is designed to work with `async/await` syntax, allowing for a more streamlined asynchronous code.


**Benefits**:
  - **Readable Code**: The use of `async` and `await` makes the code flow like synchronous code, improving readability.

  - **Avoids Callback Hell**: By using `await`, we avoid nesting and make our code look more like a series of synchronous operations.

So much better than using callbacks!