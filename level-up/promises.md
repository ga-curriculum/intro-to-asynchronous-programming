# ![Intro to Asynchronous Programming - Promises](./assets/promises.png)

**Learning objective:** By the end of this lesson, students will be able to understand and use JavaScript promises for managing asynchronous operations.

## What is a Promise?

A **promise** is a special JavaScript object. It represents the eventual completion, or failure, of an asynchronous operation.

A *promise* is always in one of three states:

- `pending`: Initial state, neither fulfilled nor rejected.
- `fulfilled`: The async operation was completed successfully.
- `rejected`: The async operation failed.

Once a *promise* has been *settled*, i.e., it's either fulfilled or rejected, its state will not change again.