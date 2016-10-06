# Intro to Node.js

### Objectives
- Explain what Node.js is & why it exists
- Use `module.exports` and `require` to organize code

## What is Node.js?

The makers of Node.js took JavaScript (which normally only runs in the browser) and made it available in your computer (on the server side). They took Google's V8 JavaScript Engine and gave it the ability to compile JS programs into machine code.

Keep in mind, Node.js is strictly a tool to run JavaScript on a server. While it's possible to build web applications and APIs in regular Node.js, we'll actually be using a Node framework - Express - to simplify the process. 

#### Why are people excited about Node?

It's new and hot in the industry but why does it matter?

A lot of developers and companies are excited because it allows you to build fast, scalable APIs and sites in JavaScript. We're _familiar_ with JS and being able to use it on the backend gives us the option to use a single programming language throughout an entire full-stack application.

#### Node is Asynchronous

On top of that, one of the big differences is that Node.js is designed to be _event-driven_ and _asynchronous_. While earlier frameworks can only do one thing at a time, Node purposefully sends nearly everything to the background and keeps going.

Imagine a paper delivery boy riding on his bike delivering papers every morning. Imagine he stops at each house, throws the paper on your doorstep, and waits to make sure you come out & pick it up before moving on to the next house. That would be what we'd call _blocking_ – each line of code finishes before moving on to the next line of code.

Now imagine the paperboy throwing the newspaper on your porch but never stopping his bicycle; never stopping, he just keeps throwing papers on porches, so that by the time you pick it up he'll be 3 or 4 houses down. That would be _non-blocking input/output (I/O)_, or _asynchronous_. This is an extremely awesome ability of node since I/O tends to be very "expensive."

#### Installing Node.js

To check if we already have Node installed, type: ``node -v`` in terminal. You will see the Node version if it's installed.

If it's not installed, you can install from the Node.js website, or better yet, use Homebrew like this:

```bash
brew install node
```

One of the advantages of using Homebrew is that you can update your versions easily like this:

```bash
brew upgrade node
```

This will install both Node.js and npm. We will introduce npm in greater depth later on.

## Exercise: Working with Node 

Before we go further, you should test your Node installation. We'll write some basic JS and runit with Node. There are two ways to do this – try them both.

#### Interactive Node

If you simply type node in terminal, you will launch Node's REPL (Read-Eval-Print-Loop) interactive utility. This is kind of like the console in Chrome Dev Tools. Let's test it:

```js
node

> 10 + 5
// 15

> var a = [ 1, 2, 3];
// undefined

> a.forEach(function(v) {
... console.log(v);
... });
// 1
// 2
// 3

> var http = require('http');
// undefined

> http
// [ a massive 'http' object returned from the 'http' module ]
```

Press control-c twice to exit REPL.

#### Executing a JS program

Write and execute some code in a file! In your working directory:

```bash
mkdir first-node
cd first-node
touch main.js
echo "console.log('hello world!');" >> main.js
node main.js
# hello world!
```

This is kind of like writing JS files before, but instead of putting them in an HTML document, we can run them straight from the command line!



### Extra Readings

[What asynchronous programming in Node is about](https://www.youtube.com/watch?v=8aGhZQkoFbQ)