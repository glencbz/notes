# Local Authentication with Express and Passport (Part 2)

## Sign-in

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

We need to add a new method to the user schema in `models/user.js` so that we can use the method `user.validatePassword()`. Let's add:

```javascript
userSchema.methods.validPassword = function(password) {
  return bcrypt.compareSync(password, this.local.password);
};
```

#### Adding flash messages to the view

As we are again using flash messages, we will to add some code to display them in the view:

In `views/login.ejs`, add the same code that we added in `views/signup.ejs` to display the flash messages:

```
<% if (message.length > 0) { %>
  <div class="alert alert-danger"><%= message %></div>
<% } %>
```

#### Login GET Route handler

Now, let's add code to `models/users.js` to render the login form in the `getLogin` action in the controller:

```javascript
function getLogin(req, res) {
  res.render('login', { message: req.flash('errorMessage') });
}
```

#### Login POST Route handler

We also need to have a route handler that deals with the login form after we have submit it. So in `models/users.js` let’s also add:

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


## Test it out

#### Invalid Login

First try to login with:

- a valid email
- an invalid password

You should also see the message 'Oops! Wrong password.'

#### Valid Login

Now, try to login with valid details and you should be taken to the index page with a message of "Welcome".

The login strategy has now been setup!

## Sign Out

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

Now in `views/layout.ejs`, we can add this to our nav bar:

```
<% if (currentUser) { %>
  <li><a href="/logout">Logout</a></li>
<% } else { %>
 <li><a href="/login">Login</a></li>
 <li><a href="/signup">Signup</a></li>
<% } %>
<li><a href="/secret">Secret page (only if authenticated)</a></li>
```

Inside `controllers/usersController.js`, we need to add the corresponding logout logic to the `getLogout` route handler:

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

For the `/secret` route, we need to add this to the `config/routes.js` file:

```javascript
router.route("/secret")
  .get(authenticatedUser, usersController.getSecret)
```

Now every time the route `/secret` is called, the method `authenticatedUser` will be executed first. In this method, we either redirect to the homepage or go to the next method to execute.

Finally, we need to add the corresponding function to the `controllers/usersController.js`:

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


