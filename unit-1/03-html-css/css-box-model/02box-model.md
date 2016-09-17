# The Box Model

All HTML elements can be considered boxes. Even if you see a circle, it's living within a box. This is what we refer to as the CSS box model: all HTML elements are wrapped in rectangular boxes. Understanding the different parts of the box model is essential to creating the layouts that you want!

The image below illustrates the four parts of the box model (you can see this in your dev tools):

![box-model](http://s6.postimg.org/gi8r6c341/css_box_model.png)

_From [www.theslate.org](http://www.theslate.org)_

These parts are:

- **Content** - the content of your element, where text and images appear
- **Padding** - the area between the content and the border; possesses the element's background color
- **Border** - a border that goes around the padding and content; possesses the element's background color (but usually has its own background color)

* **Margin** - clears an area around the border; the margin does not have a background color, it is completely transparent (because it is **outside the element**)

By default, when you specify a `height` or `width` in CSS, this applies only to the height or width of the content. This is actually a CSS property: `box-sizing: content-box` and can lead to some very unexpected results.

The remedy to this is the CSS property `box-sizing`. `box-sizing: border-box` causes the `height` and `width` to include everything up to the border. To see how intuitive this is over the default `box-sizing: content-box`, we'll refer to http://www.w3schools.com/cssref/tryit.asp?filename=trycss3_box-sizing2. Notice that even though we have two elements `width: 50%`, we still require `border-box` to make the elements sit nicely together. 



## Parts of the Box Model

#### Margin

The margin is the space around the element. The larger the margin, the more space between our element and the elements around it. We can adjust the margin to move our HTML elements closer to or farther from each other.

Let's start with our margins. Adjusting our margins not only moves our element relative to other elements on the page but also relative to the "walls" of the HTML document.

For instance, if we take an HTML element with a specific width (such as our `<div>` in the editor) and set its margin to `auto` - this tells the document to automatically put equal left and right margins on our element, centering it on the page.

If you want to specify a particular margin, to a particular side, you can do it like this:

```css
div {
  margin-top: /*some value*/;
  margin-right: /*some value*/;
  margin-bottom: /*some value*/;
  margin-left: /*some-value*/;
}
```

You can also set an element's margins all at once: you just start from the top margin and go around clockwise (going from top to right to bottom to left). For instance,

```css
div {
  margin: 1px 2px 3px 4px;
}
```

You can do top-bottom and left-right:

```css
div {
  margin: 0 auto;
}
```

Automatic left-right margins is actually a handy trick used to horizontally center elements.

#### Border

The border is the edge of the element. It's what we've been making visible every time we set the border property.

Borders can be set in two ways, just like your margins and just like we've talked about previously.

```css
div {
  border: 5px solid black;
}

/* OR */

div {
  border-width: 5px;
  border-style: solid;
  border-color: black;
}
```

#### Padding and Content

The padding is the spacing between the content and the border. We can adjust this value with CSS to move the border closer to or farther from the content.

Padding can be set in two ways, just like your margins.

```css
div {
  padding: 2px;
}

/* OR */

div {
  padding-top: 3px;
  padding-right: 1px;
  padding-bottom: 0px;
  padding-left: 9px;
}

/* OR */

div {
  padding: 3px 1px 0 9px;
}
```


Padding becomes more apparent when we have "stuff" inside the box.
