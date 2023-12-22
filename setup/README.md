# ![Intro to Asynchronous Programming - Setup](./assets/hero.png)

## Setup

Open your Terminal application and navigate to your **`~/code/ga/lectures`** directory:

```bash
cd ~/code/ga/lectures
```

Make a new directory called **`intro-to-asynchronous-programming`**, then enter this directory:

```bash
mkdir intro-to-asynchronous-programming
cd intro-to-asynchronous-programming
```

Then, create an **`app.js`** and an **`index.html`** file. These files will hold your work for this lecture:

```bash
touch app.js index.html
```

With the files created, open the contents of the directory in VSCode:

```bash
code .
```

Open the `index.html` file and add HTML boilerplate by typing `!` and then hitting the `Tab` key. Then make use of the **`app.js`** file by adding this line inside the `<head>` tag:

```html
<script defer src="./app.js"></script>
```

With this setup complete, we'll have two methods at our disposal for executing the code we write in **`app.js`**:

- Open the **`index.html`** file in your browser and access the console output in your browser's dev tools.
- Use `node` to execute the **`app.js`** file directly by using this command in your terminal:
  
```bash
node app.js
```

While either method is acceptable, you should use the same method as your instructor for simplicity.