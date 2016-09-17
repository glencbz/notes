# Objects and arrays

We've discussed primitives, but Javascript has another kind of value: objects. In JavaScript, almost everything is an object!

## Objects and Methods

For now, just think of an object as a collection of data and methods. For example, if you want to turn a number into a string you can use a helpful method called `toString`.

```js
myNumber.toString()
// => "1"
```

### Common String / Number methods

* Numbers
  * `.toString()` - converts a number to a string
  * `.toFixed()`, - converts a number to a fixed string representation
    * More info: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed
  * `parseInt('33')` - converts a string to an integer
  * `parseFloat('3.1')` - converts a string to a floating point number
* Strings
  * `.split('')` - converts a string into an array split in a provided character
  * `.indexOf('s')` - returns the index of the first appearance of a provided string
  * `.toUpperCase()` - converts a string to all caps
  * `.toLowerCase()` - converts a string to all lowercase
  * `.replace('old', 'new')` - replaces the first appearance of a string with a new string

Note that most of these functions are called on an object, while functions like `parseInt()` and `parseFloat()` only take in arguments.

### Arrays

Unfortunately, strings and numbers are not enough for most programming purposes.
What is needed are collections of data that we can use efficiently, Arrays.

Arrays are great for:

* Storing data
* Enumerating data, i.e. using an index to find them.
* Quickly reordering data

```js
var friends = ['Moe', 'Larry', 'Curly'];
// => ['Moe', 'Larry', 'Curly']
```

Items in an array are stored in sequential order, and indexed starting at `0` and ending at `length - 1`.

```js
// First friend
var firstFriend = friends[0];
// => 'Moe'

// Get the last friend
var lastFriend = friends[2]
// => 'Curly'
```

### Group Exercise

Grab the person next to you. One person, create a variable that equals a comma delimited string with at least four of your favorite foods.

```js
var favorites = "noodles,bread,cheese,filet mignon";
```

Have the second person turn that string into an array, then the first person should ask the second what their third favorite food is.

### Array Methods

* `.pop()` - remove and return the last element in an array
* `.push('element')` - add an element to the end of an array
* `.shift()` - remove and return the first element in an array
* `.unshift(3)` - add an element to the beginning of an array
* `.concat([1, 2])` - concatenate two arrays together
* `.slice(1, 3)` - return a copy of a portion of an array
* `.splice()` - alter an array by adding or removing elements
  * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice
* `.reverse()` - reverse the array
* `.sort()` - sort the elements in an array
* `.join(' ')` - take an array and join the elements together as a string


### Objects

Why use objects to store `key` and `value` pairs? They are like arrays except that data is not stored in any sorted order and keys do not have to numbered indexes.

#### Creating

```js
var friend = {firstName: "Jane", lastName: "Doe"}
```

#### Accessing

```js
friend.firstName
friend.lastName

friend['firstName']
friend['lastName']
```

### Exercise

1.) How would you represent the following using an object?

````js
John, Doe, 36, 1234 Park st.
````

**(Hint: think in terms of firstname, lastname, age, address)**

2.) Once you've represented the above as an object, update John's address to `1234 Park ln`.

3.) Using a combination of Objects and Array, how would you represent the following data:

```
Moe, Doe, 31, 1234 Park st.
Larry, Doe, 36, 1234 Spark st.
Curly, Doe, 36, 1239 Park st.
Jane, Doe, 32, 1239 Spark st.
Emma, Doe, 34, 1235 Spark st.
Elizabeth, Doe, 36, 1234 Park st.
Elinor, Doe, 35, 1230 Park st.
Mary, Doe, 31, 1231 Park st.
Darcy, Doe, 32, 1224 Park st.
Grey, Doe, 34, 1214 Park st.
Lydia, Doe, 30, 1294 Park st.
Harriet, Doe, 32, 1324 Park st.
```
