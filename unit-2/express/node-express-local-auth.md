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

Let's have a quick look at the `usersController.js` controller. As you can see, the file is structured like a module with six empty route handlers:

```
// GET /signup
// POST /signup
// GET /login
// POST /login
// GET /logout
// Restricted page
```

The statics controller, just has the home action.

#### `routes.js`

We have separated the routes into a separate file, to remove them from the `app.js` file.

### Signup

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

### `user.js`

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


In the `usersController.js` controller, for the method `postSignup`, we will add the call to the strategy we've declared earlier, `local-signup`:

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

In the view `signup.ejs`, above the form, add:

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

Now, start up the app using `nodemon app.js` and visit `http://localhost:3000/signup`. Try to signup two times with the same email, you should see the message "This email is already used." appearing when the form is reloaded.

## Sign-in - Codealong

Now we need to write the sign in logic.

We also need to implement a custom strategy for the login, In `config/passport.js`, after the signup strategy, add add a new `LocalStrategy`:

```javascript
passport.use('local-login', new LocalStrategy(lsConfig , function(req, email, password, callback) {

}));
```

The first argument is the same as for the signup strategy - we ask Passport to recognize the fields `email` and `password` and to pass the request to the callback function.

Inside `config/passport.js` let's add this code:

```javascript
...
}, function(req, email, password, done) {

  // Search for a use with this email
  User.findOne({ 'local.email': email }, function(err, user) {
    if (err) return done(err);

    // If no user is found
    if (!user) return done(null, false, req.flash('errorMessage', 'No user found.'));


    // Check if the password is correct
    if (!user.validPassword(password)) return done(null, false, req.flash('errorMessage', 'Oops wrong password!'));

    return done(null, user);
  });
}));
...

```
For this strategy, we will search for a user document using the email received in the request. If a user is found, we will try to compare the hashed password stored in the database to the one received in the request params. If password matches, the user is authenticated; if not, then the password is wrong.

#### User validate method

We need to add a new method to the user schema in `user.js` so that we can use the method `user.validatePassword()`. Let's add:

```javascript
userSchema.methods.validPassword = function(password) {
  return bcrypt.compareSync(password, this.local.password);
};
```

#### Adding flash messages to the view

As we are again using flash messages, we will to add some code to display them in the view:

In `login.ejs`, add the same code that we added in `signup.ejs` to display the flash messages:

```
<% if (message.length > 0) { %>
  <div class="alert alert-danger"><%= message %></div>
<% } %>
```

#### Login GET Route handler

Now, let's add the code to render the login form in the `getLogin` action in the controller (`users.js`):

```javascript
function getLogin(req, res) {
  res.render('login', { message: req.flash('errorMessage') });
}
```

#### Login POST Route handler

We also need to have a route handler that deals with the login form after we have submit it. So in `users.js` let’s also add:

```javascript
function postLogin(req, res) {
  var loginStrategy = passport.authenticate('local-login', {
    successRedirect: "/",
    failureRedirect: "/login",
    failureFlash: true
  });

  return loginStrategy(req, res);
}
```

You should be able to login now!

At this point, you should realise Passport alone is not enough for authentication; the Passport module itself needs a strategy module, that serves to perform a specific type of authentication. When creating authentication using Passport, you will always need Passport and a strategy, at a minimum.


## Test it out - Independent Practice

#### Invalid Login

First try to login with:

- a valid email
- an invalid password

You should also see the message 'Oops! Wrong password.'

#### Valid Login

Now, try to login with valid details and you should be taken to the index page with a message of "Welcome".

The login strategy has now been setup!

## Sign Out - Codealong

#### Logout

The last action to implement for our authentication system is to set the logout route and functionality.

#### Accessing the User object globally

By default, passport will make the user available on the object `request`. In most cases, we want to be able to use the user object everywhere, for that, we're going to add a middleware in `app.js`:

```javascript
require('./config/passport')(passport);

app.use(function (req, res, next) {
  global.currentUser = req.user;
  next();
});
```

Now in `layout.ejs`, we can add this to our nav bar:

```
<% if (currentUser) { %>
  <li><a href="/logout">Logout</a></li>
<% } else { %>
 <li><a href="/login">Login</a></li>
 <li><a href="/signup">Signup</a></li>
<% } %>
<li><a href="/secret">Secret page (only if authenticated)</a></li>
```

Inside `usersController.js`, we need to add the corresponding logout logic to the `getLogout` route handler:

```javascript
function getLogout(req, res) {
  req.logout();
  res.redirect('/');
}
```

Passport exposes a `logout()` function on req (also aliased as `logOut()`) that can be called from any route handler that needs to terminate a login session. Invoking `logout()` will remove the `req.user` property and clear the login session if one exists.

You should now be able to login and logout! Test this out.


## Sign Out, Restricting access

As you know, an authentication system is used to allow/deny access to some resources to authenticated users.

Let's now turn our attention to the `secret` route handler and its associated template.

To restrict access to this route, we're going to add a method at the top of `config/routes.js`:

```javascript
function authenticatedUser(req, res, next) {
  // If the user is authenticated, then we continue the execution
  if (req.isAuthenticated()) return next();

  // Otherwise the request is always redirected to the home page
  req.flash('errorMessage', 'Login to access!');
  res.redirect('/login');
}
```

Now when we want to "secure" access to a particular route, we will add a call to the method in the route definition.

For the `/secret` route, we need to add this to the `/config/routes.js` file:

```javascript
router.route("/secret")
  .get(authenticatedUser, usersController.getSecret)
```

Now every time the route `/secret` is called, the method `authenticatedUser` will be executed first. In this method, we either redirect to the homepage or go to the next method to execute.

Finally, we need to add the corresponding function to the `usersController.js`:

```javascript
function getSecret(req, res){
  res.render('secret.ejs');
  }
```

Now test it out by clicking on the secret page link. You should see: "This page can only be accessed by authenticated users"

Now, let's move that in the navbar:

```
<% if (currentUser) { %>
  <li><a href="/logout">Logout</a></li>
  <li><a href="/secret">Secret page (only if authenticated)</a></li>
<% } else { %>
  <li><a href="/login">Login</a></li>
  <li><a href="/signup">Signup</a></li>
<% } %>
```

## Independent Practice

- Once the user is authenticated, make sure he/she can't access the sign-in or sign-up and redirect with a message, and vice-versa for the logout

#### Solution

Make a new unAuthenticatedUser function:

```javascript
function unAuthenticatedUser(req, res, next) {
  if(!req.isAuthenticated()) return next();
  req.flash('errorMessage', 'You are already logged in!')
  res.redirect('/');
}
```

And update the routes to be:

```javascript
router.route('/')
  .get(staticsController.home);

router.route('/signup')
  .get(unAuthenticatedUser, usersController.getSignup)
  .post(usersController.postSignup);

router.route('/login')
  .get(unAuthenticatedUser, usersController.getLogin)
  .post(usersController.postLogin);

router.route('/logout')
  .get(authenticatedUser, usersController.getLogout);

router.route('/secret')
  .get(authenticatedUser, usersController.getSecret);
```

Inside the statics controller add:

```javascript
function home(req, res) {  
  res.render('index.ejs', { message: req.flash('errorMessage') });
}
```

Then on the index page, add:

```ejs
<% if (message.length > 0) { %>
  <div class="alert alert-danger"><%= message %></div>
<% } %>
```

Test this by logging in and then revisiting "/login". We could obviously move these messages to the layout at a later date, but we would need to assign a global flash message.


## Conclusion

Passport is a really useful tool because it allows developers to abstract the logic of authentication and customize it, if needed. It comes with a lot of extensions that we will cover later.

- How do salts work with hashing?
- Briefly describe the authentication process using passport in Express.
