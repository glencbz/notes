# The `this` keyword



`this` is one of the most important keywords in JavaScript, and simultaneously, one of the most challenging. Don't worry about all of the quirks of `this` though, some seasoned developers still get tripped up on it (and they're supposed to be pros!). 



At its basic level, `this` is:

-  used in functions
- refers to the object where the function operates

It still sounds a little strange doesn't it? Let's try a small example:

```js
var myInstructor = {
  name: "Prima",
  introduceSelf: function(){
    // note the use of this!
    console.log("Hi my name is " + this.name);
  }
}

myInstructor.introduceSelf();
// => Hi my name is Prima

myInstructor.name = "not Prima";
myInstructor.introduceSelf()
// => Hi my name is not Prima
```

In the example, think of `this` in the way we usually think of the word "this". I might use "this" to refer to "this article" or "this example". `this` in the `introduceSelf` method refers to "this object". In this case, "this object" is `myInstructor`. That's pretty great isn't it? Now every time we create an instructor, that instructor knows how to introduce itself.



### Understanding `this`

`this` can be rather tricky though. Many developers use `this` all the time without really understanding why or how it works the way it does. More often than not, this leads to confusing errors like `Cannot read property 'yourpropertyhere' of undefined`. 

The value of `this` in a function is:

1. only set when the function is called
2. the object that **calls the function**
3. **not** where the function is defined

We can demonstrate point 3. with a simple example:

```js
var myInstructor = {
  name: "Prima",
  introduceSelf: function(){
    console.log("Hi my name is " + this.name);
  }
}

myInstructor.introduceSelf();
// => Hi my name is Prima

// this should work right???
var primaIntroducer = myInstructor.introduceSelf;

primaIntroducer()
// => Hi my name is undefined
```

If `this` were really dependent on the definition, then in both cases, `this` should refer to `myInstructor`. However it isn't. 

In the first example, when we call `myInstructor.introduceSelf`, we take the `introduceSelf` function and 'bind' the value of `this` to `myInstructor`. 

In the second example,  when we saved `myInstructor.introduceSelf` to `primaIntroducer` , we're essentially taking `introduceSelf` and separating it from `myInstructor`. `primaIntroducer` is then called in the global scope, where the value of `this` is something else altogether.

There are ways to fix this, which we will go through later in the chapter on `call`, `apply` and`bind`.



**In the global scope**, `this` refers to the `window` object. You can test this by typing `console.log(this)` in the Dev Tools console.

### Conclusion

Even though `this` is tricky, understanding it is key to  becoming a great JavaScript developer! You might not understand all of it at the start, but as you explore more exotic applications, you'll soon come to appreciate how powerful `this` is!



### Extra Reading

JavaScript is Sexy [Understand JavaScript’s “this” With Clarity, and Master It](http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/)

Journey into JavaScript[Understanding `this` once and for all](https://journeyintojavascript.quora.com/understanding-this-once-and-for-all)

