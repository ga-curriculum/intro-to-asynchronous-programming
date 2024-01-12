# ![Intro to Asynchronous Programming - Callbacks](./assets/hero.png)

**Learning Objective:** By the end of this lesson, students will understand callback functions in relation to asynchronous JavaScript.

## Understanding callbacks in asynchronous JavaScript

A callback is a function passed into another function as an argument, so that it may be invoked at the appropriate time. Many JavaScript functions are designed to use callbacks, including browser event handling and asynchronous requests like reading files.

To demonstrate, we'll test reading a file with Node's `fs` module. 

### Demonstrating callbacks with file reading

#### Step 1: Create a test file

Create a file named `test.txt` in your project directory.
```bash
touch test.txt
```

Add sample text to `test.txt`:
```plaintext
hello!
```

#### Step 2: Read the file 

Add the following code to `app.js`:

```javascript
const fs = require('node:fs');

fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
});

console.log('run this as soon as possible');
```

>  `fs` is the Node.js file system module, allowing interaction with the file system. This code demonstrates asynchronous file reading, where `fs.readFile` is a non-blocking, asynchronous operation.

#### Step 3: Observe the asynchronous behavior

Run the code using:

```bash
node app.js
```

Notice the output order. The message `"run this as soon as possible"` appears before the `hello!` file content, illustrating an asynchronous execution of these two processes. 

### What is happening under the hood?

- Reading a file is a relatively **long process** for computers, even if it's a fraction of a second for us.

- We're trying to run the line `console.log('run this as soon a possible')` as quickly as the program can, but if we were to wait for the reading of the`test.txt` file to finish, it could take a while (at least for a computer).

- Reading the file *asynchronously* frees us up to move on to the line `console.log('run this as soon a possible')` while the file operation runs. Once the reading of the file is complete, we'll log the contents of the file with `console.log(data);`.

- When you run this code, you see the text `"run this as soon a possible"` first, followed by the contents of `test.txt`: hello! This demonstrates the non-blocking nature of asynchronous operations.

#### Understanding the asynchronous callback

Let's review the code:

 ```javascript
  fs.readFile('test.txt', 'utf8', (err, data) => { 
    console.log(data);
  });
 ```
In this code the first argument is the name of the file, the second is the [character set](https://en.wikipedia.org/wiki/UTF-8), and the callback `(err, data) => { console.log(data); }` is the asynchronous function. It's executed after `fs.readFile` *finishes* reading `test.txt`.