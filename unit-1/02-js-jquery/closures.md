# Closures

Closures are functions that refer to independent (free) variables (variables that are used locally, but defined in an enclosing scope). This is possible because in JavaScript, **functions have access to variables defined in their outer scope** (even if that scope is in a returned function, more on this later).

In other words, these functions 'remember' the environment in which they were created. Read this over and over again in your head to digest the definition of closure. 

#### Example of closures

```javascript
function init() { // function init creates an enclosing scope
  var name = "Mozilla"; // name is a local variable created by init
  
  // displayName() is the inner function, a closure ( i am a closure )
  function displayName() {
    alert(name); // use variable declared in the parent function    
  }
  displayName();    
}
init();
```

`init` creates a local variable name and then a function called `displayName`. `displayName` is an inner function that is defined inside `init` and is only available within the body of that function. `displayName` has no local variables of its own. However `displayName` has access to the `name` variable defined in `init`. We say that  `init` creates a closure, and function `displayName` is the closure.



While the example is rather straightforward, this example might surprise those of you that come from other languages.

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

If you run this code it will have exactly the same effect as before. What's different — and interesting — is that the `displayName` inner function was returned from the outer function before being executed. Normally, the local variables within a function only exist for the duration of that function's execution. 

If this wasn't JavaScript, once `makeFunc` has finished executing, it is reasonable to expect that the name variable will no longer be accessible. Since the code still works as expected, this is obviously not the case.

The solution to this puzzle is that `myFunc` has become a closure. A closure is a special kind of object that combines two things: **a function, and the environment in which that function was created.** The environment consists of any local variables that were in-scope at the time that the closure was created. In this case, `myFunc` is a closure that incorporates both the `displayName` function and the "Mozilla" string that existed when the closure was created.

This behaviour is actually what makes JavaScript work the way it does! We can also use closures in more creative ways (like 'hiding' variables in objects). We'll see more of this in Object Oriented Programming.

## More Readings

For more in-depth explanation of closures, check out these resources:

[Understanding Closures with Ease](http://javascriptissexy.com/understand-javascript-closures-with-ease/)

[MDN closure documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)