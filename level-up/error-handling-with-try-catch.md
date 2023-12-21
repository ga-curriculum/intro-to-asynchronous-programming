# ![Intro to Asynchronous Programming - Error handling with `try...catch`](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to use `try...catch` blocks in JavaScript to handle errors in code effectively.

## What is a `try...catch` statement?
The try/catch statement provides a way to handle errors that may occur in a block of code, without stopping the execution of the entire script. 

**`try`**
- The `try` block is where you write the code that might throw an `error`. Think of it as a way of saying, "Attempt this operation, but know that it might fail."
- If any code within the `try` block throws an `error`, the execution immediately jumps to the `catch` block.

**`catch`**
- The `catch` block is executed if an error is thrown within the try block.
- It receives an `error` object that contains details about what went wrong, allowing you to handle the `error`, log it, or provide alternative logic.

Visit [MDN - try...catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) for more information on try and catch.

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
When it comes to asynchronous functions, `try...catch` can be incredibly useful for handling errors that stem from database queries or API calls. Take a look at the example below:

```javascript
async function index() {
  try {
    const response = await todoDB.find();
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

In this example, the `todoDB.find()` is an asynchronous operation placed inside our `try` block. If something goes wrong with that operation, it will return a new `error` with information about what went wrong. When that happens, the `catch` block will detect the `error` and handle it. In this case, our `catch` block simply prints the `error` to the console, but far more robust error handling could be included as well. This approach can help maintain a positive user experience by preventing crashes due to unhandled errors in asynchronous code.