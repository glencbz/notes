# Conditional Statements

#### `if`

The **if statement** executes some code if a specified condition is true.

```js
if (true) {
  console.log("this will be printed");
}

if (false) {
  console.log("this will not be printed");
}

var x = 4;
//var x = 5;
if (x === 5) {
  console.log("x equals 5");
}
```

#### `if/else`

When we want code that executes when the **if statement** condition is false, we can use the **else** keyword as a shorthand.

```js
var isTasty;
var food = "vegetables";
//var food = "pizza";
if (food === "pizza") {
  isTasty = true;
} else {
  isTasty = false;
}
console.log("Is the food tasty?", isTasty);
```

#### `if/else if/else`

```js
var course = "wdi";
if (course === "uxdi") {
  console.log("Hello, User Experience Designer!");
} else if (course === "fewd") {
  console.log("Hello, Front-End Developer");
} else if (course === "wdi") {
  console.log("Hello, Immersed Developer")
} else {
  console.log("Who are you?")
}
```

#### `switch`

Sometimes, numerous **if/else** statements make code hard to read. There's an alternative called a **switch statement**. It accepts a value and compares the value against various **cases**.

Each case block must end with **break;**, otherwise the block will fall through to the next block. If none of the cases match the value, you can also implement a **default** case.

```js
var grade = "B";
switch(grade) {
  case "A":
    console.log('You got an A! Great job!');
    break;
  case "B":
    console.log('You got an B! Good job!');
    break;
  default:
    console.log('Try again next time!');
    break;
}
```

#### Truthy and falsey values

Remember how we typed `if (true)` earlier on? In Javascript, it is possible for the value inside the parentheses `()` to be something other than a boolean. For example, we can do the following:

```Javascript
if (1)
  console.log('this runs!');
if (0)
    console.log("this doesn't!");
```

The way this works is determined by what are considered **truthy** and **falsey** values.

- Truthy values evaluate to true (like 1)
- Falsey values evaluate to false (like 0)

There are only several falsey values in Javascript
- false
- 0 and -0
- "" and ''
- null
- undefined
- NaN

It is possible however, for a truthy value to `== false`. [Some great reading on truthy-falsey values can be found here ](http://stackoverflow.com/questions/19839952/all-falsey-values-in-javascript)
