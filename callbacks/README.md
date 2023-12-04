# ![Intro to Asynchronous Programming - Callbacks](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand callback functions in relation to asynchronous JavaScript.

## Callbacks in asynchronous JavaScript
A callback is a function passed into another function, so that it may be called upon at the appropriate time. In the past, this pattern was commonly used in JavaScript to handle asynchronous operations. Many JavaScript functions are designed to use callbacks, including event handling, and asynchronous requests.

In the example below, we can see a callback function being used to facilitate a hypothetical database query:

```javascript
todoDB.find(function(err, result) {
  if (err) {
    console.error('Error fetching data:', err);
    return;
  }
  console.log('To-do items:', result);
});
```

In this scenario:
- `todoDB.find` is a function that queries our database.
- The `todoDB.find` function accepts a callback as an argument. This callback gets executed once the database operation is complete.
- callback function defines two parameters: `err`, which handles any potential errors, and `result`, representing the data retrieved from the database.
- If there is an error (`err` is not `null`), it logs the error; otherwise, it logs the fetched results.

## The problem with callbacks
Developers will often times nest several callback functions when dealing with asynchronous code. However, when callbacks need to call functions that also accept callbacks, it leads to deeply nested structures. This is also known as "callback hell" or the "pyramid of doom". The resulting code becomes hard to read and debug, as illustrated by the pyramid-like structure in the code below.

```javascript
function loadApplication() {
  request('/api/customers', function (response) {
    const customerId = response.customers[0];
    request(`/api/customers/${customerId}`, function (response) {
      const photoId = response.customer.photoId;
      request(`/api/photos/${photoId}`, function (response) {
        console.log('Callback Hell');
      });
    });
  });
}
```

To avoid this pattern, ES6 introduced *promises*. Promises simplify asynchronous programming by replacing nested callbacks with a more straightforward and manageable structure. They make the code cleaner and easier to read, helping you handle tasks that take time, like loading data, in a more organized way. Today, promises are a key part of modern JavaScript for managing these asynchronous operations efficiently.

> 📚  A [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is a special JavaScript object. It represents the eventual completion, or failure, of an asynchronous operation. 
> 