# ![Intro to Asynchronous Programming - Level Up - Intro to the Fetch API](./assets/intro-to-the-fetch-api.png)

**Learning Objective:** By the end of this lesson, students will understand the basics of the Fetch API in JavaScript.

## What is the Fetch API?

The [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) is a tool for making network requests in JavaScript. It facilitates communication between an application and a server, allowing the application to either send or receive data. Think of it as a messenger that can move data between your application and other places on the internet. 

The primary function provided by the Fetch API is the [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch) method. It is used to make network requests. The `fetch()` method accepts a URL as an argument, and returns a Promise that resolves to a response. The `fetch()` method also accepts an optional options object that can be used to specify the HTTP method of the request. If no HTTP method is specified, the default GET request is used.

## Anatomy of `fetch` request

The `fetch()` method takes two parameters:

```javascript
fetch(URL, options)
```

- A URL to the resource you want
- An optional options object

Let's take a look at how a fetch request is constructed:

```javascript
const fetchData = async (url) => {
  const response = await fetch(url);
  const data = await response.json();
}
```

- We define an asynchronous function called `fetchData` that accepts a URL as an argument.
- Inside the function, we use `fetch` to make a GET request to the specified URL. Since `fetch` is asynchronous, we use `await` to pause the execution until the request completes and returns a response.
- Next, the response is converted into a JavaScript object using the [`json()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/json) method. This step is also asynchronous, so once again we use the `await` operator.
- Finally, the fetched data is logged to the console.

> 📚 The `.json()` method in JavaScript is used to convert a response from a network request into a JavaScript object. It's typically applied to the response object returned by the Fetch API to handle JSON data sent from the server.

## The options object

The [options object](https://developer.mozilla.org/en-US/docs/Web/API/fetch#options) allows you to apply various settings to a request made with the fetch method. Some of the most common properties for the options object include:

- [`method`](https://developer.mozilla.org/en-US/docs/Web/API/fetch#method)
The `method` property is used to specify the HTTP method (`GET`, `POST`, `PUT`, `DELETE`, etc.) of the request. 

    ```javascript
    fetch(url, { method: 'POST' })
    ```

-  [`headers`](https://developer.mozilla.org/en-US/docs/Web/API/fetch#headers)

    The `headers` property is used to set *HTTP headers* for the request. HTTP headers can be used to include additional information about the request, such as the type of data being submitted.

    ```javascript
    fetch(url, { headers: { 'Content-Type': 'application/json' }})
    ```

-  [`body`](https://developer.mozilla.org/en-US/docs/Web/API/fetch#body)

    The `body` property can be used to include any data, like information entered into a form, along with the request. 

    ```javascript
    fetch(url, { 
      method: 'POST',
      body: JSON.stringify({ greeting: 'Hello World!' })
    })
    ```

    > 💡 In the example above, the [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) method is used to convert the JavaScript object into a `JSON` string.

- [`mode`](https://developer.mozilla.org/en-US/docs/Web/API/fetch#mode)

  Specifies the mode of the request, such as `cors`, `no-cors`, or `same-origin`. It's important for handling [cross-origin requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

  > 📚  Cross-origin requests happen when a website tries to access resources from an outside source on the web. Normally, browsers block these requests for security reasons, but they can be conducted safely using the CORS (Cross-Origin Resource Sharing) mechanism. 

