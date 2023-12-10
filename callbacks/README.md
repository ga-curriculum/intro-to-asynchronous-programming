# ![Intro to Asynchronous Programming - Callbacks](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand callback functions in relation to asynchronous JavaScript.

## Callbacks in asynchronous JavaScript

A callback is a function passed into another function as an argument, so that it may be invoked at the appropriate time. Many JavaScript functions are designed to use callbacks, including browser event handling, and asynchronous requests like reading files.

As an example, create a file `test.txt` with the following contents:

```
hello!
```

Now, in the same directory as `test.txt` create a file `example.js` with the following contents:

```javascript
const fs = require('node:fs');

fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
});

console.log('run this as soon a possible');
```

Run the code with:

```
node example.js
```

Reading a file takes a relatively long time for computers to do, even if it's a fraction of a second for us.  We're trying to run the line `console.log('run this as soon a possible')` as quickly as the program can, but if we were to wait for the reading of the file to finish, it could take a while (at least for a computer).  Instead what we do is have the process of reading a file run asynchronously and then move onto the line `console.log('run this as soon a possible')` while the file operation runs.  Once the reading of the file is complete, we'll log the contents of the file with `console.log(data);`.  If you were to run this code, you would see the text "run this as soon a possible" first, followed by the contents of test.txt: hello!

tktk: Hunter perhaps a diagram again like below, but showing the above example.  The left panel waits for the file read, followed by `console.log('run this as soon a possible');`, and the right panel shows them running in parallel:

![](https://2327111203-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LA-UVvJIdbk5Kfk3bDs%2F-M4zU72YWwW2hSyXI5LY%2F-M4zVQZMwwMDTDL3Tzd9%2Fasync-programming.png?alt=media&token=7dfdb955-c7bb-4765-a137-89a099e5f411)

The important thing to note from the above example is the following code:

```javascript
fs.readFile('test.txt', 'utf8', (err, data) => { 
	console.log(data);
});
```

Here, we pass an anonymous function definition into `fs.readFile` as the third argument (the first argument is the name of the file, and the second is the [character set](https://en.wikipedia.org/wiki/UTF-8)).  Once `fs.readFile` has completed reading the file `test.txt`, it will execute this anonymous callback function.