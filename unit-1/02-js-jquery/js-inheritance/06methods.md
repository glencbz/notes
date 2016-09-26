## Useful methods when working with inheritance

### `hasOwnProperty`

Object.hasOwnProperty('nameOfProperty') - always make sure the name of the property is in quotes. Classes that inherit from other classes will also return true if the property is checked.

Example 1

```js
var taco = {
  food: 'taco'
}

taco.hasOwnProperty(food); // returns an error
taco.hasOwnProperty('food'); // returns true
```

Example 2 with inheritance

```js
function Person(name) {
  this.name = name
}

Person.prototype.greet = function() {
  return 'Hello, my name is ' + this.name;
};

function Student(name, course) {
  Person.call(this, name);
  this.course = course;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

var person = new Person('Bob');
var student = new Student('Tom', 'WDI');

person.hasOwnProperty('name'); //returns true
student.hasOwnProperty('course'); //returns true
student.hasOwnProperty('name'); //returns true
```

### `instanceof`

This method is a bit more common, and the syntax looks like this:

`object instanceof Class`

Example 1:

```js
var color1 = {};
color1 instanceof Object; // returns true
```

Example 2 with inheritance

```js
function Person(name) {
  this.name = name
}

Person.prototype.greet = function() {
  return 'Hello, my name is ' + this.name;
};

function Student(name, course) {
  Person.call(this, name);
  this.course = course;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

var p = new Person('Bob');
var s = new Student('Tom', 'WDI');

s instanceof Person //returns true
p instanceof Student //returns false
Person instanceof Object //returns true
String instanceof Object //returns true
Object instanceof Boolean //returns false
```

### `isPrototypeOf`

This method is used a bit less frequently, but the syntax looks like this:

```js
Object.prototype.isPrototypeOf(objectInstance);
```

Example:

```js
var p = new Person('Bob');
var s = new Student('Tom', 'WDI');

Person.prototype.isPrototypeOf(s); // returns true
Student.prototype.isPrototypeOf(p); // returns false
```

You can read more about the difference between isPrototypeOf and isInstanceOf [here](http://stackoverflow.com/questions/2464426/whats-the-difference-between-isprototypeof-and-instanceof-in-javascript)
