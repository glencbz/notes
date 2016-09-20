# DOM Manipulation with jQuery - Intro


Before we get into jQuery, let's just think about how we would perform the following tasks:
  - `select` a DIV and change it's content
  - `append` a new DIV with some content to a web page
  - `handle` forms where users want to dynamically add elements to the page
  - `listen` for events on a collection of DIVs or other HTML elements
    + For example, a blog site might have a "like" button for each comment on a post.

#### First, let's just talk about selecting an element with jQuery

To select an element in the DOM, we use the global jQuery function:

```JavaScript
// This is the basic syntax for jQuery selections
$(' ')

// To select a particular element by tag, you do
$('h2') // selects all h2 elements

// To select by ID, you use the same syntax as CSS selectors
$('#someID') // Would select the element with ID="someID"

// To select all elements of a particular class, use CSS syntax again
$('.someClass') // Selects all elements of the class "someClass"

// And you can use more complicated CSS selectors as well
$('p.anotherClass') // Selects all <p> tags that also have the class "anotherClass" (<p class="anotherClass")
```

If you use variable assignment when doing a selection, a "jQuery" object is returned

```JavaScript

// We prepend '$' to variable names when a variable is going to be a jQuery object to help us remember what that variable is for.
var $jqObject = $('p'); // Returns a jQuery object containing all <p> tags on your web page.

// However, we don't have to prepend '$' to our variables. It's just so we can remember what a variable is being used for.
var jqObject = $('p'); // This is functionally identical to the version above that includes the '$' in front of jqObject.
```

#### Selecting a DOM element and changing it's content

In this HTML:


```html
<div id="myDiv">Hello world!</div>
```

```JavaScript
var divToManipulate = document.getElementById('myDiv');
divToManipulate.innerHTML = "Goodbye world!";
```

Now the code above isn't too hard to deal with, but even so, in jQuery, this is a one-liner.

```javascript
$('#myDiv').html("Goodbye world!");
```

See it in action [here](http://jsbin.com/rirumatozu/4/edit?html,js,output)

If we wanted to **save our selection as a jQuery object**, the code would look like this instead:

- First we select the element we want and save it as a jQuery object

```javascript
var $myDiv = $('#myDiv');
```

- Then we use our jQuery object to perform our task

```javascript
$myDiv.html("Goodbye world!");
```

There are three things about the example above that make jQuery easier to use:
  1. jQuery is using the same syntax as CSS to select elements
  2. jQuery allows us to chain methods together to accomplish our goals (i.e., $().html(...) ), making code shorter and easier to understand
  3. jQuery deals with any cross-browser compatibility issues, which may not seem like a big deal in this example, but which quickly become difficult to deal with as things get more complex

#### Appending a DOM element to a web page

If we had the following HTML page...

```html
<html>
<body>

  <div id="container"></div>

</body>
</html>
```

If we want to add a new `<div>` that provides a nice greeting, our vanilla JavaScript would have to be:

```javascript
  var myDiv = document.getElementById('container');
  var newP = document.createElement('p');
  newP.innerHTML = "Hello complicated, multi-step world of adding an element to the DOM!";
  myDiv.appendChild(newP);
```

And in jQuery, it looks like this:

```javascript
  $('#container').append("<p>").append("Hello simple insertion using jQuery chaining");
```

In the jQuery code example above, we first select the DIV with `id="container"`, then we append a new paragraph element (automatically created using core jQuery selector function), and then we append the text we want to insert to the new paragraph element we just created. In effect, the new HTML looks like this after the jQuery is run:

```html
  <div id="container">
    <p>
      Hello simple insertion using jQuery chaining
    </p>
  </div>
```

You can [see this in action on JSBin](http://jsbin.com/rocabu/1/edit?)


#### Modifying Styles (CSS) Using jQuery

You can do more than select elements and modify content. You can also create or update CSS style attributes in jQuery using the .css() method

```js
$("#myDiv").css("color", "red");
```

The code above will change the color of all text inside the DIV with id="myDiv" to red.

[Check this out here](http://jsbin.com/cupumu/1/edit?html,js,output)

Or, if we have a bunch of elements that all have the same class (in this example, it's class="myClass"), we can use the class selector to modify the color of all of them at once:

```js
$(".myClass").css("color", "blue");
```

[You'll find this example here](http://jsbin.com/yutoyi/1/edit?html,js,output)

But that seems kind of boring. I mean, what if we want to do something with less hard-coding using jQuery.

[Here's a repeat of the last example](http://jsbin.com/wevoti/1/edit?html,js,output) that sets the text in all elements of class="myClass" to a random color. Try to understand how it works before moving on:

```javascript
var randColorValue = function() {
  return Math.floor( Math.random() * 255 );
}

var randColor = function() {
  var red = randColorValue();
  var green = randColorValue();
  var blue = randColorValue();

  return "rgb(" + red + "," + green + "," + blue + ")";

}

$(".myClass").css("color", randColor() );
```

#### Adding and Removing Elements Using jQuery

Sometimes in a dynamic web application, user-input is meant to trigger the addition or removal of content or functionality. Using jQuery, we can easily create new DOM elements and insert them into the DOM, or remove existing elements (and any content they contain) from the DOM.

So, let's imagine we have a web page with the following content on it:

```html
<body>
  <div id="outerContainer">
    <div class="innerItem innerItemHeader">Enjoy some hipster ipsum:</div>
    <div class="innerItem">
      Aesthetic migas paleo McSweeney's, pork belly Kickstarter Echo Park sriracha keytar disrupt viral drinking vinegar fanny pack typewriter.
    </div>
  </div>
</body>
```

Let's say we want to add some more hipster ipsum to the page. Something like:

```html
<div class="innerItem">
	Farm-to-table Godard roof party bespoke, fashion axe mustache vinyl.
</div>
```

To add this DIV, and our hipster ipsum content using jQuery, we'd do the following:

Define a new DIV and assign jQuery object to $newDiv

```javascript
$newDiv = $('<div>');

// Add hipster ipsum content
$newDiv.html("Farm-to-table Godard roof party bespoke, fashion axe mustache vinyl.");

// Set it's class to innerItem
$newDiv.addClass("innerItem");

// Append our new element  
$('#outerContainer').append($newDiv);
```


See this in action (and play around with it) [on JSBin](http://jsbin.com/gupade/3/edit?html,js,output)

