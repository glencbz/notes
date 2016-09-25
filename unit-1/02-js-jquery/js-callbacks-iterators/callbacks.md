# Callbacks

### Objectives
*After this lesson, students will be able to:*

- Explain the concept of a 'callback' and how we can pass functions as arguments to other functions
- Pass a named function as a callback to another function
- Pass an anonymous function as a callback to another function
- Describe the difference between asynchronous and synchronous program execution, and why callbacks are important to asynchronous program flow (Bonus)


### An Introduction to callbacks

Callback functions are derived from a programming paradigm known as **functional programming**. At a fundamental level, functional programming specifies the use of functions as arguments. 

Functional programming is often seen as an esoteric technique of specially trained master programmers. That said, many of functional programming's core concepts are useful and accessible!

#### What is a Callback?

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



### Why use callbacks?

Most of our programming is synchronous, that is, our code is executed line after line in a nice, synchronised manner. However, many programs need to be asynchronous. For example, we might want to execute some code if a user clicks on a button. However, we have no control over when the user will click; it could be 1s, 10s, or maybe even 1 hour later.  We have to prepare some code to be executed at a later time.

Callbacks are the way that most JavaScript implements asynchronous programming. We put the code we want in our callback, and when the time comes, the callback will be "called back" to do the work we want.

## Examples of Callbacks


One of the most common uses of callbacks on the web is to create interactions on a webpage.
```javascript
var element = document.getElementById("sample-id");

element.addEventListener("click", function(){
  console.log("Called the callback!");
})
```

We've actually done this before in DOM Manipulation! This is a callback because we're creating a function that gets called sometime in the future.

We can also do this with a named function:
```javascript
var element = document.getElementById("sample-id");
var cb = function(){
  console.log("Called the callback!");
}

element.addEventListener("click", cb)
```

Callbacks also let us do some cool things with arrays and iterators (more on this in iterators)

```javascript
var friends = ["Mike", "Stacy", "Andy", "Rick"];

friends.forEach(function(eachName, index){
  console.log(index + 1 + ". " + eachName);
});

// => 1. Mike
// => 2. Stacy
// => 3. Andy
// => 4. Rick
```

### How do Callback Functions Work?

Functions are variables, we can pass them around, use them as return values and make use of them in other functions.  When we pass a callback function as an argument to another function, we are only **passing the function definition**.

In other words, when we pass the callback as a parameter, we are **not executing the function**. That is why we don't include parentheses `()` like we do when we are executing a function. The callback is “called back” (hence the name) at some specified point inside the outer function’s body.

In fact, callback functions are a great example of closures! When a callback is executed inside the containing function’s body, it executes just as if the callback were defined in the containing function. This means the callback is a closure.

Closures have access to the containing function’s scope. Since the callback function is a closure, it can access the containing function’s variables, and even the variables from the global scope.
