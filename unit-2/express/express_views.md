# Views and Templates in Express

We're continuing the codealong from the previous article! Refer to our Express introduction for the first part.

#### Views

`res.send` is handy for small strings, but what we really want is to send HTML files to the client. What the client actually sees is what we call a **view**. We'll create a folder `/views` and put a view called `index.html` inside it.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Testing a View</title>
  </head>
  <body>
    <h1>Hello world!</h1>
  </body>
</html>
```

Your project directory should look like this

```W
├── app.js
├── node_modules
│   └── express
├── package.json
└── views
    └── index.html
```

We have to make some modifications to `app.js` as well. Firstly we have to use `res.sendFile` instead of `res.send`. Secondly, we have to tell Express where to get our views from by setting our static directory to `views`.

```js
var express = require('express');
var path = require('path');
var app = express();
var port = 3000;

// this sets a static directory for the views
app.use('/', express.static(path.join(__dirname, 'views')));
// equivalent to: app.use(express.static(path.join(__dirname, 'views')));


app.get('/', function(req, res) {
  // use sendFile to render the index page
  res.sendFile('index.html');
});

app.listen(port);
console.log('Server started on ' + port);
```

Express will serve everything in a static directory as if our urls were our system paths.

- `views/index.html` will be served at the url `/index.html` i.e. `/`
- `views/otherpage/something.html` will be served at `/otherpage/something.html`

#### Templates

The downside to this method is that we are only sending HTML files. Imagine if you were Amazon and every item has a similar, but slightly different page. We couldn't possibly create one HTML file for each item.

We can use **templates**, which represent HTML pages, but with values that we can change. This gets turned into real HTML by the templating engine. We'll be using a templating engine called **ejs** (embedded JavaScript).

Let's try editing what we have!

1.  Install `ejs` with the command `npm install —save ejs`

2.  Replace the line `app.use(…)` with the following

```js
    app.set('view engine', 'ejs');
```

3. Replace the line `res.sendFile(…)` with `res.render('index');`
4. Rename `index.html` to `index.ejs`

We're not just sending files any more, we're trying to render our template as HTML. Our syntax is nice and short because ejs assumes we'll be placing all template files into the `/views` folder.

#### Templates with variables

The previous example just gives us the same page as before! What we *really* want to is incorporate values in our template.

Let's update our `index.ejs` a little

```ejs
<!DOCTYPE html>
<html>
  <head>
    <title>Testing a View</title>
  </head>
  <body>
    <h1>Hello, <%= name %>!</h1>
  </body>
</html>
```

The JavaScript being embedded is enclosed by the `<% %>` tags. The addition of the `=` sign on the opening tag means that a value will be printed to the screen. We can also use the following signs to tell EJS to parse code in different ways:

- `<%- name %>` will print out the expression without escaping HTML. 
  - If the name was `<span>"Sterling Archer"<span/>`, then the `<span>` tags won't be escaped.
- `<% name %>` will execute the expression, without printing to the screen.
  - Handy for `if` statements and loops


We can then pass the `name` variable to our template like so:

```js
var express = require('express');
var app = express();
var port = 3000;

app.set('view engine', 'ejs');

app.get('/', function(req, res) {
  res.render('index', {name: "Sterling Archer"});
});

app.listen(port);
```

This doesn't only apply to primitive variables. We can even include variable declarations and iterators using ejs.

```ejs
<!DOCTYPE html>
<html>
  <head>
    <title>Testing a View</title>
  </head>
  <body>
    <h1>Hello, <%= name %>!</h1>

    <% var obsessions = ['spying', 'sarcasm', 'Kenny Loggins']; %>

    <ul>
    <% obsessions.forEach(function(item) { %>
      <li><%= item %></li>
    <% }); %>
    </ul>
  </body>
</html>
```

### Partials

Partials can be used to modularize views and reduce repetition. A common pattern is to move the header and footer of a page into separate views, or partials, then render them on each page.

#### Example

**partials/header.ejs**

```
<!DOCTYPE html>
<html>
<head>
  <title>My Site</title>
</head>
<body>
```

**partials/footer.ejs**

```
</body>
</html>
```

**index.ejs**

```
<% include ../partials/header.ejs %>

<h1>Welcome to my site!</h1>

<% include ../partials/footer.ejs %>
```
