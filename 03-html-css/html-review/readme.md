#HTML

### What is HTML?

> **H**yper**T**ext **M**arkup **L**anguage

At its most fundamental level, HTML is the language that describes the documents you see on the web. Think of HTML as the part that contains the actual data, rather the way the page is presented (CSS) or the logic of the page (Javascript).

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

Elements can be nested (elements can contain elements). Nesting allows you to create big elements that contain elements related to each other:

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
Elements often contain attributes, which are key-value pairs. They   look like `key="value"` in the start tag:

```html
<div data-attribute="5"></div>

<p class="trump-words">Wall?!</p>
```



Some of the more important attributes are `class` and `id`, which we will see later in CSS. Just know that class names can be used in more than one element, but ids must be unique. See below.

```html
<div class="general-container"></div>
<div class="general-container"></div>
<span class="general-container"></span>

<div id="specific-container"></div>
```

## Going through a HTML document

### What is `<!DOCTYPE html>`?

This statement specifies the markup rules for the page. There are other DOCTYPEs that define [other markup standards](http://www.w3.org/QA/2002/04/valid-dtd-list.html), like XHTML.

You won't need to worry about the other document types for now, so make sure to always use `<!DOCTYPE html>` at the top of a HTML document.

### The ```<html></html>``` tags

These tags tell the browser we're beginning a HTML document. Put everything inside these tags.

### The ```<head>``` tags

The `<head></head>` tags is where hidden information about the document goes. This includes metadata, the title of the webpage (which appears in the browser), links to CSS and possibly JavaScript files. The head goes at the top of the page, and is declared only once.

### Meta Tags

Metadata is data (information) about data. The <meta> tag provides metadata about the HTML document. Metadata will not be visible on the webpage, but will be machine parsable. Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata. The metadata can be used by browsers (how to display content or reload the page), search engines (keywords), or other web services.

Some common meta tags you will see are charset, content, author, and description (for SEO).

### The ```<body>``` tags

The `<body></body>` tags denote the content of the document. This content is rendered and displayed in the browser.

### Divs + Spans

HTML provides for us two 'empty' containers to store whatever content we want. One is a div (block element) and the other is a span (inline element)

<p data-height="388" data-theme-id="0" data-slug-hash="qbJREg" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/qbJREg/'>Divs vs Spans</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### Text Tags

<p data-height="514" data-theme-id="0" data-slug-hash="NxOddg" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/NxOddg/'>Text Tags</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### Lists

<p data-height="349" data-theme-id="0" data-slug-hash="XXxpMx" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/XXxpMx/'>Lists</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### Tables

<p data-height="268" data-theme-id="0" data-slug-hash="jWeyma" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/jWeyma/'>Tables</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Before CSS became mainstream, websites were designed using tables. Although they are much less frequently used, building tables is still a very useful skill to know. The tags for tables are such:

* `<table></table>` - create a table
* `<tr></tr>` - create a table row
* `<th></th>` - create a table heading
* `<td></td>` - create a table cell
* `<tbody></tbody>` - create the body of the table (newer tag)
* `<thead></thead>` - create the head of the table (newer tag). No matter where this is located, whatever is in it will be the first row
* `<tfoot></tfoot>` - create the foot of the table (newer tag). No matter where this is located, whatever is in it will be the last row

### Practice Creating Tables

Clone the repo and open instructions.html in your browser. Edit the basic data provided in skeleton.html to create a webpage that looks like the solution picture shown in the instructions.

https://github.com/WDI-SEA/html_top_ten_movies_table

### Images and Links

<p data-height="268" data-theme-id="0" data-slug-hash="NxOdgv" data-default-tab="html" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/NxOdgv/'>Images and Links</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### Forms, Labels, Input Types

####Forms

One of the most common ways to send data to a server is by using a form. A form has two essential attributes, action and method.

* **Action** - This specifies a route where you are going to. For example an action of '/test' will take you to the /test route (something you have probably configured in your server side code)

* **Method** - The HTTP Verb that this form will be using (HTML only knows GET and POST, but there are ways to override this default which we will see when we use Node and Rails. The default method is GET so if you are making a GET request you can leave this empty.

####Labels

Labels are text you place before/after inputs to tell the user what the input is for. The for attribute is for screen readers and if the ID of the input matches the ID of the for attribute then you can click on the label and have it automatically focus/check the input.

####Input Types

By default, input elements will allow users to type in text. There's also a plethora of different input types, specified by a `type` attribute. Take a look at the Codepen below for some examples.

<p data-height="268" data-theme-id="0" data-slug-hash="xZygWo" data-default-tab="result" data-user="bhague1281" class='codepen'>See the Pen <a href='http://codepen.io/bhague1281/pen/xZygWo/'>Form Elements</a> by Brian Hague (<a href='http://codepen.io/bhague1281'>@bhague1281</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Documentation on input types: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input

### User Input Practice

Clone the following repo and open instructions.html in your browser. Your goal is to work to turn the basic skeleton.html page into a webpage meeting the requirements described in the instructions that looks like the picture shown in solution.png. Good luck!

https://github.com/WDI-SEA/html_user_inputs
