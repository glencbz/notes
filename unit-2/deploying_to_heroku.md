# Deploying the Node Application to Heroku

1. Create Procfile and add ‘web: nodemon app.js’.
2. Create new db in mlab.
3. Create new user for that db in mlab.
4. Create .env.local and add:
  ```js
    MONGO_URI=mongodb://localhost/<dbname>
  ```
5. Create .env.production and add:
  ```js
mongodb://<dbuser>:<dbpassword>@<address>:<port>/<dbname>
  ```
4. In app.js, check to see if these have been added, if not add:
```js
dotenv.load({ path: '.env.' + process.env.NODE_ENV});
mongoose.connect(process.env.MONGO_URI);  
app.listen(process.env.PORT || <your port>);
```
5. In terminal, run: `heroku create`
6. In terminal, run: `git push heroku master`
7. To open, run: `heroku open`

EXTRA. If you hit an application error, in terminal, run: `heroku logs -- tail`
