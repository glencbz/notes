# Variable Scope and Hoisting

### Variable Scope

A variable's scope refers to the **context** in which the variable **exists**. We've already been using terms like local variable and global variable with some understanding of this principle, but let's take a closer look.

Scoping is important because it allows us to separate our code cleanly. Whenever we create a variable (including functions!), we have to give a name that we can use later on. It might be handy for all variables to be accessible everywhere, but there's a danger - there's no guarantee that our names will be unique throughout *ALL* of the JavaScript code that we're going to use. This means that some of our code might accidentally interfere with other parts of the code. We need to limit where we allow our variables to live.

In JavaScript, we have two kinds of scope, global and local. Globally scoped variable (or global variables) are available everywhere. Local scope is the kind of limited context that we've dicussed previously. A local scope is created **only** when we declare a new variable using `var` in a **function**. If it's outside the function, it's global:

```js
var globalVariable = "I'm outside"
    
function firstFunction(){
  var localVariable = "I'm inside";
}

function secondFunction(){
  console.log(globalVariable);
  console.log(localVariable);
}

firstFunction()
secondFunction();

// => I'm outside
// => undefined
```

This is because `var` designates that we want a new variable, and since we're in a function, our variable is created inside that function and isn't accessible anywhere else.

But, if we omit the `var`, JavaScript assumes we're trying to reference an existing variable, leading to problems like this:

```js
function firstFunction(){
  notLocalVariable = "I'm not inside?";
}

function secondFunction(){
  console.log(notLocalVariable);
}

firstFunction();
secondFunction();

// => I'm outside
// => Uncaught ReferenceError: localVariable is not defined
```
Local scope also has precedence over global scope. This protects us from using the same name twice if one of the names is in a local scope. 

```js
var localOrGlobal = 'global';

function myContext(){
  var localOrGlobal = 'local';
  console.log(localOrGlobal);
}

myContext();
// => local

console.log(localOrGlobal);
// => global
```

Most of the time, we're going to want to use local variables. Global variables are dangerous precisely because they're available everywhere. That makes them easy to reference, but that means that you might be making changes to the variables from *anywhere* in the code. In the long run, this tends to lead to bugs that are hard to track down. Avoid them if possible!

### Hoisting

In most languages, you have to declare a variable or function before you first reference it. This is **not** the case in JavaScript and can lead to very confusing and messy behaviour sometimes. In JavaScript, declarations are "hoisted" to the top of their enclosing scope. This is why it is **good practice to put all declarations at the top of the scope**, that way your code is written matches the way your code actually runs.

However, hoisting works a bit differently for functions and variables.

#### Function Hoisting

Function definitions are hoisted along with the declaration. This means that these two examples are equivalent:

Code that works because of hoisting
```js
callsLaterFunction()
// => Wow!
// This is an error in most languages!

function callsLaterFunction(){
  laterFunction();
}

function laterFunction(){
  console.log("Wow!")
}
```
Code that works regardless of hoisting
```js
// This is how most code is structured
function laterFunction(){
  console.log("Wow!")
}

function callsLaterFunction(){
  laterFunction();
}

callsLaterFunction()
```

#### Variable Hoisting

Variable definitions are hoisted, but **not assignments**. Let's see the example below:

```js
console.log(myVar);
// => undefined
var myVar = 3;

console.log(myVar);
// => 3
```

This is because only the definition is hoisted. Which means that our code translates to this:

```js
// CORRECT EXAMPLE
var myVar;
console.log(myVar);
// => undefined
myVar = 3;

console.log(myVar);
// => 3
```

and **not** this (this would happen if assignment were also hoisted):

```js
// WRONG EXAMPLE
var myVar = 3;
console.log(myVar);
// => 3
console.log(myVar);
// => 3
```

Because of this, the way you declare a function actually affects how your code runs. Remember that we can declare a function using a statement like `var myFunction = function(){}`? Variable assignments are not hoisted, which means this code (modified from before) will fail:

```js
callsLaterFunction()
// ERRORRRRRRRRRRRRRRRR

var callsLaterFunction = function (){
  laterFunction();
}

var laterFunction = function (){
  console.log("Wow!")
}
```

That is why it is best not to rely on hoisting to make our code work, but to structure everything in a clean, readable manner.

### Extra Reading

[JavaScript is Sexy](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/) on hoisting
