# ![Intro to Asynchronous Programming - Concepts](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will have a basic understanding of asynchronous programming in JavaScript.

## What is asynchronous programming?

By default, JavaScript operates in a synchronous manner, where code is executed line by line in the order that it was written. This also means that each line of code must complete its execution before the next line can begin. If a particular task is time-consuming, it can cause a delay in the execution of subsequent lines of code.

[Asynchronous programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing) is a way to make your program preform tasks that might take a while, without blocking other tasks. 

Asynchronous programming allows for the initiation of a task that will complete sometime in the future, while the rest of the code continues to run. An asynchronous operation allows the program to handle other tasks, and then come back to the original task once it is ready.

> 📚  In programming, asynchronous refers to operations or events that don't occur in sequential order.
> 

tktk: Hunter, what do you think about an image here?  Maybe something like this: ![](https://2327111203-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-LA-UVvJIdbk5Kfk3bDs%2F-M4zU72YWwW2hSyXI5LY%2F-M4zVQZMwwMDTDL3Tzd9%2Fasync-programming.png?alt=media&token=7dfdb955-c7bb-4765-a137-89a099e5f411)

## Why do we use asynchronous programming?

Asynchronous programming is especially useful for tasks that involve waiting. This usually involves scenarios where an application needs to wait for an external process, like fetching data from a database or reading a file. 

Unlike synchronous programming, where the entire application might freeze during such operations, asynchronous programming allows the rest of your application to remain active. This means your program can continue updating the user interface or responding to user inputs while waiting for the data or file.

Asynchronous programming significantly improves the overall user experience by preventing the freezing of the application during lengthy operations. Users are not left waiting for the application to respond, leading to a smoother and more interactive interface.

You've most likely experienced asynchronous programming already, but you probably didn't realize it. Many applications like Facebook, Twitter, various blogs, and news media sites will load only a small amount of content initially, so that the user is able to quickly view and interact with the application. As the user scrolls down the page, additional content is loaded at the bottom, so that there is always something additional to look at below whatever the user is currently viewing. 

This kind of feature is called *infinite scroll*, and it's just one of many examples of asynchronous programming. If these applications had tried to load all the information as the page is loaded, the user would have to wait for a very long time. Instead, the page loads with a small amount of content and then begins adding additional content asynchronously as the user interacts with the application.

Many essential tools and operations in JavaScript are designed to function asynchronously - operations like reading files or database queries being prime examples. Understanding how to work with asynchronous code will enable you to integrate these functionalities in your applications.

>💡 Understanding asynchronous programming is crucial in JavaScript, especially for operations like server requests, file reading, or any other task that takes time to complete. 
>