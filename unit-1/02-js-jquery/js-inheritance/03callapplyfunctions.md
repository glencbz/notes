#`call`, `apply`, `bind` and Other functions

There are several functions that we can use to change what `this` represents.

### `call`

`call` is useful when you want to use a function once. It calls the function on the object supplied and sets `this` to the object.

**Example 1:**

```js
var getAge = function(friend) {
  return friend.age;
};

var john = { name: 'John', age: 21 };
getAge(john);
```

rewritten using `call`

```js
var getAge = function() {
  return this.age;
};

var john = { name: 'John', age: 21 };
getAge.call(john);
```

**Example 2:**

```js
var setAge = function(friend, newAge) {
  friend.age = newAge;
};

var john = { name: 'John', age: 21 };
setAge(john, 35);
```

rewritten using `call`

```js
var setAge = function(newAge) {
  this.age = newAge;
};

var john = { name: 'John', age: 21 };
setAge.call(john, 35);
```

### `apply`

`apply` works just like `call`, but your second parameter is an array of objects instead of a comma separated list.

Going back to Example 2, here's what it would look like with `apply`.

```js
var setAge = function(newAge) {
  this.age = newAge;
};

var john = { name: 'John', age: 21 };
setAge.apply(john, [35]);
```



### `bind`

`bind` is different, because instead of performing just one function call, you create a new function. `bind` returns a new function with `this` bound to whatever object was supplied:

```js
var setAge = function(newAge) {
  this.age = newAge;
};

var john = { name: 'John', age: 21 };
var johnsAge = setAge.bind(john);
johnsAge(35);
```



### Calling on a solution

Let's talk about using `call` or `apply` to set the `this` context for a function before it is run.

```js
function Person(name) {
  this.name = name;
  this.friends = [];
}

Person.prototype.addFriend = function(name) {
  this.friends.push(new Person(name));
};

function Student(name, course) {
  // masks all the constructor properties including name (as the second parameter)
  Person.call(this, name);
  this.course = course;

  // If we wanted to, we could also use .apply like so:
  // Person.apply(this, [name]);
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;
```

The code above is why we forgo talking about `this` until now. In the context of event listener callbacks, `this` refers to the DOM element that trigged the event. But here, `this` can *really be anything you want it to be*.

Still confused? [Understanding `this` once and for all](https://journeyintojavascript.quora.com/understanding-this-once-and-for-all)



## `this` and Callbacks Problems

Inheritance isn't the only situation where we have to deal with `this`. When the callback function is a method that uses the `this` object, we have to modify how we execute the callback function to preserve the `this` object context.

Let's define an object with some properties and a method. We will later pass the method as a callback function to another function:

```javascript
var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object​
  setUserName: function(firstName, lastName)  {
    // this refers to the fullName property in this object​
    this.fullName = firstName + " " + lastName;
  }
}

function getUserInput(firstName, lastName, callback) {
  callback(firstName, lastName);
}

getUserInput("Barack", "Obama", clientData.setUserName);

console.log (clientData.fullName);
//=> Not Set

console.log (window.fullName);
//=> Barack Obama
```

Since `getUserInput` is a global function, `this` defaults to the window object.

#### Use the `call` or `apply` Function To Preserve `this`

We can fix the preceding problem by using either the `call` or `apply` functions.

Let's walk through an example by defining another object with properties and a method and pass the method as a callback later:

```javascript
var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object
  setUserName: function (firstName, lastName)  {
    // this refers to the fullName property in this object
    this.fullName = firstName + " " + lastName;
  }
}

function getUserInput(firstName, lastName, callback, callbackObj)  {
  // The use of the Apply function below will set the this object to be callbackObj
  callback.apply(callbackObj, [firstName, lastName]);
}
getUserInput("Barack", "Obama", clientData.setUserName, clientData);

console.log(clientData.fullName);
//=> Barack Obama
```
Now, we have the function as well as the object we want to access. We can then `apply` or `call` our function on our object, making it behave the way we want. 

Note that we achieve a similar result with `bind`, but we have to make some modifications. First we have to finish creating our object and then `bind` the method to the object we want.

```js
var clientData = {
  id: 094545,
  fullName: "Not Set",
  // setUserName is a method on the clientData object
  setUserName: function (firstName, lastName)  {
  // this refers to the fullName property in this object
    this.fullName = firstName + " " + lastName;
  }
}

// bind the setUserName method to clientData and assign it back to clientData
clientData.setUserName = clientData.setUserName.bind(clientData);

function getUserInput(firstName, lastName, callback)  {
  // because the callback is already bound, we don't need to worry about supplying an object
  callback(firstName, lastName);
}

getUserInput("Barack", "Obama", clientData.setUserName);

console.log(clientData.fullName);
//=> Barack Obama
```
