# HTML from first principles

1/31/2020

# TLDR

HTML is a simple but powerful language. It allows you to package up and give a name to parts of your application. Master its fundamentals now, and save yourself a world of confusion later.

HTML can be understood with the following major concepts:

* Elements
* Opening tags
* Closing tags
* Content
* Attributes
* Parents
* Children
* Siblings

Once you master the fundamentals of HTML as a language, you can start using the [many elements that already exist](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) to create applications.

# First principles

First principles are powerful. They give you the fundamental knowledge necessary to build complex solutions. Remember, complex concepts are built on simpler concepts. Skimp on your understanding of the first principles and suffer the consequences. Do not underestimate their power.

We will now explore the first principles of HTML.

# HTML

HTML stands for HyperText Markup Language. With a simple syntax, it allows you to give names to parts of your application. Those names grant access to various functionality. Some of this functionality will be predetermined, but some you can create yourself.

The following is an example HTML program, meant to be run in a web browser:

```html
<!DOCTYPE html>

<html>
  <head>
    <title>Hello people</title>
  </head>

  <body>
    <h1 style="color: blue">Hello people!</h1>
  </body>
</html>
```

You can view this running live [here](https://lastmjs.github.io/html-from-first-principles-example/). You can see the code repository [here](https://github.com/lastmjs/html-from-first-principles-example).

Let's break this program down, focusing on the most fundamental parts of the HTML language.

# Elements

The most fundamental part of the HTML language is the element. Our example program has multiple elements in it. Can you name them? Their names are as follows: `html`, `head`, `title`, `body`, and `h1`. Those are just the names though. To create an element correctly you must combine the name with opening and potentially closing tags, like this: `<html></html>`, `<head></head>`, `<title></title>`, `<body></body>`, and `<h1></h1>`.

The `<!DOCTYPE html>` is not an element, but a declaration that the browser uses for its own internal purposes. You should put `<!DOCTYPE html>` at the top of any HTML document that you expect to run in a modern web browser.

But what are elements? Elements are containers. They contain functionality, usually some visualization and some behavior to go along with that visualization. There are many elements. You can learn about them [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) or [here](https://www.w3.org/TR/2012/WD-html-markup-20121025/elements.html).

I'll explain what the elements in our example program do:

* `<html></html>`
  * This element is the main container of our application. Everything else must go inside of this element
* `<head></head>`
  * This element contains information about the HTML document that is generally not displayed with the main content of our application
* `<title></title>`
  * This element changes the text in the title bar or tab of the browser
* `<body></body>`
  * This element contains all content that will be displayed 
* `<h1></h1>`
  * This element creates the most prominent heading a browser can produce. Essentially it makes text look big and important

Like I said earlier, there are many more elements. You can even [create your own](https://developers.google.com/web/fundamentals/web-components/customelements).

## Opening tags

Every HTML element has an opening tag. For the `html` element in our example program, the opening tag looks like this: 

```html
<html>
```

All opening tags have an opening angle bracket `<`, followed by the name of the element, followed by a closing angle bracket `>`.

## Closing tags

Closing tags on elements are sometimes optional, sometimes required, and sometimes forbidden. It just depends on the element. For the `html` element in our example program, the closing tag looks like this: 

```html
</html>
```

All closing tags have an opening angle bracket `<`, followed by a forward slash `/`, followed by the name of the element, followed by a closing angle bracket `>`. All of the elements in our example program traditionally have closing tags. Some that don't include `input`, `img`, and `meta`.

## Content

Anything between the opening tag and closing tag of an element is its content. Content can include text or even other elements. Let's look at the `title` element from our example program: 

```html
<title>Hello people</title>
```

Hmmm...looks like the content is `Hello people`. What about the `head` element? It looks like this:

```html
<head>
  <title>Hello people</title>
</head>
```

The content in this case is `<title>Hello people</title>`. It includes an entire element with that element's own content as well.

## Attributes

HTML opening tags may be decorated with attributes to provide extra functionality to an element. Attributes should only be written within opening tags. Let's look at the `h1` element from our example program:

```html
<h1 style="color: blue">Hello people!</h1>
```

It has one attribute. It looks like this: `style="color: blue"`. Its name is `style` and its value is `"color: blue"`. Can you guess what it does? That's right! It changes the color of any text within the `h1` element to blue.

All attributes start with a name, followed by an equals sign `=`, followed by a value within double quotes. You may put more than one attribute inside of an opening tag.

# Parents, children, and siblings

HTML elements exist in a hierarchical relationship with other elements. It is helpful to think of this in terms of a tree, a family tree even. The first element in an HTML program, the `html` element, is the root or parent of all other elements. If you look at our example program, you will notice that all of the other elements are inside of the content of the `html` element.

All of the elements immediately inside of the `html` element are its immediate children. Can you name the immediate children of the `html` element? They are: `head` and `body`.

`head` and `body` are siblings to each other, because they are at the same level within their parent, which is `body`.

`head` has one child, it is `title`. `title` has no siblings and no children. 

`body` has one child, it is `h1`. `h1` has no siblings and no children.

If you want to, you can extend the family relationship analogy even further: `html` has two grandchildren, `title` and `h1`. I'm not sure that extending the analogy to cousins, great uncles, etc is useful, but feel free.

Here's our example program again, with the hierarchical relationships defined:

```html
<!DOCTYPE html>

<!--html is the parent of all elements within it-->
<html>
  <!--head's parent is html, its one sibling is body and it has one child-->
  <head>
    <!--title's parent is head, it has no siblings and no children-->
    <title>Hello people</title>
  </head>

  <!--body's parent is html, its one sibling is head and it has one child-->
  <body>
    <!--h1's parent is body, it has no siblings and no children-->
    <h1 style="color: blue">Hello people!</h1>
  </body>
</html>
```

# Conclusion

Learn HTML. Learn its fundamentals. Understand elements, opening tags, closing tags, content, attributes, and the hierarchical relationship of all elements (parents, children, and siblings). Understanding these things will make you a powerful steward of the digital world.

# Paid mentorship

I love to teach for understanding. Reach out if you are in need of a web development mentor: jordan.michael.last@gmail.com