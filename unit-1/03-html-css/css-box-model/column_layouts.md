# Column Layouts

Very often, we want to create a layout on our page that has columns like so:

![Column | Column](http://kb4dev.com/images/68)

We've already learned two ways to do this! Let's see how `inline-block` and floats compare.

###`inline-block`

`inline-block` puts elements on the same line right? This should be simple. Wait, what? There's a space between them.

<p data-height="265" data-theme-id="0" data-slug-hash="kkkqZv" data-default-tab="css,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/kkkqZv/">Bad bad inline block</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

A quirk of `inline-block` is that your elements are inline, i.e. they are treated like text. This means that if you have any whitespace between the tags in your html, this whitespace also appears in browser. This also applies to **newlines**.

Though there are solutions, none of them are good.