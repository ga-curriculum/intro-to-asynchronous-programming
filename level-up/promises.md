# ![Intro to Asynchronous Programming - Promises](./assets/promises.png)

**Learning Objective:** By the end of this lesson, students will have a comprehensive understanding of JavaScript promises and their application in managing asynchronous operations.

## Understanding JavaScript Promises

A **Promise** in JavaScript is a powerful and versatile object that represents the eventual completion (or failure) of an asynchronous operation. It's a central feature in modern JavaScript used for handling asynchronous tasks like API calls, file operations, or timers.

### Promise states

A promise can exist in one of three states:

1. **Pending**: The initial state of a promise. The operation has not completed yet.
2. **Fulfilled**: Indicates that the asynchronous operation was successful.
3. **Rejected**: Signifies that the operation failed or encountered an error.

### Key characteristics of Promises

- **They are immutable**: Once a promise settles (either fulfilled or rejected), its state is immutable. It can't switch from fulfilled to rejected or vice versa.
- **They are asynchronous**: Promises allow JavaScript to continue running other code while waiting for the asynchronous task to complete, enhancing efficiency.

## Handling Promises

In modern JavaScript, many built-in methods return promises, making it easier to work with asynchronous operations.

Common examples include:

- Node's `fs/promises` module
- fetching data from a web API using `fetch()`
- Interacting with databases

Promises in JavaScript can be consumed in various ways, including using `.then()` and `.catch()` for chaining asynchronous operations, `async/await` for more modern  readable and synchronous-style code, or employing `Promise.all()` for executing multiple promises concurrently and handling their results together.

> To ***consume a promise*** in JavaScript refers to the process of handling the eventual result (either fulfillment or rejection) of a promise.

### Example 1: Reading a file with `fs/promises`

The `fs/promises` module in Node.js offers a promise-based approach to file system operations, such as reading and writing files. Here's how you can read a file using this module:

```javascript
const fs = require('fs/promises');

async function readFileContents(filePath) {
  try {
    // The `fs.readFile()` method returns a promise
    const data = await fs.readFile(filePath, 'utf8');
    // This line is executed after the promise is resolved
    console.log('File content:', data);
  } catch (error) {
    // This block catches any errors from the promise
    console.error('Error reading file:', error);
  }
}

// Call the function with the path to the file
readFileContents('./example.txt');
```

### Example 2: Fetching data with `fetch()`

One typical use case is the `fetch()` method for making network requests. `fetch()` returns a promise, which resolves with the response of the request.

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json()) // The `fetch()` method returns a promise
  .then(data => {
    // This block is executed after the promise is resolved
    console.log(data);
  })
  .catch(error => {
    // This block catches any errors from the fetch operation
    console.error('Error fetching data:', error);
  });

```

### Example 3: Performing database operations

Many database libraries in JavaScript also use promises for operations like querying the database.

```javascript
database.query('SELECT * FROM users')
  .then(users => {
    // The `database.query()` method returns a promise
    console.log(users); // Executed after the promise is resolved
  })
  .catch(error => {
    // This block catches any errors from the database query
    console.error('Database query error:', error);
  });
```

> 💡 **Always handle errors**: Use `.catch()` or `try...catch` (with async/await) to handle errors in promises.

### Chaining Promises

Promises can be chained, allowing for sequential asynchronous operations where each subsequent operation starts when the previous one is completed.

```javascript
firstAsyncFunction()
  .then((result1) => secondAsyncFunction(result1))
  .then((result2) => thirdAsyncFunction(result2))
  .catch((error) => console.log(error));
```

## Creating a Promise from scratch

Promises are created using the `Promise` constructor, which takes a function as its argument. This function generally performs an asynchronous operation and calls either `resolve` (on successful completion) or `reject` (on failure).

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  if (/* operation successful */) {
    resolve('Success!');
  } else {
    reject('Failure.');
  }
});
```

### Handling the results

To handle the results of a promise, you can use the `.then()` and `.catch()` methods.

- **`.then()`**: Attaches a callback for the fulfillment of the promise.
- **`.catch()`**: Attaches a callback for the rejection or failure of the promise.

```javascript
myPromise
  .then((value) => {
    // Handle fulfillment
    console.log(value); // 'Success!'
  })
  .catch((error) => {
    // Handle rejection
    console.log(error); // 'Failure.'
  });
```
