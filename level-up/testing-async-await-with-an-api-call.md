# ![Intro to Asynchronous Programming - Testing `async/await` with an API call](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to make fetch requests using `async/await` syntax.

## Defining the endpoint

First, let's define the API *endpoint* we will be using:

```javascript
const todosAPIUrl = 'https://jsonplaceholder.typicode.com/todos/'
```

>📚 In the context of an API call, an endpoint refers to a specific URL where you can access and interact information. It's essentially the address or entry point for a particular resource on the web.
>

In the next step, we'll create a function to make a `GET` request to this endpoint, with the goal of accessing the `todos` resource.

## Defining a fetch function
Add the following code to `app.js`:

```javascript
async function show(todoId) {
  try {
    const response = fetch(`${todosAPIUrl}${todoId}`);
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};

console.log("First");
show(1);
console.log("Third");
```

Let's break down this code together:

In this example, we are defining an `async` function called `show`. The `show` function accepts a `todoId` as an argument. The `show` function calls upon the `fetch` method, and prints the `response`.

The `fetch` method is making a request to a modified version of our `todosAPIUrl` endpoint. Notice how we are adding the `todoId` to the end of the URL. This results in a URL like the example below:

```plaintext
https://jsonplaceholder.typicode.com/todos/1
```

Finally, we are calling upon the `show` function and passing an argument of `1`. The number `1` in this scenario is our `todoId`, a unique identifier for a particular `todo` that we wish to retrieve.

>💡 Notice how we are logging the statements of `First` and `Third` before and after the invocation of `show`. These statements will help us track the asynchronous nature of our code.
>

## Pending promises
When we run our code, notice what we are getting as a `response`:

```plaintext
First
Promise { <pending> }
Third
```

Logging the `response` gives us an unresolved `Promise` object. This happens because `fetch` is asynchronous and returns a `Promise` immediately. Our request to the provided URL is working correctly, but the actual data is not yet available when we try to log it.

To view the actual information contained in the `response`, we'll need to modify our code with the `await` operator.

## Awaiting promises
We have already declared our function as asynchronous with the `async` keyword, so the only change we need to make is adding the `await` operator before the invocation of `fetch`.

Let's update the function with the `await` operator:

```javascript
async function show(todoId) {
  try {
    const response = await fetch(`${todosAPIUrl}${todoId}`);
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

Try running our updated code. Now, the `await` keyword tells JavaScript to pause execution at this point, and wait for the `Promise` to resolve. The response variable then holds the actual response from the API, not just a `Promise`.

>💡 After running the code, notice the order of the statements now being printed to your console.
>

## Extracting data with the `json()` method
Although we successfully `await` the response from the API, the `response` does not directly contain the data we need. At the moment, we are viewing an HTTP response, not the actual [*JSON data*](https://developer.mozilla.org/en-US/docs/Glossary/JSON). 

>📚 JSON, short for JavaScript Object Notation, is a format for storing and transporting data. It's often used when in API calls and closely resembles a JavaScript object.
> 

To access the JSON data, we can use the [*`json()`*](https://developer.mozilla.org/en-US/docs/Web/API/Response/json) method on our `response` object. This method is also asynchronous and initially returns a `Promise`, so we'll need to implement the `await` operator once more.

>📚 The `json()` method in JavaScript is used to convert the response body from a request into a JavaScript object. 
> 

Let's modify our code to utilize the `json()` method:
```javascript
async function show(todoId) {
  try {
    const response = await fetch(`${todosAPIUrl}${todoId}`);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log(error);
  }
};
```

Now when we run our code, our console should display something like the `data` object below:
```plaintext
{ userId: 1, id: 1, title: 'delectus aut autem', completed: false }
```