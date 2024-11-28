<h1>
  <span class="headline">Intro to Asynchronous Programming</span>
  <span class="subhead"><code>then()</code> and <code>catch()</code></span>
</h1>

**Learning objective:** By the end of this lesson, students will understand how to apply `then()` and `catch()` to asynchronous operations.

## What are `then()` and `catch()`?

In JavaScript, `then()` and `catch()` are methods used to handle asynchronous operations. They provide functionality similar to what you can achieve with `async`/`await` and `try...catch` blocks. In short, `then()` is used for handling the fulfillment of a promise, while `catch()` is used for handling any errors.

## `then()`

The `then()` method chains to the end of an asynchronous operation, like a `fetch` request. It accepts a callback function that is executed when the asynchronous operation completes. The callback function passed to the `then()` accepts the result of the promise as its input.

```javascript
// add a new endpoint
const commentsApiUrl = 'https://jsonplaceholder.typicode.com/comments/4';

fetch(commentsApiUrl)
  .then((response) => response.json())
  .then((data) => console.log(data));
```

In the code block above, we are chaining two instances of the `then()` method together.

Let's break down what is accomplished in each:

- **First callback:** The first instance of `then()` has a callback of `(response) => response.json()`. This function receives the response (`response`) from the `fetch` request. It then calls `response.json()` to convert the response body into a JavaScript object. This conversion is also an asynchronous operation, so `response.json()` returns another `Promise` object.
- **Second callback:** The second instance of `then()` waits for the `Promise` returned by `response.json()` to be resolved. It then executes its callback `(data) => console.log(data)`, which receives the data and logs it to the console.

Note how similar this looks to the equivalent code if we used `async`/`await` to accomplish the same task:

```javascript
const functionName = async (url) => {
  const response = await fetch(url);
  const data = await response.json();
  console.log(data);
};
```

`async`/`await` is typically preferred in modern code, as `then()` syntax is prone to callback hell and the pyramid of doom. However, recognizing `then()`/`catch()` syntax can be helpful when reading documentation or working with older code.

## `catch()`

The `catch()` method can be chained to the end of a `then()`. It accepts a callback function as an argument. This callback function is executed if an error occurs at any point in the chain and receives the error as an argument.

```javascript
fetch(commentsApiUrl)
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
```

Again, this is very similar to the functionality provided by `try...catch` blocks!
