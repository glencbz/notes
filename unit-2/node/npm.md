# npm and Node

### What is npm?

npm is two things:

- an online repository of node projects/modules
- a command line utility that aids in **package installation**, version management and dependency management

With npm, we have easy access to huge variety of resources that we can use for our Node projects! Most of the time, you'll be using the package management features of npm to download and manage Node modules.

To communicate with npm you need to create a special file, titled `package.json`. `package.json` tells Node that the current directory houses a Node project and provides information about your project. It must, at a minimum, have name and version properties defined within it:

```json
{
  "name": "my-app",
  "version": "0.0.1"
}
```

In time, we'll see all kinds of cool things we can do with `package.json`.

***note:***

The `name` property value should be in file-type syntax.

### Node Modules

Like most other modern languages, Node is modular. This means that we can write JS files (i.e. modules) that are meant to be reused in other files. Remember that on the front end, we used multiple JS files by naming the files in our HTML file. In Node, we don't have HTML, we `require` the files in our JS.

This is done in Node in two steps:

1. The module creates a variable called `module.exports` that contains everything it wants to share with other files
2. The file that wants to import the module calls the function `require()` on the module

For example, let's make two files: `touch my-module.js main.js`

```js
// my-module.js
var number = 7
module.exports.name = "Kenaniah"
module.exports.arr = [1, 2, 3]
module.exports.getNumber = function(){
    console.log("Get number called. Returning: ", number)
    return number
}

console.log("End of my-module.js file")
```


```js
// main.js

// here we're grabbing everything that's "exported" in our other file, and storing it a variable called 'my'

// note how this is a file path
var my = require('./my-module')

// Variables and such that were not exported aren't in scope
console.log("number is " + typeof number) // undefined

// Anything exported can be accessed on the object
console.log("Name is: ", my.name)

// Closures are still closures
console.log("The number is: " + my.getNumber())

// JavaScript is still JavaScript
console.log("The array contains " + my.arr.length + " elements")

// Let's see the module we imported
console.log(my)
```

Then try running:
```
node my-module.js
node main.js
```

#### Things to Note

A `module` isn't actually a global object, but rather, it is local to each module (i.e. the file it is being defined in). However, we can use the `exports` property on modules (`module.exports`) to specifically declare what from the module we want to be made available to other modules/files through the use of `require()`

> Note: The module's source file is only executed the first time that file is required.

## npm - "Node Package Manager"

Though, it's frequently referred to as a package manager, technically, the founders of Node are quite frank when they say: "[npm] is a recursive bacronymic abbreviation for 'npm is not an acronym'."  Read more [here](https://docs.npmjs.com/misc/faq#if-npm-is-an-acronym-why-is-it-never-capitalized).

Before we practice using npm, you should know a more: Node uses a package management system to distribute open-source modules. We can use the _Node Package Manager_ by running its command, `npm`.

`npm`  uses a file called `package.json`. This file provides a bunch of handy configurations that help make our life easier.

| Task                                     | Node.js           |
| ---------------------------------------- | ----------------- |
| Install a new module                     | `npm install ...` |
| Update modules                           | `npm update`      |
| Run the `start` command | `npm start` (provided start is defined in `package.json`) |                   |

You'll use this in a handful of lessons in the coming week. For now, let's focus on you making a quick module of your own!

### Independent Practice 

Partner up with your neighbor - your task is to make a module together (`car.js`) and that defines a car – with both properties and functions – and export it as a module to a `main.js` file.


In the `car.js` file:

Properties should include:
- color, convertible (boolean), speed (0, at first)

Functions specs:
- include accelerate and decelerate
  - these should take one argument, the speed, and add or subtract it the from the current speed
  - return a string with the old speed and new speed
- call these functions at the bottom of the file

In the `main.js` file, be sure to require the module and console log a message about your car object, including the current speed of the car.

## Conclusion

- What are some of the important distinguishing features of Node?
- Demonstrate how to run JS on your computer, both interactively and in a file
- Demonstrate how `module.exports` & `require` work



