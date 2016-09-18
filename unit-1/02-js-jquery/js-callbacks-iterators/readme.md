#Functional Programming

Programming with functions! Weren't we already doing that? Well yes, but we can use functions more heavily, especially in place of loops.

Previously, we saw that functions can be assigned to variables. For example:

```js
var add = function(a, b) {
  return a + b
}

add(1, 2);
> 3
```

Functions are **first-class citizens** in JavaScript. This means that we can create functions, store them into variables, and pass functions into other functions. Functions are only executed when called. Try this to illustrate:

###Exercise

Try running the following. What is printed to the screen?

```js
var bag = function() {
  console.log('Hello, I am a bag');
}

console.log(bag);
```

We can take advantage of this behavior by defining **callback functions**. Callback functions are passed in and *called* at a specific time.
