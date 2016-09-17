# Functions

## Objectives
* Define a function
* Define a function with a parameter
* Define a function that operates on two parameters
* Understand the difference between printing and returning
* Create functions with and without return values
* Recognize the scope of variables inside and outside functions

## Defining a function

A function is a module that can store and invoke code. When writing repetitive
code, we can isolate code into **functions** in order to reduce repetition. For
example, if we needed to say "Hello World" to the screen multiple times, we can
create a function like so.

```js
function greeting() {
	console.log("Hello World");
}

greeting();
```

We took the `console.log("Hello World")` code and put it in a function! This is then assigned to a variable called `greeting`. To use it, we take the variable name and append parentheses to the end of the function variable. This is known as **calling** the function.

**Parts of a function**

```
function FUNCTIONNAME(PARAMETERS) {
	//CODE
}
```

## Defining a function with a parameter

We can also create functions that accept **parameters**, and use those parameters as variables in the function.

```js
function greeting(taco) {
	// anything inside of here will execute when called
	console.log("Good morning", taco);
}

var name = "Josh"
var name2 = "Brian"
greeting(name);
// Good morning Josh
greeting(name2);
// Good morning Brian
```

##Defining a function with two parameters

Functions can have multiple parameters, separated by commas.

```js
function greeting(taco, stuff) {
	// anything inside of here will execute when called
	console.log("Good morning", stuff, taco);
	console.log("taco:", taco);
	console.log("stuff:", stuff);
}

var name = "Josh"
var name2 = "Brian"
greeting(name, name2);
greeting(name2, name);
```

## Returning

Note that functions can have **input** via parameters. They can also have **output** as return values. Returning values from a function is denoted by the keyword `return`. Also, return values are optional.

```js
function multiply(num1, num2) {
	console.log("inside the function");
	return num1 * num2
}

var firstNum = 2;
var secNum = 3;
var taco = multiply(firstNum,secNum);

console.log(firstNum + " multiplied by " + secNum + " is " + taco )
```

```js
// With a return value
function returnHello(name) {
	return("Hello, " + name)
}

console.log("with a return value:", returnHello("jane") );

// Without a return value
function returnHello2(name) {
	console.log("inside returnHello2: Hello, " + name);
}
returnHello2("nachos");
console.log("without a return value:", returnHello2("taco") ); //will show as undefined
```

Note that printing something to the screen using `console.log` is not the same as returning values. Returning a value is like "assigning a value" to the function call. This means that returned values can be used again in your code. Compare these two examples:

```js
//Expected behaviour
function multiply(num1, num2) {
	return num1 * num2;
}

console.log("2 * 3 =", multiply(2,3));
//2 * 3 = 6
```

```js
//Totally unexpected behaviour
function multiply(num1, num2) {
	console.log(num1 * num2);
}

console.log("2 * 3 =", multiply(2,3));
//6
//2 * 3 = undefined
```

## Declaring functions

There are two main ways to declare a function
```js
var multiply = function(a, b) {
	return a * b;
}

function multiply(a, b) {
	return a * b;
}
```

The main difference between these two is that the first one is defined at run-time, meaning that if we try to call the function before it's declared, an error will be thrown:
```js
multiply(2, 2); // ERROR

function multiply(a, b) {
	return a * b;
}
```

The second declaration is defined at parse-time, so we can call the function wherever we'd like.
```js
multiply(2, 2); // success

function multiply(a, b) {
	return a * b;
}
```

Despite being more flexible, the former declaration that assigns the function to a variable is more common when developing Node applications. You can read more about the difference [here](http://stackoverflow.com/questions/336859/var-functionname-function-vs-function-functionname)

## Anonymous functions

Anonymous functions are functions that are not stored to a variable. Here is an analog

```js
// this assigns the value 3 to three
var three = 3;

//this is just the value 3
3;

// these do the same thing
console.log(2 + three);
console.log(2 + 3);
```

Similarly

```js
//named function
var hi = function(){
	console.log('hi!');
}

//anonymous function
function(){
	console.log('hi!');
}

//these do the same thing
hi();
(function(){
	console.log('hi!');
})()
```

Anonymous functions look like a mess, but they are great for functions you only need once and will never use again. We'll see more of them when we review **callbacks**.

###Exercises

1. What is the return value of this function when called?

```js
function lightsabers(num) {
	console.log('I have ' + num + ' lightsabers.');
}

lightsabers(2);
```

2. How would the function above be modified if the user wanted to pass in an object of lightsabers, like this one?

```js
var myLightsaberCollection = {
	blue: 1,
	green: 3
}

function lightsabers(lightsaberCollection) {
	//code here
}

lightsabers(myLightsaberCollection);

// Output
// I have 1 blue lightsaber
// I have 3 green lightsabers
```
