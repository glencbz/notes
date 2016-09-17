# Data Types, Variables and Arrays

## History

**Then**
* developed by Brendan Eich (for Netscape, now Mozilla)
* 10 days
* went through a few different names before settling on JavaScript (Java was popular)
* taken to [ECMA](https://en.wikipedia.org/wiki/Ecma_International) for standardization

**Now**
* JavaScript is THE front-end language
* clunky, [things to complain about](http://wtfjs.com/), but it works and is web-driven!
* tons of open source libraries
* also used as a backend language, using Node.js
* working on [ECMAScript 6](https://github.com/lukehoban/es6features)

## Comments

Comments come in two forms

### Line comments

```js
// descriptive stuff
```
### Multi-line comments

```js
/**
  These
  are
  comments on
  many lines
*/

```

---

## Numbers

Numbers are one of the *types* of **values** we want to be able to interact and play with in JS.

### Integers

```
 ..., -1, 0, 2, 3, 4, 5, ...
```

### Floats (or Decimal numbers)

```
 2.718, 3.14, .5, .25, etc
```

In JS these are both the same **type** of object, which it calls *Numbers*.

This can infrequently cause problems!

```js
0.1 * 0.2 = 0.020000000000000004
```

[How to deal with floating point precision in JavaScript](http://stackoverflow.com/questions/1458633/how-to-deal-with-floating-point-number-precision-in-javascript)

### Exercise

```js
2 + 2 * 3
```

How would you get the `2 + 2` to execute before the `* 3`? In other words, how would you change this expression to get 12?

---
## Strings

Strings are collections of letters and symbols known as **Characters**, and we use them to deal with words and text in Javascript. Strings are just another type of **value** in Javascript.

```js
"John"
'Jane'
```

### Exercise

You can use operators on strings too! Try typing `"John" + "Jane"`. This is called String concatenation

### Tangent: Type coercion

Try this...

```js
"1" + 1
```

Without removing the quotes, how would you get this to equal 2?

---

## Booleans

Booleans are a type that can only have one of two values: true or false.

```js
true
false
```

---

## Operator Review

```
+ (add)
- (subtract)
* (multiply)
/ (divide)
% (modulus)
```


### Special Number Operators

Javascript can be a little cheap with the number of operations it allows you to do. For example, how is someone supposed to square a number or cube a number easily? Luckily there is a special `Math` object with some very useful methods.

* Taking a number to some `power`? Then just use `Math.pow`

```js
// 3^2 becomes
Math.pow(3,2);
// => 4

// 2^4 becomes
Math.pow(2,4);
// => 16
```
* Taking a square root

```js
// √(4) becomes
Math.sqrt(4);
// => 2
```

* Need a `random` number? Then use `Math.random`.

```js
// The following only returns a random decimal
Math.random();
// => .229375290430

/**
  The following will return a
  random number between 0 and 10
*/
Math.random() * 10;
```

* Since Numbers can be **Floats** or **Integers** we often want to get rid of remaining decimal places, which can be done using `Math.floor`.

```js
// Remove the decimal
Math.floor(3.14)
// => 3

Math.floor(3.9999)
// => 3
```

## Variables

Having made some expressions it becomes evident we want to store these values.

```js
var myNumber = 1;
// or also

var myString = "Greetings y'all!";
```

The main note to make here is that these variables should always have the `var` keyword and use `camelCase`



### Reference

[Values, variables, and literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Values,_variables,_and_literals)

[re-introduction to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)

[MDN JavaScript documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript)