# Building Models with ActiveRecord & Migrations

### Objectives
- Create a class that inherits from ActiveRecord
- Create a table schema to describe the class/model in our database
- Write a migration to update our model with new attributes
- Write a migration to change our model's attributes
- Write a migration to delete a model's attribute

## Wait, what are Models? - Intro

#### Refresh on Models

In Rails, when we 'model' kinds of objects, we use classes. This is a little different from Mongoose models because we don't immediately define a database schema, we define code objects. These objects in Ruby represent the real world objects we care about.

#### But objects are just a collection of data, how can we map them to a relational database?

Well, that's where ORMs come in.  ORM stands for: Object Relational Mapping, and it's a technique that connects the rich objects of an application to tables in a database management system. For example, Mongoose is an ORM for MongoDB.

Let's discuss how a user object, instantiated from the User class, could map to a Users table in our database.

We'll pretend we have a User class with the attributes id, name, age, and address:

```ruby
class User
  attr_accessor :id, :name, :age, :address
end
```

And let's pretend that we create a new user, Rob stark, whose object is shown below:

```ruby
=> #<User:0x007fc8b18c5718 @address="1 Winterfell Lane", @age=16, @id=1, @name="Rob Stark">
```

With an ORM, we're able to take that instance of class User and map it to our relational database:

```psql
 id  |   name    | age |                      address                       | king?
----+-----------+-----+----------------------------------------------------+-------
  1 | Rob Stark |  16 | 1 Winterfell Lane                                  | t
(1 row)
```

Using ORMs, the properties and relationships of the objects in an application can be easily stored and retrieved from a database without writing SQL statements directly and with less database access code, overall.

#### An Actively Awesome ORM: ActiveRecord

Taken from [rubyonrails.org](guides.rubyonrails.org/active_record_basics.html):

Active Record, as an ORM Framework, gives us several mechanisms, the most important being the ability to:

- represent models and their data
- represent associations between these models
- represent inheritance hierarchies through related models
- validate models before they get persisted to the database
- perform database operations in an object-oriented fashion

Active Record is the M in MVC - the model - which is the layer of the system responsible for representing business data and logic.

This will all make a lot more sense once we start using it...so, let's start using it!


## Requiring and using ActiveRecord - Demo


Imagine we're a successful talent management agency, Tunr, and we have a Rails app. Most likely, we'll see something like this in our controllers:

```ruby
Artist.all #what?
Artist.create(params[:artist]) #who?
Artist.find(params[:id]) #nah uh!!
```

We get all these awesome methods - that we don't have to write ourselves - and we can call them on our Artist class; and this is all possible when we require ActiveRecord (yes, it's just another gem!)

## Let's Create Some Data Tables with migrations...and without SQL!

To create a table in Rails we need to create a "migration".  From [rubyonrails.org](rubyonrails.org):

*"Migrations are a convenient way to alter your database schema over time in a consistent and easy way. They use a Ruby DSL so that you don't have to write SQL by hand, allowing your schema and changes to be database independent. You can think of each migration as being a new 'version' of the database."*

Migrations tell your application what goes into your database, and each one is timestamped, so it knows how to walk through them over time. This is crucial, especially when on a team of developers, because it keeps your database up-to-date even when someone else changes it – the computer always has a history of changes via new migration files.

So let's look at a migration that creates our table

```ruby
class CreateArtists < ActiveRecord::Migration
  def change
     create_table :artists do |t|
        t.string :name
        t.string :photo_url
        t.string :nationality

        t.timestamps
     end
  end
end
```

Run the migration with ```rails db:migrate```. That'll fetch any migrations it hasn't run yet and run 'em.

```bash
== 20150710152405 CreateArtistsTable: migrating ===============================
== 20150710152405 CreateArtistsTable: migrated (0.0000s) ======================
```

And we have a table! Nice work!  And _now_ you've got a `schema.rb` file – this file is _sacred_. Not to be touched, only to be admired. It's a snapshot of the current state of your database, and Rails is the only one who should be modifying it, ever.

If ever you're unsure what a database looks like, browse your `schema.rb`.

```ruby
ActiveRecord::Schema.define(version: 20150710152405) do

  # These are extensions that must be enabled in order to support this database
  enable_extension "plpgsql"

  create_table "artists", force: :cascade do |t|
    t.string   "name"
    t.string   "photo_url"
    t.string   "nationality"
    t.datetime "created_at"
    t.datetime "updated_at"
  end

end
```

## Conclusion
- What is ActiveRecord and how does it interact with your database?
- What are migrations?
- Briefly, describe how to configure your Sinatra app to use ActiveRecord.

