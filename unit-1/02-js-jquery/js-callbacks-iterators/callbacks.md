# Callbacks

### Objectives
*After this lesson, students will be able to:*

- Explain the concept of a 'callback' and how we can pass functions as arguments to other functions
- Pass a named function as a callback to another function
- Pass an anonymous function as a callback to another function
- Describe the difference between asynchronous and synchronous program execution, and why callbacks are important to asynchronous program flow (Bonus)


## Callbacks - Intro

Callback functions are derived from a programming paradigm known as **functional programming**. At a fundamental level, functional programming specifies the use of functions as arguments. 

Functional programming is often seen as an esoteric technique of specially trained master programmers. That said, many of functional programming's core concepts are useful and accessible!

#### What is a Callback/Higher-order Function?

A callback function, also known as a higher-order function, is a function that is passed to another function as a parameter. The callback function is then called (or executed) inside the other function. It's basically something that looks like this:

```js
function callbackFn(){
  // do some fancy work here
  //
}

function callingFn(cb){
  //do other fancy work here
  //
  
  // call the callback
  cb();
}
```

The use of callback functions is essentially a pattern, an established solution to a common problem. This is why coding with callback functions is also known as a callback pattern.

## Examples of Callbacks

Let's walk through a couple of examples of code that utilize callbacks:

Callbacks can be named functions:
```javascript
function loopyName(eachName, index){
  console.log(index + 1 + ". " + eachName);
};

var friends = ["Mike", "Stacy", "Andy", "Rick"];
friends.forEach(loopyName);
```

Callbacks are commonly anonymous functions:
```javascript
var friends = ["Mike", "Stacy", "Andy", "Rick"];
​
friends.forEach(function(eachName, index){
  console.log(index + 1 + ". " + eachName);
});
```

In both of these cases, we passed a function to the `forEach` method as a parameter. The only difference is that in the first case, we gave the function a name *before* passing it to `forEach`.

Callbacks are also extremely common when creating interactions on a web page.
```javascript
var element = document.getElementsByTagName("body")[0];

element.addEventListener("click", function(){
  console.log("Executed in the callback function.");
})
```

## How Callback Functions Work? Discussion

Functions are variables, we can pass them around, use them as return values and make use of them in other functions.  When we pass a callback function as an argument to another function, we are only **passing the function definition**.

In other words, when we pass the callback as a parameter, we are **not executing the function**. That is why we don't include parentheses `()` like we do when we are executing a function. The callback is “called back” (hence the name) at some specified point inside the outer function’s body.

#### Callback Functions Are Closures!

When a callback is executed inside the containing function’s body, it executes just as if the callback were defined in the containing function. This means the callback is a closure.

Closures have access to the containing function’s scope. Since the callback function is a closure, it can access the containing function’s variables, and even the variables from the global scope.


## Named Functions as Callbacks

It is a common pattern to use an anonymous function as a callback. However, you can use a named function, too!

Take this code, and past it into your text editor:

```javascript
// global variable​
var allUserData = [];

// generic logStuff function that prints to console​
function logStuff(userData) {
  if (typeof userData === "string") {
    console.log(userData);
  } else if (typeof userData === "object") {
    for (var item in userData) {
      console.log(item + ": " + userData[item]);
    }
  }
}

// A function that takes two parameters, the last one a callback function
function getInput(options, callback) {
  allUserData.push(options);
  callback(options);
}
```


When we call the `getInput` function, we pass `logStuff` as a parameter - `​logStuff` will called back (or executed) inside the getInput function​

```javascript
getInput({name:"Alex", speciality:"JavaScript"}, logStuff);
```


Since the callback function is just a normal function when it is executed, we can pass parameters to it!

We can pass any of the containing function’s properties (or global properties) as parameters to the callback function.

By the way, you can always check a callback is a function before executing it:

```javascript
if (typeof callback === "function") {
  callback(options);
}
```

## `this` and Callbacks Problems

When the callback function is a method that uses the `this` object, we have to modify how we execute the callback function to preserve the `this` object context.

Let's define an object with some properties and a method​. We will later pass the method as a callback function to another function​:

```javascript
var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object​
  setUserName: function(firstName, lastName)  {
    // this refers to the fullName property in this object​
    this.fullName = firstName + " " + lastName;
  }
}

function getUserInput(firstName, lastName, callback) {
  callback(firstName, lastName);
}

getUserInput("Barack", "Obama", clientData.setUserName);

console.log (clientData.fullName);
//=> Not Set

console.log (window.fullName);
//=> Barack Obama
```

Since `getUserInput` is a global function, `this` points to the window object.

#### Use the `call` or `apply` Function To Preserve `this`

We can fix the preceding problem by using the `call` or `apply` function.

Every function in JavaScript has two methods: `call` and `apply`. These methods are used to set the this object inside the function and to pass arguments to the functions. You can read more about `call` and `apply` in the chapter on **Inheritance**.

- [`call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) takes the value to be used as the `this` object inside the function as the **first parameter**. The remaining arguments (separated by commas) are passed to the function.

- [`apply`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) takes only two parameters. The first parameter is also the value to be used as the `this` object inside the function. The second parameter is an array of values (or the arguments object) to pass to the function.

Let's walk through an example by defining another object with properties and a method and pass the method as a callback later:

```javascript
var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object​
  setUserName: function (firstName, lastName)  {
    // this refers to the fullName property in this object​
    this.fullName = firstName + " " + lastName;
  }
}

function getUserInput(firstName, lastName, callback, callbackObj)  {
  // The use of the Apply function below will set the this object to be callbackObj​
  callback.apply(callbackObj, [firstName, lastName]);
}
getUserInput("Barack", "Obama", clientData.setUserName, clientData);

console.log(clientData.fullName);
//=> Barack Obama
```

## Conclusion
- Describe callbacks, at a high level.
- Explain why you don't pass callbacks as parameters with parenthesis.