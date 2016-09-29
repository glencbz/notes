
# Intro to Express and Templating

### Objectives
- Use and configure middleware like body-parser to handle form submissions
- Write out the skeleton of a RESTful API
- Review what JSON is and why we're using JSON as the format for our data
- Interact with HTTP verbs using CURL or an app
- Identify the HTTP verbs we'll be using for an API

## Recapping Node and Intro to Express

#### First let's review

* What is Node?

Node is a low-level, non-blocking, event-driven platform which allows you to write JavaScript on the server-side.

* What is npm?

npm is Node's package manager. It's used to manage dependencies.

#### What is express.js?

Express.js is a simple [web framework](http://stackoverflow.com/questions/2964140/what-is-a-software-framework) for Node.js.

It's biggest highlights are:

- extremely lightweight/minimalistic (gives you the power to have more control over your application)
- easy to create routes
- very simple to apply [middleware](http://stackoverflow.com/questions/2904854/what-is-middleware-exactly)

## Let's create an app using Node and Express - Codealong

Get to it:

1. `mkdir express-blog`
2. `cd express-blog`
3. `npm init` (Hit enter to accept the defaults and see the new [`package.json`](https://docs.npmjs.com/cli/init) file
4. `npm install express --save`
5. `touch app.js` in express-blog directory


The `--save` option adds the module as a dependency in your `package.json` file. This allows anyone looking at your app (i.e. a dev team member) to be able to see what your app is "made of" and if they clone your app and run `npm install`, all dependencies will be installed!

Check out the package.json file:

```json
"dependencies": {
  "express": "^4.11.1"
}
```

Let's start coding!

```javascript
// app.js

// import express
var express = require('express');
// create the app
var app     = express();
var port = 3000;

// create a route
app.get('/', function(req, res) {
  res.send('yes this is briam');
});

// run the app at this port
app.listen(port);
console.log('Server started on ' + port);
```

Then run the app using:

```bash
node app.js
```

Navigate to `http://localhost:3000` in your browser and voila!

## Routing in Express

Let's understand what actually happens in our Express app, particularly these lines here:

```javascript
// create a route

app.get('/', function(req, res) {
  res.send('yes this is briam');
});
```

This is what we call a **route**. In Express, a route maps a url to a callback function. Whenever somebody sends an http to the given url with the right HTTP method, the callback function is called.

In this case, we first specify the method `get`, and the arguments we pass to this function are the url `'/'` and the callback function, which is anonymous. The callback function takes two arguments: `request` and `response` (often shortened to `req` and `res`).

Hence, we think of the code here as creating a simple rule: if someone sends a GET request at the `'/'` url, we will send them the response `'yes this is briam'`.

Try adding this route and see if you can acccess it from the browser:

```javascript
// create a route

app.get('/other', function(req, res) {
  res.send('Another route?!?');
});
```


Now this is pretty awesome (isn't it?) but it doesn't really do anything. Plus, what if we want to start creating pages instead of just using sending text?

## Views and Templates in Express

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