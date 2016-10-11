# Intro to Express

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


Now this is pretty awesome but it doesn't really do anything. Plus, what if we want to start creating pages instead of just using sending text? In the next article, we'll go through how to create more complicated responses.

## Reference
* [In class exercise on Express](https://github.com/primaulia/express-ref)