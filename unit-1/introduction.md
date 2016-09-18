# Intro To jQuery

### Objectives
*After this lesson, students will be able to:*

- Describe jQuery and the context to use it
- Include jQuery in your projects
- Practice using jQuery selectors


### Preparation
*Before this lesson, students should already be able to:*

- Use vanilla JavaScript to manipulate the DOM
- Use a text editor
- Explain CSS selectors

## jQuery - Intro (5 mins)

#### What is jQuery?
jQuery is a 3rd-party library that is intended to make front-end development tasks — particularly those involving DOM selection and manipulation — easier, faster, and more fun.

##### But wait, what do we mean by 'library'?
We've already seen that we can make our jobs easier and faster by using Node modules (AKA libraries) in our apps.

**A `library`** is just a collection of reusable methods that serve a particular purpose.


#### So, as a library, what does jQuery offer us?

jQuery helps us manipulate the DOM, allowing us to perform complex manipulations using less code with less hassle.  jQuery's syntax was developed to mimic CSS selector syntax, making code easier to develop, read, and manage; also, the syntax is more concise, and jQuery solves many cross-browser compatibility issues for us.

## Using jQuery - Demo (5 mins)

#### Installation
jQuery is a client side library, which means we need to include it in our HTML. To do this, we have two options:

1. Reference jQuery from a server on the internet:

- Directly from jQuery's website (http://code.jquery.com/)
`<script src="http://code.jquery.com/jquery-1.11.1.min.js"></script>`
From a CDN (content delivery network) like [CDNJS](https://cdnjs.com/) or [Google Hosted Libraries](https://developers.google.com/speed/libraries/)


`<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>`

2. Download a copy of jQuery to host on your own server:

[CDNJS](http://www.cdnjs.com), [Google Hosted Libraries](https://developers.google.com/speed/libraries/), and the [jQuery site](http://www.jquery.com) will all allow you to download a copy of jQuery to include in your projects.

#### What's with the 'min.js' in the name of the jQuery file?

If you look carefully at the filenames of the jQuery versions you download, or just look at the URL in the "src" attribute for each script tag above, you'll notice something at the end of each file name — namely, that they end in 'min.js'. This means the JavaScript code has been minified.

## Minified? Did I read that right? Discussion (10 mins)

Yep. You did. Minification is the process of making a JavaScript file smaller by, among other things, removing all line breaks and whitespace, reducing the length of variable and function names, and stripping out all comments. Minification can significantly reduce the size of a JavaScript file, and in turn, significantly decrease the time it takes our browsers to load the file into memory.

In jQuery's 1.11.1's case, the original unminified code is about 276 kilobytes, whereas the minified code is only 94 kilobytes. That makes the minified version **one-third** the size of the original - not bad!

Minified scripts can be difficult to read, so most servers that host jQuery and other libraries will also offer the original (non-minified) version of the code so developers can understand the code.

Minification is performed on a JavaScript when it's ready for release and there are many options for doing this. If you'd like to minify your own scripts, try a Google search to check out the various options. Or, you can try the [Closure Compiler from Google](https://developers.google.com/closure/compiler/) which runs locally on your computer like any other piece of software you might use as a developer.

Also, if you do happen to come across a library where you can't find a non-minified version to look at, software also exists to decompress a minified script. These are usually called unminifiers, pretty-printers, or beautifier). They take a minified JavaScript and attempt to decompress it, making it easier to read and understand.

**Even if you don't fully understand the code, it's a good exercise to visit code.jquery.com and take a look at minified and non-minified jQuery.**

#### And one more thing: 1.x vs. 2.x jQuery

If you've visited code.jquery.com, you'll see that there are two major versions in development:
  - The 1.x branch is the most cross-browser-compatible version of the jQuery core
  - The 2.x branch, while offering some new features, is not compatible with older web browsers — most notably, it's not compatible with Internet Explorer versions 8 and below
