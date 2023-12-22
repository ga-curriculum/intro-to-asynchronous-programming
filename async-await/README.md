# ![Intro to Asynchronous Programming - Async/Await](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how the async/await syntax applies to asynchronous operations in JavaScript.

## The problem with callbacks

Developers will often times nest several callback functions when dealing with asynchronous code. However, when callbacks need to call functions that also accept callbacks, it leads to deeply nested structures. This is also known as "callback hell" or the "pyramid of doom". The resulting code becomes hard to read and debug, as illustrated by the pyramid-like structure in the following example.

To set up the example, let's create a second file, similar to the `test.txt` file we created before. Put the following content in `test2.txt`:

```
hello 2!
```

Repeat the process again, with a `test3.txt` file:

```
hello 3!
```

Now let's update `example.js` to print the contents of both of these files, synchronously:

```javascript
const fs = require('node:fs');

fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
	fs.readFile('test2.txt', 'utf8', (err2, data2) => { 
		console.log(data2);
		fs.readFile('test3.txt', 'utf8', (err3, data3) => { 
			console.log(data3);
		});
	});
});

console.log('run this as soon a possible');
```

Can you see why this kind of structure has such negative names? To avoid this pattern, ES6 introduced *Async/Await*.

## What is Async/Await? 

*Async/Await syntax* is an alternate way of handling operations that don't happen instantaneously, like fetching data from a database or reading a file. Async/Await is [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) that makes the handling of asynchronous operations more straightforward and readable - in essence, "sweeter" for human use. The only downside is that you need to learn two new JavaScript keywords.

*`async`*
When the `async` keyword is placed before a function declaration, it alerts javascript to the fact that there may be asynchronous operations that need to run synchronously (i.e. line by line).

*`await`*
The `await` operator is used to pause the execution of code until an asynchronous operation has completed. The `await` operator can only be used inside an `async` function.

Check [**MDN - async and await**](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await) for more information on async and await. 

## Anatomy of an `async` function

Let's rewrite the previous file reading code using async/await:

```javascript
const fs = require('node:fs/promises');

const example = async () => {
	console.log('run this as soon a possible');
	const data = await fs.readFile('test.txt', 'utf8');
	console.log(data);
	const data2 = await fs.readFile('test2.txt', 'utf8');
	console.log(data2);
	const data3 = await fs.readFile('test3.txt', 'utf8');
	console.log(data3);
}

example();
```

So much better than using callbacks!  A couple of things to note:

- `const fs = require('node:fs/promises');` this is a slightly different NodeJS package that we're using which enables `async`/`await` syntax.
- We define and then invoke an `async` function called `example` because the lines marked with `await` need to occur inside `async` functions and can't occur in global scope.

Once Node has entered the invocation of `example()`, the flow of control runs in an easily readable manner from one line to the next without any need for callbacks. This is because we have added the `await` keyword in front of each `fs.readFile()` invocation. In addition, the `await` keyword allows `fs.readFile` to return the contents of the file as a string, rather than pass it into a callback function as an argument.nThis allows us to assign this information to the variable `data`.