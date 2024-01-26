# ![Intro to Asynchronous Programming - Error handling with `try...catch`](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to use `try...catch` blocks in JavaScript to handle errors in code effectively.

## What is a `try...catch` statement?

The try/catch statement provides a way to handle errors that may occur in a block of code, without stopping the execution of the entire script. 

**`try` {**

- The `try` block is where you write the code that might throw an `error`. Think of it as a way of saying, "Attempt this operation, expecting it might fail."

- If any code within the `try` block throws an `error`, the execution immediately jumps to the `catch` block.

**} `catch` {**

- The `catch` block is executed if an error is thrown within the try block.

- It receives an `error` object that contains details about what went wrong, allowing you to handle the `error`, log it, or provide alternative logic.

**` } `**

Visit [MDN - try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) for more information on the syntax and use of try and catch.

## Anatomy of a `try...catch`

Let's take a moment to get a sense of how to structure a `try...catch` block.

```javascript
try {
  // Code that could potentially throw an error
} catch (error) {
  // Code to handle that error
}
```

In this structure, the `try` block can contain any code that might throw an `error` when executing. When an `error` is thrown in the `try` block, it is caught and handled by the `catch` block, allowing an application to continue running.

## Using `try...catch` in asynchronous functions

Asynchronous functions often involve operations like database queries or API calls, where errors might occur. The `try...catch` structure is essential for effectively handling these errors.

Take a look at the example below:

```javascript
const index = async () => {
  try {
    // Asynchronous operation
    const data = await myDatabase.find();
    console.log(data);
  } catch (error) {
    // Error handling
    console.log(error);
  }
};
```

- The asynchronous operation `myDatabase.find()` is placed inside the `try` block. If an error occurs during this operation, it will return a new `error` with information about what went wrong.

- The `catch` block captures any thrown `error`. In this case, our `catch` block simply prints the `error` to the console, but far more robust error handling could be included as well.

- Using `try...catch` in asynchronous functions can can help maintain a positive experience for both developers and end users by preventing crashes due to unhandled errors in asynchronous code.
