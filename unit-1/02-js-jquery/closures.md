# Closures



#### What are closures?

Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). This is possible because in JavaScript, **functions have access to variables defined in their outer scope** (even if that scope is in a returned function, more on this later).

In other words, these functions 'remember' the environment in which they were created. Read this over and over again in your head to digest the definition of closure. 

#### Example of closures

```javascript
function init() { // function init creates an enclosing scope
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() { // displayName() is the inner function, a closure ( i am a closure )
    alert(name); // use variable declared in the parent function    
  }
  displayName();    
}
init();
```

`init()` creates a local variable name and then a function called `displayName()`. `displayName()` is an inner function that is defined inside `init()` and is only available within the body of that function. `displayName()` has no local variables of its own, however it has access to the variables of outer functions and so can use the variable name declared in the parent function.

**So function `init() {}` creates a closure, and function `displayName() {}` is the closure.
** Keep reading on :)

```javascript
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

If you run this code it will have exactly the same effect as the previous `init()` example: the string "Mozilla" will be displayed in a JavaScript alert box. What's different — and interesting — is that the `displayName()` inner function was returned from the outer function before being executed.

That the code still works may seem unintuitive. Normally, the local variables within a function only exist for the duration of that function's execution. Once `makeFunc()` has finished executing, it is reasonable to expect that the name variable will no longer be accessible. Since the code still works as expected, this is obviously not the case.

The solution to this puzzle is that **myFunc has become a closure. A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.** The environment consists of any local variables that were in-scope at the time that the closure was created. In this case, myFunc is a closure that incorporates both the displayName function and the "Mozilla" string that existed when the closure was created.

## More Readings

For more in-depth explanation of closures, check out these resources:

[Understanding Closures with Ease](http://javascriptissexy.com/understand-javascript-closures-with-ease/)

[MDN closure documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)