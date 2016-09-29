# Routing in Express

#### Logging in Express with Middleware

You may see the word 'middleware' on the web, particularly with regards to express. Middleware is simply code that can be executed anywhere between a request and a response.

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

Let's go through this: After setting up the view engine for our app, we use a method of `app` called `use`. The argument of `use`  is a callback, also known as our middleware. `use` tells Express to use our middleware.  

In this example, we are simply logging out the request method ('GET'), the request path ('/') and the request IP ('127.0.0.1' - localhost). `next()` is a callback function used for the purpose of allowing the app to continue on to other processes once this middleware is done executing. You can think of the `next()` function as telling the app to "move on" to the next middleware.

The order of these arguments is crucial: request is always first, response is always second and the callback is always third.



## Routes with Patterns

We've already seen some basic routes in the introduction, but often, we want routes that are more general; instead of writing the exact url, we can define patterns that our url follows. 

By putting a colon before a string in our route, we can create routes with different variables, or **parameters**. These parameters are automatically pulled out for us by Express and can be accessed via the `req.params` object.

Try running the script below and navigate to http://localhost:3000/greet/Prima/Aulia

```js
var express = require('express');
var app = express();

app.get('/', function(req, res) {
  res.send('hello brian');
});

app.get("/greet/:name/:lastname", function(req, res) {
  res.send("Hello " + req.params.name + " " + req.params.lastname);
});

app.get("/multiply/:x/:y", function(req, res) {
  res.send("The answer is: " + (req.params.x * req.params.y));
});

app.get("/add/:x/:y", function(req, res) {
  res.send("The answer is: " + (parseInt(req.params.x) + parseInt(req.params.y)));
});

app.listen(3000);
```

In addition to having routes where different portions of the URL are different paramaters, we can use the generic string of the URL in our route logic using the wildcard.

```js
app.get("/add/*", function(req, res) {
  var myParams = req.params[0].split("/")
  var result = myParams.reduce(function(total, num) {
    return total + parseInt(num)
  }, 0);
  res.send("The answer is  " + result);
});
```

Navigate to a URL like `http://localhost:3000/add/5/3/3/2/3` and you will get an answer.



## Using a Router - Codealong

We've added routes using `app.use` previously, but there's a better alternative: using a router. A router is like a part of your Express application that just handles the way your app does routing. It's normally better to use this way of doing routes because this allows all your routes to be in their own file. This allows us to make applications more modular, and you won't have a more manageable app.js.

####  Basic router

```javascript
var express = require('express');
var app     = express();
var port    = 3000;
var router  = express.Router();

app.set('view engine', 'ejs');
```
Then we add our routes.

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

//and of course
app.listen(3000);
```

Our  **`views/index.ejs`** file will be simple:

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



Your directory should look something like this

```js
.
├── config
│   └── routes.js
├── index.js
├── node_modules
├── package.json
└── views
    └── index.ejs
```