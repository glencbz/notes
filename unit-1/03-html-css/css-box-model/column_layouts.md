# Column Layouts

Very often, we want to create a layout on our page that has columns like so:

![Column | Column](http://kb4dev.com/images/68)

We've already learned two ways to do this! Let's see how `inline-block` and floats compare.

### 1. `inline-block` (not recommended)

Let's give our columns `display: inline-block`. `inline-block` puts elements on the same line right? This should be simple. Wait, what? There's a space between them.

<p data-height="265" data-theme-id="0" data-slug-hash="kkkqZv" data-default-tab="css,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/kkkqZv/">Bad bad inline block</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

A quirk of `inline-block` is that your elements are inline, i.e. they are treated like text. This means that if you have any whitespace between the tags in your html, this whitespace also appears in browser. This also applies to **newlines**.

Though there are solutions, none of them are good. You can either 1. format your html badly (**VERY BAD**) 2. Comment out the newline (**BAD**).

<p data-height="265" data-theme-id="0" data-slug-hash="ZppPjo" data-default-tab="html,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/ZppPjo/">Inline-block fixes</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

If not for that extra space, this method would be simple and intuitive. Unfortunately, we can't remove it without making our code ugly so we will avoid this.

### 2. Floats

What if we just assign our columns `float: left`? Floats can be confusing, but at least they work!

Let's try a more unusual layout, with two columns of `width: 20%` sitting on top of a blue background.

<p data-height="265" data-theme-id="0" data-slug-hash="WGGmaj" data-default-tab="css,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/WGGmaj/">Floats</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

It seems to work just fine, but why does the container need a height? Usually our elements will grow to fit all of the children content.

In this case, our container's content is all floated. When this happens, the container "ignores" the floated content and collapses to `height: 0`. We shouldn't have to set the container height manually, the fix for this is what is known as the **clearfix hack**.

<p data-height="265" data-theme-id="0" data-slug-hash="kkkqzJ" data-default-tab="css,result" data-user="glencbz" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/glencbz/pen/kkkqzJ/">Clearfix</a> by Glen Choo (<a href="http://codepen.io/glencbz">@glencbz</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

This sorcery adds some invisible content to the container to remind it not to collapse. Bear this in mind if you use floats.

### Reference

[W3 on layouts](http://www.w3schools.com/html/html_layout.asp) documents some other methods you can use (as well as the ones listed here).

