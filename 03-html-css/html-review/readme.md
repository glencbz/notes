#HTML

## What is HTML?

> **H**yper**T**ext **M**arkup **L**anguage

At its most fundamental level, HTML is the language that describes the documents you see on the web. Think of HTML as the part that contains the actual data, rather the way the page is presented (CSS) or the logic of the page (Javascript).

## Fundamentals

### HTML elements

HTML documents consist of elements - the things that hold the data. **Different kinds of elements** correspond to **different kinds of data** (`h1` for big headers, `p` for paragraphs, etc). This means that the kind of element you choose doesn't just affect the layout, it actually has meaning!

Most HTML elements consist of content (text and other elements) surrounded by a start tag and an end tag. We could write a small header like so:


<h6>Sample Header</h6>

```html
<h6>Sample Header</h6>
```

There exists exceptions that do **not** need a closing tag (such as the `img` tag). These are known as **void elements**.

<img src="/_assets/ga_cog.png">

```html
<img src="/_assets/ga_cog.png">
```

Elements can be nested (elements can contain elements). **Children** elements are nested under **parent** elements. Nesting allows you to create big elements that contain elements related to each other:

<blockquote>
    <h1>Trump said something again!</h1>
    <p>Build <strong>another</strong> wall?!</p>
</blockquote>


```html
<blockquote>
 <h1>Trump said something again!</h1>
 <p>Build <strong>another</strong> wall?!</p>
</blockquote>
```

### Attributes
Elements often contain attributes, which are key-value pairs. Attributes aren't 'content', they describe the elements themselves (recall the use of the `src` attribute in the `img` tag earlier on). They look like `key="value"` in the start tag:

```html
<div sample-key="sample-value"></div>

<p class="trump-words">Wall?!</p>
```

Two of the most important attributes are `class` and `id`, as we will see later in CSS. Classes describe elements of a certain type and can be reused. Ids uniquely identify elements. Example:

```html
<p class="trump-words" id="tw-1">Build wall! </p>
<p class="trump-words" id="tw-2">More walls!!</p>
```

## Structure of an HTML document

HTML documents have a well-defined structure. Deviating from this structure will almost certainly lead to unintended consequences. 

This little snippet has everything you need for an html document:

```html
<!DOCTYPE html>
<html>
	<head>
	<title>Webpage title</title>
		<meta name="keywords" content="JavaScript"></meta>
	</head>
	<body>
		<h1>My First Heading</h1>
		<p>My first paragraph.</p>
	</body>
</html>
```

A real-world HTML document will usually have many more lines and contain a huge variety of tags. Since many of these tags are simple to understand, we will just cover some of the most important/tricky tags.

### Most important tags

Take special note of these tags. These are tags that are always there and are only declared once!

#### `<!DOCTYPE html>`, DOCTYPE

This statement specifies the markup rules for the page. There are other DOCTYPEs that define [other markup standards](http://www.w3.org/QA/2002/04/valid-dtd-list.html), like XHTML.

You won't need to worry about the other document types for now, so make sure to always use `<!DOCTYPE html>` at the top of a HTML document.

#### `<html>`

These tags contain the entire HTML document. Put everything inside these tags.

#### `<head>`, Head

The `<head>` element contains **hidden** information i.e. the stuff that you don't usually see in the browser. This includes metadata, webpage title and links to other files (such as CSS files). It always appears at the top.

#### `<body>`, Body

The `<body>` element contains the main body of the webpage. This is the content that is rendered and displayed in the browser, i.e. paragraphs, images, etc. It comes after the head.

### Other notable tags

#### `<meta>`, Metadata

Metadata is data about data. In our case, the `<meta>` tag provides metadata about the HTML document. Metadata will not be visible on the webpage, but will be machine parsable. Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata. The metadata can be used by browsers (how to display content or reload the page), search engines (keywords), or other web services.

Some common `<meta>` tags you will see are charset, content, author, and description (for SEO).

#### `<h1>, <h2>... <h6>`, Headings

These tags define headings. Headings can have different levels of importance, `<h1>` being the most important and `<h6>` the least important. 

Browsers will render the text as bigger or smaller depending on how important the heading is. **However**, it is considered bad practice to use these tags just to change the size of the text (you should use CSS to do that).  

#### `<div> and <span>`

These elements are unusual because they are inherently meaningless by themselves, but can be styled using CSS. Hence, they should usually be used for layout and presentation purposes (and not paragraphs, headings, etc).

`<div>`s are:
- block elements (separate from other content)
- usually used to group together related elements

Note how the blue background of the `<div>` covers both of its children elements:

<p data-height="265" data-theme-id="0" data-slug-hash="zKAKVp" data-default-tab="html,result" data-user="glencbz" data-embed-version="2" data-preview="true" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/zKAKVp/">Divs</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

`<span>`s are:
- inline elements (part of other content)
- usually used to distinguish some text from other text

<p data-height="265" data-theme-id="0" data-slug-hash="LRGRwJ" data-default-tab="html,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/LRGRwJ/">Spans</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

#### Lists

There are two kinds of lists: unordered (`<ul>`) and ordered (`<ol>`). A list is composed of the list element itself and children elements called list items (`<li>`).

<p data-height="349" data-theme-id="0" data-slug-hash="XXxpMx" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/XXxpMx/'>Lists</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

#### Tables

<p data-height="268" data-theme-id="0" data-slug-hash="jWeyma" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/jWeyma/'>Tables</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Before CSS became mainstream, websites were designed using tables. Though they are less common now, building tables is still a very useful skill to know. The tags for tables are such:

- `<table>` - create a table
- `<tr>` - create a table row
- `<th>` - create a table heading
- `<td>` - create a table cell
- `<tbody>` - create the body of the table (newer tag)
- `<thead>` - create the head of the table (newer tag). No matter where this is located, whatever is in it will be the first row
- `<tfoot>` - create the foot of the table (newer tag). No matter where this is located, whatever is in it will be the last row

### Forms, Labels, Input Types

####Forms

One of the most common ways to send data to a server is by using a form. A form has two essential attributes, action and method. 

- **Action** - This specifies a route (or url) where you are going to. For example an action of '/test' will take you to the /test route (something you have probably configured in your server side code)

- **Method** - The HTTP Verb that this form will be using (HTML only knows GET and POST, but there are ways to override this default which we will see when we use Node and Rails. The default method is GET so if you are making a GET request you can leave this empty.

####Labels

Labels are text you place before/after inputs to tell the user what the input is for. The `for` attribute allows you to associate a label with its corresponding input. This is helpful for screen readers and users can also click on the label to focus/check the input.

####Input Types

There's a plethora of different input types, specified by a `type` attribute. By default, input elements will allow users to type in text. Take a look at the Codepen below for some examples.

<p data-height="268" data-theme-id="0" data-slug-hash="xZygWo" data-default-tab="result" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/xZygWo/'>Form Elements</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Documentation on input types: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input