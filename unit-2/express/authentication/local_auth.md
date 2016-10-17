# Local Authentication with Express and Passport

### Objectives

- Create a login form with email & password
- Use `passport-local` to find a user and verify their password
- Restrict access to API without an authenticated user

## Passport and the logic - Intro

From the [Passport website](http://passportjs.org/docs):

"_Passport is authentication Middleware for Node. It is designed to serve a singular purpose: authenticate requests. When writing modules, encapsulation is a virtue, so Passport delegates all other functionality to the application. This separation of concerns keeps code clean and maintainable, and makes Passport extremely easy to integrate into an application._

_In modern web applications, authentication can take a variety of forms. Traditionally, users log in by providing a username and password._"

#### Strategies

The main concept when using Passport is to register _Strategies_.  A strategy is a Passport middleware that will create some action in the background and execute a callback. This callback should handle successful and unsuccessful attempts

Because strategies are packaged as individual modules, we can pick and choose what modules we need for our application. This logic allows us to keep the controller logic simple because we can delegate the authentication to Passport.

On a high-level, Passport is the authentication middleware and the strategy is middleware used by Passport.


## Implementing Passport.js - Codealong

#### Setup/Review Starter Code

First, unzip the starter code and setup with `npm install` to ensure that we have all of the correct dependencies.

The starter-code is structured like this:

```
.
└── app
    ├── app.js
    ├── config
    │   ├── passport.js
    │   └── routes.js
    ├── controllers
    │   └── users.js
    ├── models
    │   └── user.js
    ├── package.json
    ├── public
    │   └── css
    │       └── bootstrap.min.css
    └── views
        ├── index.ejs
        ├── layout.ejs
        ├── login.ejs
        ├── secret.ejs
        └── signup.ejs

7 directories, 12 files
```

Now let's open the code up in Atom with `atom .`.

#### Users & Statics Controller

Let's have a quick look at the `controllers/usersController.js` controller. As you can see, the file is structured like a module with six empty route handlers:

```
// GET /signup
// POST /signup
// GET /login
// POST /login
// GET /logout
// Restricted page
```

The statics controller, just has the home action.

#### `config/routes.js`

We have separated the routes into a separate file, to remove them from the `app.js` file.

### Part 1: Signup 

First we will implement the signup logic. For this, we will have:

1. a route action to display the signup form
2. a route action to receive the params sent by the form

As for the signup logic itself, we will delegate the work to a strategy. This strategy handles:
1. saving the user data into the database
2. hashing the password
3. validating the data

Open the file `config/passport.js` and add:

```javascript
var LocalStrategy   = require('passport-local').Strategy;
var User            = require('../models/user');

var lsConfig = {
    usernameField : 'email',
    passwordField : 'password',
    passReqToCallback : true
};

var ls = new LocalStrategy(
    lsconfig,
    function(req, email, password, done) {
    });

module.exports = function(passport) {
  passport.use('local-signup', ls);
}
```

The first thing to note here is that we are using a dependency, `passport-local`, to help configure the strategy middleware of Passport. This module lets you authenticate using a username and password. 

Because our strategies are modular, we could swap them out for others. One useful one is `passport-google-oauth` which lets your app authenticate using Google.

#### `lsconfig`

 By default, `passport-local` expects to find the fields `username` and `password` in the request. If you use different field names, as we do, you rename them in `LocalStrategy`'s configuration. We do this configuration by passing our `lsconfig` object to our new `LocalStrategy`.

### Configure Strategy

Just like how Express has `.use()` available for mounting middleware, so does Passport. `passport.use()` takes two arguments: a name and a strategy. By declaring the name of the strategy, Passport can refer to it later. 

To use a `LocalStrategy`, we first have to configure it. Inside our empty callback, we will implement our custom logic to signup a user.

```javascript
// in the local strategy callback
  function(req, email, password, done) {
    // Find a user with this email
    User.findOne({ 'local.email' : email }, function(err, user) {
      // Handle errors
      if (err) return done(err);
      
      // If there is a user with this email
      if (user) 
        return done(null, false, req.flash('errorMessage', 'This email is already used!'));

      // Otherwise
      else {
        var newUser            = new User();
        newUser.local.email    = email;
        newUser.local.password = User.encrypt(password);
        
        // Create and save the new user
        newUser.save(function(err, user) {
          if (err) return done(err);
            return done(null, user);
        });
      }
    });
  });

```

Our `LocalStrategy` takes a callback argument that is executed when this strategy is called. This callback method will receive the request object and the values that match the configuration object fields (`usernameField` and `passwordField`). This callback also takes a callback parameter (`done`) to execute when this strategy is done, just like the `next` callback in Express middleware.

First we will try to find a user with the same email, to make sure this email is not already used. In this case, we will call `done` with `null` (meaning no error) and `false` (meaning there is no user object).

**If no user is returned**, it means that the email received in the request can be used to create a new user object. We will, therefore create a new user object, hash the password and save the new created object to our Mongo collection. When all this logic is created, we will call the `callback` method with the two arguments: `null` and the new user object created.

**If a user is returned**, we pass a user object to `done`. Based on this argument, Passport will know if the strategy has been successfully executed and whether the request should redirect to the `success` or `failure` path. (see below).

### `models/user.js`

The last thing is to add the method `encrypt` to the user model to hash the password received and save it as encrypted:

```javascript
userSchema.statics.encrypt = function(password) {
  return bcrypt.hashSync(password, bcrypt.genSaltSync(8), null);
};
```

As we did in the previous lesson, we generate a salt token and then hash the password using this new salt.

That's all for the signup strategy.

#### Route Handler

Now we need to use this strategy in the route handler.


In the `controllers/usersController.js` controller, for the method `postSignup`, we will add the call to the strategy we've declared earlier, `local-signup`:

```javascript
function postSignup(req, res) {
  var signupStrategy = passport.authenticate('local-signup', {
    successRedirect: '/',
    failureRedirect: '/signup',
    failureFlash: true
  });

  return signupStrategy(req, res);
}
```

Here we are calling the method `authenticate` (given to us by passport) and then telling passport which strategy (`'local-signup'`) to use.

The second argument tells passport what to do in case of a success or failure.

- If the authentication was successful, then the response will redirect to `/`
- In case of failure, the response will redirect back to the form `/signup`

#### Session

We've seen in previous lessons that authentication is based on a value stored in a cookie. This cookie is sent to the server for every request until the session expires or is destroyed.

To use the session with passport, we need to use two new methods in `config/passport.js` :

```javascript
module.exports = function(passport) {

  passport.serializeUser(function(user, done) {
    done(null, user.id);
  });

  passport.deserializeUser(function(id, done) {
    User.findById(id, function(err, user) {
      done(err, user);
    });
  });
...

```

The method `serializeUser` is used when a user signs in or signs up. Passport will call this method to save (i.e. serialize) some information about the user session (`user.id` in this case).

The method `deserializeUser` is called every time there is a value for Passport in the session cookie. In this method, we will receive the value stored in the cookie (we stored `user.id`) then search for a user and call `done`. The user object will then be stored in the request object.

## User Feedback: Flash Messages

Flash messages are one-time messages that are rendered in the views. When the page is reloaded, the flash is destroyed.

In our current Node app, back when we have created the signup strategy, in the callback we had this code:

```javascript
req.flash('errorMessage', 'This email is already used.')
```

This will store the message 'This email is already used.' into the response object and then we will be able to use it in the views. This is really useful to send back details about the process happening on the server to the client.


## Incorporating Flash Messages - Codealong

In the view `views/signup.ejs`, above the form, add:

```
<% if (message.length > 0) { %>
  <div class="alert alert-danger"><%= message %></div>
<% } %>
```

Let's add some code into `getSignup` in the users controller to render the template:

```javascript
function getSignup(req, res) {
  res.render('signup', { message: req.flash('errorMessage') });
}
```

Now, start up the app using `nodemon app.js` and visit `http://localhost:3000/signup`. Try to signup two times with the same email, you should see the message "This email is already used." appearing when the form is reloaded. Awesome!

We'll look at the next article to figure out how to actually implement signing in and out
