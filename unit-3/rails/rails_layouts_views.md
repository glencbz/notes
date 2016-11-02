# Layouts, Partials, and Views

### Objectives
- Describe how templates & views work together
- Use partials for static content and rendering dynamic content

## Views in Rails - Intro

In this lesson we will cover the details of rendering views and best practices for keeping the views DRY.

We've used layouts before in ejs and Express. We define a layout (`layout.ejs`) and then insert the content we want later on. This logic is pretty much the same with Ruby on Rails. When the app is created, Rails will automatically add a layout `application.html.erb` in `app/views/layouts/application.html.erb`.

## Using views with Rails - Demo

In Rails, the logic for the rendering a view is quite straightforward. Given that every route in Rails will execute a method inside a controller, when the method is executed, Rails will look for:

1. A folder inside `views` which has a name that corresponds to the controller's name (`posts` and `PostsController` for example).
2. A file named:  `<method name>.html.erb`.

For example , if we call `http://localhost:3000/posts`, Rails will execute the method `index` in the controller `posts` and then look for a template located in `app/views/posts/index.html.erb`  This works when the method always renders the same template.

In some cases though, you may want to render a template with a different name than the current method. We can specify which template we want to render, let's take a look at this action:

```ruby
def create
  @post = Post.new(post_params)

  respond_to do |format|
    if @post.save
      format.html { redirect_to @post, notice: 'Post was successfully created.' }
    else
      format.html { render :new }
    end
  end
end
```

In the `if` case , we can see that in the code executed in the block `redirect_to @post, notice: 'Post was successfully created.'` This code will redirect the request to the show method. `redirect_to` the `@post` object in rails means "go to the method to show only this object".

In the `else` case, the code executed is `render :new` - this means we're rendering the `new` template, not the `create` template.  This template uses an instance variable `@post`. In this case, it will use the instance variable defined at the start of the create method.

By default, Rails will render the template that has the name of the current method in the controller, unless there is a `render` statement in the method that tells Rails to use a different template.

There are different syntaxes for render, and they all do the same action described above but the rule of thumb is to use the simplest one that makes sense for the code you are writing.

```ruby
render :edit
render action: :edit
render "edit"
render "edit.html.erb"
render action: "edit"
render action: "edit.html.erb"
render "books/edit"
render "books/edit.html.erb"
render template: "books/edit"
render template: "books/edit.html.erb"
render "/path/to/rails/app/views/books/edit"
render "/path/to/rails/app/views/books/edit.html.erb"
render file: "/path/to/rails/app/views/books/edit"
render file: "/path/to/rails/app/views/books/edit.html.erb"
```

## Integrating Layouts - Codealong

Create a new Rails app "views_and_layouts" and scaffold the resource posts:

```bash
rails new views_and_layouts
cd views_and_layouts
rails g scaffold Post title content:text
rake db:migrate
```

Open the posts controller and look at how each method renders the templates: some of them, like index and show, are abstract because the name of the template is the name of the method, but for some other methods, like create or update, we need to explicitly tell Rails what to do at the end of the method.

#### Different Layouts

By default, Rails will render the layout `application.html.erb` - just like `layout.html.erb` in Sinatra - but sometimes, you want to render a template in a different layout.

For instance, let's create a layout called `sidebar.html.erb`

```bash
touch app/views/layouts/sidebar.html.erb
```

Take this template and add it into the `sidebar.html.erb`:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Sidebar Template</title>
</head>
<body>
  <header>
    <h1>My Website</h1>
    <ul>
      <li>Menu 1</li>
      <li>Menu 2</li>
      <li>Menu 3</li>
      <li>Menu 4</li>
    </ul>
  </header>
  <main>
    <%= yield %>
  </main>
  <footer>
    <ul>
      <li>About us</li>
      <li>Team</li>
      <li>Terms and conditions</li>
    </ul>
  </footer>
</body>
</html>
```

Note the yield statement, `<%= yield %>`. Much like the `body` in ejs, this statement defines where our content goes into the layout.

In our application controller, we'll create a controller method `index like so:

```ruby
def index
  render layout: "sidebar"
end
```

This line will just tell Rails to use the same logic of template rendering, but instead of using the default `application.html.erb`, it will render the template inside `sidebar.html.erb`.

#### Using partials

A best practice is to always keep every template as small as possible. A rule of thumb would be to keep shorter than 50 lines, for the sake of readability.

So for example, if your website has a layout with a top menu, the content and then the footer, this should all be in the layout, as it is rendered on every page.  But if all this html is in one file, the layout will end up being 200+ lines of code.

When this happens, you should think about splitting the template into partials. Partials are just chunks of a template that will be rendered into another one, like children of the layout.

This layout in `sidebar.html.erb` will soon be too long and unreadable, thus we need to split into different parts:

Create a new file:

```bash
mkdir app/views/application
touch app/views/application/_header.html.erb
```

And inside move the following from `sidebar.html.erb`:

```erb
<header>
  <h1>My Website</h1>
  <ul>
    <li>Menu 1</li>
    <li>Menu 2</li>
    <li>Menu 3</li>
    <li>Menu 4</li>
  </ul>
</header>
```

Now let's create another file:

```bash
touch app/views/application/_footer.html.erb
```

And inside move the following from `sidebar.html.erb`:

```erb
<footer>
  <ul>
    <li>About us</li>
    <li>Team</li>
    <li>Terms and conditions</li>
  </ul>
</footer>
```

Now the main `sidebar.html.erb` file is back to a normal size, we just need to include the partials and the final result will then be the same than before.

**Note:** Every partial needs to have an underscore as the first character - this way Rails knows that it is not a proper template but only a partial that will be included in a template.

Let's now call the partials in the layout:

```erb
<!DOCTYPE html>
<html>
<head>
  <title>Sidebar Template</title>
</head>
<body>
  <%= render "header" %>
  <main>
    <%= yield %>
  </main>
  <%= render "footer" %>
</body>
</html>
```

Rails will automatically look in the folder `app/views/application/` for a file that is called by the name given to the method `render` with an underscore prefix.

##Independent Practice

Create a Rails app called `fanzine`. This app will have a controller called `home` and four routes called:

- Homepage
- Info
- About
- redirect_home

You'll have to match these routes with these templates:

- Homepage renders the template "homepage"
- Info renders the template "information"
- About renders the template "about"
- redirect_home redirect the request to "/homepage"

This app only has one layout, but the layout should have a menu with links to the four routes. These links should be inside a partial called `menu` and the file should be in `app/views/application`. The menu should appear on every page.

## Conclusion

#### Questions

- Where do we use the method `render` (2 places)
- What is the easiest way to go to the show page of a restful controller from another method in this controller?
- How to render a different layout only for one method?
