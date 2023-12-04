# ![Intro to Asynchronous Programming - Concepts](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will have a basic understanding of asynchronous programming in JavaScript.

## What is asynchronous programming?

[Asynchronous programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing) is a way to make your program do tasks that might take a while, without stopping everything else. This means your program can still do other things while waiting for an *asynchronous* task to finish.

By default, JavaScript operates in a synchronous manner, where code is executed line by line in the order that it was written. This also means that each line of code must complete its execution before the next line can begin. If a particular task is time-consuming, it can cause a delay in the execution of subsequent lines of code.

In contrast, asynchronous programming breaks from that ordered sequence of execution. It allows for the initiation of a task that will complete sometime in the future, while the rest of the code continues to run. An asynchronous operation allows the program to handle other tasks, and then come back to the original task once it is ready.

> 📚  In programming, asynchronous refers to operations or events that don't occur in sequential order.
> 

## Why do we use asynchronous programming?

Asynchronous programming is especially useful for tasks that involve waiting. This usually involves scenarios where an application needs to wait for an external process, like fetching data from a website or reading a file. 

Unlike synchronous programming, where the entire application might freeze during such operations, asynchronous programming allows the rest of your application to remain active. This means your program can continue updating the user interface or responding to user inputs while waiting for the data or file.

By preventing the freezing of the application during lengthy operations, asynchronous programming significantly improves the overall user experience. Users are not left waiting for the application to respond, leading to a smoother and more interactive interface.

Many essential tools and operations in JavaScript are designed to function asynchronously. Operations like API calls or database queries being prime examples. Understanding how to work with asynchronous code will enable you to integrate these functionalities in your applications.

>💡 Understanding asynchronous programming is crucial in JavaScript, especially for operations like server requests, file reading, or any other task that takes time to complete. 
>