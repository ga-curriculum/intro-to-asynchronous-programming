# ![Intro to Asynchronous Programming - Level Up - `Promise.all()`](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to use `Promise.all()` to handle multiple promises simultaneously.

## What is `Promise.all()`?

`Promise.all()` is a feature in JavaScript for handling multiple promises *at the same time*. It accepts an array of promises, and returns a single promise that resolves when all of the promises in the array have completed.

## Why use `Promise.all()`?

Imagine you have multiple API calls to make and you need all the results to proceed. Instead of waiting for each call to complete one after the other, you can use `Promise.all()` to make these calls in parallel. If any promise is rejected, `Promise.all()` immediately returns an error.

## Making API calls with `Promise.all()`

Let's get some practice implementing `Promise.all()`. First, let's add two new endpoints to our code:

```javascript
const todosAPIUrl = 'https://jsonplaceholder.typicode.com/todos/'

// New endpoints:
const postsAPIUrl = 'https://jsonplaceholder.typicode.com/posts/1'
const userAPIUrl = 'https://jsonplaceholder.typicode.com/users/1'
```

Next, define and call upon a function called `fetchMultiple` like the example below:

```javascript
async function fetchMultiple() {
  try {
    const promise1 = fetch(postsAPIUrl);
    const promise2 = fetch(userAPIUrl);
    const responses = await Promise.all([promise1, promise2]);
    console.log(responses)
  } catch (error) {
    console.log(error)
  }
}

fetchMultiple()
```

Notice how we are passing an array containing `promise1` and `promise2` to our `Promise.all()`. When we run our code, we should see an array containing two response objects.

## Extracting data with `Promise.all()`

How might we use `Promise.all()` to extract the data from our array of responses? As we saw earlier, `Promise.all()` can accept an array of promises as an argument. As a result, the JavaScript `map()` method will be useful here.

Let's modify our code with the following:

```javascript
async function fetchMultiple() {
  try {

    const promise1 = fetch(postsAPIUrl);
    const promise2 = fetch(userAPIUrl);
    const responses = await Promise.all([promise1, promise2]);

    const dataArr = await Promise.all(responses.map((res) => {
      return res.json();
    }));

    console.log(dataArr)
  } catch (error) {
    console.log(error)
  }
}

fetchMultiple()
```

If we run our code, we should see something like the following print to our console:

```javascript
[
  {
    id: 1,
    name: 'Leanne Graham',
    username: 'Bret',
    email: 'Sincere@april.biz',
    address: {
      street: 'Kulas Light',
      suite: 'Apt. 556',
      city: 'Gwenborough',
      zipcode: '92998-3874',
      geo: [Object]
    },
    phone: '1-770-736-8031 x56442',
    website: 'hildegard.org',
    company: {
      name: 'Romaguera-Crona',
      catchPhrase: 'Multi-layered client-server neural-net',
      bs: 'harness real-time e-markets'
    }
  },
  {
    userId: 1,
    id: 1,
    title: 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit',
    body: 'quia et suscipit\n' +
      'suscipit recusandae consequuntur expedita et cum\n' +
      'reprehenderit molestiae ut ut quas totam\n' +
      'nostrum rerum est autem sunt rem eveniet architecto'
  }
]
```