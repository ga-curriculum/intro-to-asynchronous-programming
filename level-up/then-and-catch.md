# ![Intro to Asynchronous Programming - Level Up - `then()` and `catch()`](./assets/then-and-catch.png)

**Learning objective:** By the end of this lesson, students will understand how to apply `then()` and `catch()` to asynchronous operations.

In JavaScript, `then()` and `catch()` are methods used to handle asynchronous operations. They provide functionality similar to what you can achieve with `async/await` and `try...catch` blocks. In short, `then()` is used for handling the fulfillment of a promise, while `catch()` is used for handling the errors.

## `then()`

The `then()` method chains to the end of an asynchronous operation, like a `fetch` request. It accepts a callback function that is executed when the asynchronous operation completes. The callback function passed to the `then()` accepts the result of the promise as its input.

```javascript
fetch('https://jsonplaceholder.typicode.com/users/1')
  .then((res) => res.json())
  .then((data) => console.log(data));
```

In the code block above, we are chaining together two instances of the `then()` method. Let's breakdown what is accomplished in each:

- First callback: The first instance of `then()` has a callback of `(res) => res.json()`. This function receives the response (`res`) from the `fetch` request. It then calls `res.json()` to convert the response body into a JavaScript object. This conversion is also an asynchronous operation, so `res.json()` returns another yet another `Promise` object.

- Second callback: The second instance of `then()` waits for the `Promise` returned by `res.json()` to be resolved. It then executes its callback `(data) => console.log(data)`, which receives the data and logs it to the console.

## `catch()`

The `catch()` method can be chained to the end of a `then()`. It accepts a callback function as an argument. This callback function is executed if an error occurs at any point in the chain, and receives the error as an argument.

```javascript
fetch('https://jsonplaceholder.typicode.com/users/1')
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
```