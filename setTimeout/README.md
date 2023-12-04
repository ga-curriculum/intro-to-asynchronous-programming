# ![Intro to Asynchronous Programming - `setTimeout`](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to utilize the `setTimeout()` method in JavaScript.

## What is the `setTimeout()` method?
A great example of asynchronous code in JavaScript is the global [`setTimeout()`](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout) method. The `setTimeout()` method is designed to create a timer that runs a block of code when the timer runs out. The `setTimeout()` method is asynchronous, in that it breaks from the ordered execution of code, and does not block the execution of later lines of code.

### Anatomy of `setTimeout()`
Calling upon the `setTimeout()` method requires the following two arguments:

```javascript
setTimeout(callback, delay);
```

1. `callback` - This is the reference to the function that `setTimeout()` will execute after the specified delay. It can be either a named function or an anonymous function.

2. `delay` - This specifies the time to wait before executing the `callback`, measured in milliseconds. For example, a delay of 1000 milliseconds equates to 1 second.

### Optional arguments
The `setTimeout()` method can also accept a series of optional arguments. These arguments are passed to the `callback` when it is executed.

```javascript
setTimeout((message) => {
   console.log(message);
}, 2000, 'Hello World!');
```

In the example above, the callback function defines a parameter named `message`. `setTimeout()` is given the string `'Hello World!'` as an optional argument. After the 2000-millisecond delay, this string is passed to the callback function, resulting in `'Hello World!'` being logged to the console.

## Understanding the asynchronous nature of `setTimeout()`
By default, JavaScript operates in a synchronous manner, meaning code is executed sequentially. This means each line must complete its task before the next line begins execution.

For instance, in the following synchronous code, each `console.log` statement prints out in the order they are written:
```javascript
console.log("First");
console.log("Second");
console.log("Third");
```

However, introducing `setTimeout()` changes this behavior:
```javascript
console.log("First");

setTimeout(() => {
  console.log("Second");
}, 1000);

console.log("Third");
```

When the `setTimeout()` function is called, it schedules the `"Second"` message to print after a 1-second delay. However, this delay doesn't stop the rest of the code from running. That is why `"Third"` is printed immediately after `"First"`, without waiting for the 1-second delay. 