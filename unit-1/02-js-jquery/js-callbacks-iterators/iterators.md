# Iterators

Iterators are examples of _functional programming_ replacements for `for` loops. We can use these functions to perform common Array operations for us.

What might we want to with an array?

* run some piece of logic on each item
* create a new array with each item being slightly transformed
* filter the array to contain only a subset of items
* combine all the items in some fashion

We could accomplish all of this using `for` loops, but writing `for` loops is error prone and tiring. JavaScript provides iterator functions for all of these common operations. They are called (respectively):

* [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
* [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

##General Practice

1. Declare an array
2. Call an iterator on the array
3. Pass a function to the iterator
4. Get results


##`forEach`

`forEach` is the _functional programming_ replacement for your standard `for` loop.  You can take the body from your `for` loop, wrap it in a function, and pass that argument to `forEach`. Let's look at an example:

```js
var friends = ["Markus", "Tim", "Ilias", "Elie"];

// old way, with a for loop
for (var i = 0; i < friends.length; i++) {
  console.log("Hello, " + friends[i] + "!");
}

// cool new way, with the .forEach iterator
friends.forEach(function (buddy) {
  console.log("Hello, " + buddy + "!");
});

// both output the same thing
// > Hello, Markus!
// > Hello, Tim!
// > Hello, Ilias!
// > Hello, Elie!
```

**Try it**

Use the `.forEach` iterator to loop over the following
array of foods and say you like them.

```js
var foods = ["pizza", "tacos", "ice cream"];

// your code here

// The output should be
// > "I like pizza"
// > "I like tacos"
// > "I like ice cream"
```

**Try it again**

Use the `.forEach` iterator to loop over the following
array of objects and say how delicious each one is.

```js
var foods = [
  {name: "Pizza", level: "very"},
  {name: "Tacos", level: "mostly"},
  {name: "Cottage Cheese", level: "not very"}
];

// your code here

// The output should be
// > Pizza is very delicious
// > Tacos is mostly delicious
// > Cottage Cheese is not very delicious
```


## `map`

Sometimes we want to loop over an array and build a new array in the
process. This is what `map` helps us solve. It is like `forEach`, but
it returns a new array based on the return value of the function.

```js
var names = ["tim", "ilias", "elie", "markus"];

// old way with for loop
var cased = [];
for (var i = 0; i < names.length; i++) {
  cased.push(names[i].toUpperCase());
}
console.log(cased);

// new way with `map`
var cased = names.map(function (person) {
  return person.toUpperCase();
});
console.log(cased);

// Should output
// > ["TIM", "ILIAS", "ELIE", "MARKUS"]
// > ["TIM", "ILIAS", "ELIE", "MARKUS"]
```

##`filter`

Filter is an iterator that loops through your array and filters it
down to a subset of the original array. A callback is called on each
element of the original array: if it returns true, then the element is
included in the new array, otherwise it is excluded.

```js
var names = ["tim", "ilias", "elie", "markus"];

var isEven = function (name) {
  return name.length % 2 === 0;
};
var isOdd = function (name) {
  return name.length % 2 !== 0;
};

var evenLengthNames = names.filter(isEven);
var oddLengthNames = names.filter(isOdd);

console.log(evenLengthNames);
console.log(oddLengthNames);

// Should output
// > ["elie", "markus"]
// > ["tim", "ilias"]
```

##`reduce`

Reduce iterates over an array and turns it into one, accumulated
value. In some other languages it is called `fold`. Note that the `reduce` function takes two parameters.

```js
var nums = [1,2,3,4];
var add = function (a, b) {
  return a + b;
};

var sum = nums.reduce(add);
console.log(sum);

// Should output:
// > 10
// which is, 1 + 2 + 3 + 4
```

Reduce also usually accepts an option third parameter that will be the
initial accumulated value. If it is omitted, then the reduction starts
with the first two values in the array.

```js
var nums = [1,2,3,4];
var add = function (a, b) {
  return a + b;
};

var sum = nums.reduce(add, 10);
console.log(sum);

// Should output:
// > 20
// which is, 10 + 1 + 2 + 3 + 4
```

## Resources

Here are some good blog posts that break down `map`, `filter`, and `reduce`.

* [Transforming Arrays with Array#map](http://adripofjavascript.com/blog/drips/transforming-arrays-with-array-map.html)
* [Transforming Arrays with Array#filter](http://adripofjavascript.com/blog/drips/filtering-arrays-with-array-filter.html)
* [Transforming Arrays with Array#reduce](http://adripofjavascript.com/blog/drips/boiling-down-arrays-with-array-reduce.html)

