# HTML CSS

# HTML Recap

Front-end or Client-side web development is dominated by 3 'languages' HTML, CSS and Javascript. You will use these all the time. HTML is about defining the structure or a document. CSS is about the design and presentation of it, and Javascript is about control the behaviours of it. We'll cover all three but first let's focus on HTML.

#### What is HTML?

* Stands for Hyper Text Markup Language

* Currently at Version 5 \(as of October 2014\)

* Made up of tags \(opening and closing usually\), which in turn create elements


```html

&lt;!-- This whole thing is an element --&gt;

&lt;tagname attribute="attribute\_value"&gt;&lt;\/tagname&gt;

&lt;!-- A paragraph tag with two classes, could be selected in CSS using p.default-paragraph.another-class {} --&gt;

&lt;p class="default-paragraph another-class"&gt;Some content in here&lt;\/p&gt;

```

#### What does an HTML document need?

```html

&lt;!doctype html&gt; &lt;!-- Always have this - it describes which version of HTML you are using --&gt;

&lt;html lang="en"&gt;

&lt;head&gt;

&lt;!-- This is the meta data of the page, often invisible --&gt;

&lt;meta charset="utf-8"&gt;

&lt;title&gt;This is a Web Page&lt;\/title&gt;

&lt;\/head&gt;

&lt;body&gt;

&lt;!-- This is where the actual content is --&gt;

&lt;\/body&gt;

&lt;\/html&gt;

```

#### Common Elements

```html

&lt;!-- Heading Tags - getting less important the higher the number --&gt;

&lt;h1&gt;&lt;\/h1&gt;

&lt;h2&gt;&lt;\/h2&gt;

&lt;h3&gt;&lt;\/h3&gt;

&lt;h4&gt;&lt;\/h4&gt;

&lt;h5&gt;&lt;\/h5&gt;

&lt;h6&gt;&lt;\/h6&gt;

&lt;p&gt;&lt;\/p&gt; &lt;!-- A paragraph tag --&gt;

&lt;!-- An HTML element can have attributes. Attributes are key value pairs \(just like javascript objects\) that provide additional information. They look like this. --&gt;

&lt;a href="generalassemb.ly"&gt;General Assembly&lt;\/a&gt;

&lt;img src="" \/&gt;

&lt;video src=""&gt;&lt;\/video&gt;

&lt;br \/&gt; &lt;!-- a new line --&gt;

&lt;hr \/&gt; &lt;!-- a horizontal line --&gt;

&lt;button&gt;&lt;\/button&gt;

&lt;input \/&gt;

&lt;pre&gt;&lt;\/pre&gt; &lt;!-- Preformatted text --&gt;

&lt;code&gt;&lt;\/code&gt;

&lt;textarea&gt;&lt;\/textarea&gt;

&lt;ul&gt; &lt;!-- Unordered list --&gt;

&lt;li&gt;&lt;\/li&gt; &lt;!-- List item --&gt;

&lt;\/ul&gt;

&lt;ol&gt; &lt;!-- Ordered list --&gt;

&lt;li&gt;&lt;\/li&gt;

&lt;\/ol&gt;

&lt;div&gt;&lt;\/div&gt; &lt;!-- A division, this is just a way to group content --&gt;

&lt;section&gt;&lt;\/section&gt;

&lt;article&gt;&lt;\/article&gt;

&lt;aside&gt;&lt;\/aside&gt;

&lt;header&gt;&lt;\/header&gt;

&lt;footer&gt;&lt;\/footer&gt;

&lt;main&gt;&lt;\/main&gt;

&lt;nav&gt;&lt;\/nav&gt;

&lt;!-- etc. --&gt;

````

#### DOM (Document Object Model)

One last point we shall mention briefly is the DOM or Document Object Model. The DOM is technically an API for representing and interacting with elements in HTML. The easiest way to think about this is that HTML is the language we used to describe what we want, the DOM is the object created to then represents that in memory, in a tree like structure. Later we'll talk about manipulating the DOM and what we mean is changing the structure of the pages we defined in out HTML.

!\[\]\(https:\/\/www.w3.org\/TR\/DOM-Level-2-Core\/images\/table.gif\)

For more information, see \[here\]\(https:\/\/developer.mozilla.org\/en\/docs\/Web\/HTML\/Element\).

#### Resources:

* [http://www.w3schools.com/html/](http://www.w3schools.com/html/)

