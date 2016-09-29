
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



#### Logging in Express with Middleware - Codealong (10 mins)

You may have seen this word floating around or seen it when you did Sinatra (Rack Middleware). Middleware is simply code that can be executed anywhere between a request and a response.

In our Hello World app we are logging out the server port once it has started - that is it. We get no other information about requests or errors like we have in Rails. We can use _Middleware_ to achieve this.

Add the following to your app.js file:

```javascript
// app.js
.
.
.
app.set('view engine', 'ejs');


// Middleware
app.use(function(req, res, next) {
  console.log('%s request to %s from %s', req.method, req.path, req.ip);

  next();
});

app.get('/', function(req, res) {
.
.
.
```

Let's go through this: After setting up the `view engine` for our app, we use a new method of app called `use`. As an argument to `use` we pass in a function that performs some executables, log some data and fire a callback named `next`. This function, this block of code, is our middleware and `use` is a method given to us by Express whose purpose is to simply implement any middleware we pass to it.

In this example, we are simply logging out the request method ('GET'), the request path ('/') and the request IP ('127.0.0.1' - localhost). `next()` is just a callback function used for the purpose of allowing the app to continue on to other processes once this middleware is done executing. You can think of the `next()` function as telling the app to "move on."

The order of these arguments is crucial: request is always first, response is always second and the callback is always third.

## Adding Routes to our app - Codealong (15 mins)

Let's add some routes. This should all be familiar but let's go through it.

[ExpressJS 4.0](https://scotch.io/tutorials/learn-to-use-the-new-router-in-expressjs-4) comes with the new Router. Router is like a mini Express application. It doesn’t bring in views or settings but provides us with the routing APIs like `.use`, `.get`, `.param`, and `route`.

First we define our _router_. This is what handles our routing. It's normally better to use this way of doing routes (and extracting them into their own files) as it makes applications more modular, and you won't have a 500 line app.js.

```javascript
var express = require('express');
var app     = express();
var port    = process.env.PORT || 3000;
var router  = express.Router();
```

This needs to be under the definition of `var app`!  Then we add our routes.

```javascript
router.get('/', function(req, res) {
  res.render('index', { header: 'index!'});
});

router.get('/contact', function(req, res) {
  res.render('index', { header: 'contact!'});
});

router.get('/about', function(req, res) {
  res.render('index', { header: 'about!'});
});
```

At the bottom of the page add:

```javascript
app.use('/', router);
```

As we saw before we are rendering our template and then passing in a local variable (_header_) to use in our template, just like instance variables defined in our controller or layouts that we passed to our views in Rails. We can our variable in our `index.ejs` file like this:

```ejs
<h1><%= header %></h1>
```


#### Creating a router module


Let's move this router into another file to separate it from our `app.js`

```bash
$ mkdir config
$ touch config/routes.js
```

Inside this file we need to move all of our route handlers and at the end of the file, we need to export our router:

```javascript
var router  = express.Router();

router.get('/', function(req, res) {
  res.render('index', { header: 'index!'});
});

router.get('/contact', function(req, res) {
  res.render('index', { header: 'contact!'});
});

router.get('/about', function(req, res) {
  res.render('index', { header: 'about!'});
});

module.exports = router;
```

Now inside our app.js, let's require this router at the top:

```javascript
var router = require("./config/routes");
```

## Restful Routing - Intro (10 mins)

As we've already seen with Sinatra, we will use the RESTful standard to build our web apps. At the moment, we've just covered how to handle GET requests, but we can create callbacks for all types of requests. For example, if we want to create a restful controller for the resource posts, we can add this into our `config/routes.js` file:

```javascript
router.get('/posts', function(req, res) {
  console.log("index");
  res.send("INDEX");
});

router.get('/posts/:id', function(req, res) {
  console.log("show");
  res.send("SHOW");
});

router.get('/posts/new', function(req, res) {
  console.log("new");
  res.send("NEW");
});

router.post('/posts', function(req, res) {
  console.log("create");
  res.send("CREATE");
});

router.get('/posts/:id/edit', function(req, res) {
  console.log("edit");
  res.send("EDIT");
});

router.put('/posts/:id', function(req, res) {
  console.log("update");
  res.send("UPDATE");
});

router.delete('/posts/:id', function(req, res) {
  console.log("delete");
  res.send("DELETE");
});
```

We can namespace our endpoints by adding a first argument to `.use()`, in this case "/posts". Likewise, we could've further namespaced our api with "/api/posts". Dev teams namespace their APIs with "/api" to help clearly define if an endpoint is meant for clients or other devs.

Anyway, the code above will create these 7 routes:


```javascript
GET    /posts
GET    /posts/:id
GET    /posts/new
POST   /posts
GET    /posts/:id/edit
PUT    /posts/:id
DELETE /posts/:id
```

If we want, we might create a dedicated router for this resource and namespace the routes like this:

```javascript
app.use("/posts", postRouter)
```

On a side note, just like how we use `.use()` to integrate middleware into our app, express has a middleware method specifically for routes, `.param()`.

## BodyParser and handling params/JSON - Intro (5 mins)

When data is sent to the server via a POST request, the content of the request is passed as a string, but we want to access it as if it was a JSON object:

Let's create a new view file, `views/posts/new.ejs`, and inside add a form like this:

```html
<h1>New Post</h1>

<form method="post" action="/posts">
  <label for="post_title">Title</label><br>
  <input type="text" name="post[title]" id="post_title"><br>

  <label for="post_author">Author</label><br>
  <input type="text" name="post[author]" id="post_author"><br>

  <label for="post_content">Content</label><br>
  <textarea name="post[content]"></textarea><br>

  <button>Go go gadget Postmaker</button><br>
</form>
```

Inside our new action, we then need to render this page:

```javascript
router.get('/posts/new', function(req, res) {
  res.render("posts/new");
});
```

Inside our create action, we need to logout the body of the HTTP request:

```js
router.post('/posts', function(req, res) {
  console.log(req.body)
})
```

Once this form is submitted, by default we this body will show was `undefined`. In order for it to be used, we need to use a package called `body-parser`.

## Configure your app to use body-parser - Codealong (10 mins)

First add the package to your `package.json` dependencies:

```bash
$ npm install body-parser --save
```

Now in `app.js`, add:

```javascript
var bodyParser = require("body-parser");
```

and also:

```javascript
app.use(bodyParser.urlencoded({
  extended: true
}));
```

The params passed with a request will be "decoded" automatically, allowing you to use dot notation when working with JavaScript objects.

```
{ post: { title: 'asdad', author: 'asdasd', content: 'asdadas' } }
```

If you are writing an api, meant to receive and send JSON, you would change the line above to:

```javascript
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({
  extended: true
}));
```

Now the app will decode all JSON received in the body of a client request.


## Independent Practice (15 minutes)

> ***Note:*** _This can be a pair programming activity or done independently._

In the same file, try to create the 7 Restful Routes for the resource "author". Every method should return some text saying the HTTP Verb, which URI has been used to do the request and which REST action it corresponds to.

Example, for a POST request to `/authors` the text sent back should be:

```
POST request to /authors, this is the CREATE action
```

Also, test your application with `cURL` requests to each of the RESTful endpoints.

## Conclusion (5 mins)
A framework can be overwhelming at the start, after a couple of days you will see how it makes your life easier.  We will work more on how to make RESTful controllers, this is just an introduction.

- What is Middleware and why is it helpful in Express?
- Explain how body-parser helps decode information in your application.
- Identify some similarities and differences between Express and Sinatra.
