Easy stuff --- 
- Tags
- Attributes
- inline styles(bg colour, fonts, etc)
hard stuff ---- 
- external styles, classes, ids
- flexbox css
- connecting js to html(selectors, DOM)
- chrome dev tools
## Basic terminology

- **Tag** - A tag is a piece of text that is enclosed in angle brackets. It is used to define the structure of an HTML document.
- **Attribute** - An attribute is a piece of text that is placed inside the opening tag of an HTML element. It is used to provide additional information about the element.
- **Element** - An element is a piece of text that is enclosed in angle brackets and can have attributes. It is used to define the content of an HTML document.

## HTML tags for text

- `<p>` - Paragraph
- `<span>` - Span
- `<div>` - Div
- `<a>` - Anchor
- `<img>` - Image
- `<br>` - Break
- `<hr>` - Horizontal rule
- `<b>` - Bold
- `<i>` - Italic
- `<u>` - Underline
- `<strong>` - Strong
- `<em>` - Emphasis
- `<code>` - Code
- `<pre>` - Preformatted text

## HTML tags for lists

- `<ul>` - Unordered list
- `<ol>` - Ordered list
- `<li>` - List item

## HTML tags for tables

- `<table>` - Table
- `<tr>` - Table row
- `<td>` - Table cell

## HTML tags for forms

- `<form>` - Form
- `<input>` - Input field
- `<textarea>` - Text area
- `<select>` - Select box
- `<option>` - Option
- `<button>` - Button

## HTML tags for images

- `<img>` - Image
- `<source>` - Source
- `<picture>` - Picture
- `<video>` - Video

## HTML tags for links

- `<link>` - Link
- `<meta>` - Meta
- `<link rel="stylesheet">` - Stylesheet
- `<link rel="icon">` - Icon

## HTML tags for scripts

- `<script>` - Script
- `<script src="script.js"></script>` - Script with src
- `<script async src="script.js"></script>` - Script with async and src
- `<script defer src="script.js"></script>` - Script with defer and src
- `<script type="module" src="script.js"></script>` - Script with type module and src

## HTML tags for meta tags

- `<meta charset="utf-8">` - Charset
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` - Viewport
- `<meta name="description" content="Description">` - Description
- `<meta name="author" content="Author">` - Author
- `<meta name="keywords" content="Keywords">` - Keywords
- `<meta name="robots" content="index, follow">` - Robots
- `<meta name="googlebot" content="index, follow">` - Googlebot

## HTML tags for media

- `<audio>` - Audio
- `<video>` - Video
- `<source>` - Source
- `<track>` - Track
- `<iframe>` - Iframe
- `<embed>` - Embed
- `<object>` - Object

## Attributes for HTML tags

### Attributes examples

```html
<p id="my-id" class="my-class">
	Hello world
</p>
<img src="image.jpg" alt="Image">
<a href="https://www.google.com">Google</a>
<input type="text" placeholder="Enter your name">
<button>Click me</button>
```

- `id="my-id"` - Adds an `id` attribute with the value `my-id`
- `.my-class` - Adds a `class` attribute with the value `my-class`
- `src="image.jpg"` - Adds a `src` attribute with the value `image.jpg`
- `alt="Image"` - Adds an `alt` attribute with the value `Image`
- `href="https://www.google.com"` - Adds a `href` attribute with the value `https://www.google.com`
- `type="text"` - Adds a `type` attribute with the value `text`
- `placeholder="Enter your name"` - Adds a `placeholder` attribute with the value `Enter your name`

Some attributes are global attributes and can be used on any HTML tag. Some attributes are specific to certain tags and can only be used with that tag. For example, the `href` attribute is a specific attribute for the `<a>` tag, and the `title` attribute is a global attribute that can be used on any HTML tag.

### HTML5 attributes

Some examples of HTML5 attributes are:

- `autofocus` - Adds an `autofocus` attribute to an input field
- `required` - Adds a `required` attribute to an input field
- `readonly` - Adds a `readonly` attribute to an input field
- `section` - Adds a `section` attribute to a section element
- `footer` - Adds a `footer` attribute to a footer element

> footer, section, and header are new HTML5 attributes. They are used to define the structure of a web page. Fundamentally, they are used to group related content together, just like the `<div>` tag is used to group related content together.

## HTML5 tags

- `<header>` - Header
- `<footer>` - Footer
- `<nav>` - Navigation
- `<main>` - Main
- `<article>` - Article
- `<section>` - Section
- `<aside>` - Aside
- `<details>` - Details
- `<summary>` - Summary
- `<time>` - Time
- `<mark>` - Mark
- `<meter>` - Meter
- `<progress>` - Progress
- `<video>` - Video
- `<audio>` - Audio
- `<source>` - Source

---
---
# CSS

cascading style sheets

common styling attributes - 
- font-size
- color  
	  - gives font colour to the text
- background
	  - gives bacground colour to the element
- border-radius
	  - rounded border shapes
- border
	  - this tells how the border is 
	    border: 1px solid black // gives a solid black border
	    border: 1px dotted black // gives a dotted black border
- padding 
		- space from the top or bottom; // inside the div
		- 
- margin
	  - space added outside the div
	    margin: 50px;
	    // means outside the div element 50px will be added to the top to the right, left , bottom
- box-shadow
	  - gives shadow to the box element

Example of the code --
```css
<h1 style= "
font-size: 100px;
color: red;
background: aqua; 
border-radius: 10px; 
padding: 10px; 
margin: 20px;
box-shadow: 2px 10px 10px black;
">
hi there ;
</h1>
```

previously we position elements by using padding 
padding-left = 10px
padding-right = 20 px
this are the not the optimum ways so we use

- flexbox
- grid
  

---
---
# Emmit

Emmit is a code snippets manager for VS Code. It is used to create HTML code faster. Emmit is a must-have tool for any web developer. In VS Code, Emmit is enabled by default. It works only after you have created a new HTML file.

> Learn the shortcuts and just press the tab or enter key to get the code you want.

## Some common Emmit shortcuts

- `!` - Inserts a `<!DOCTYPE html>` tag
- `h1` - Inserts a `<h1>` tag
- `h2` - Inserts a `<h2>` tag
- `p` - Inserts a `<p>` tag
- `img` - Inserts an `<img>` tag
- `a` - Inserts an `<a>` tag
- `ul` - Inserts an `<ul>` tag
- `ul>li` - Inserts a `<li>` tag inside an `<ul>` tag
- `ul>li>a` - Inserts an `<a>` tag inside a `<li>` tag inside an `<ul>` tag
- `ul>li*3` - Inserts 3 `<li>` tags inside an `<ul>` tag
- `div` - Inserts a `<div>` tag
- `div>p` - Inserts a `<p>` tag inside a `<div>` tag
- `div>p*3` - Inserts 3 `<p>` tags inside a `<div>` tag

### ID and Class

- `#` - Inserts an `id` attribute
- `.` - Inserts a `class` attribute

Example:

- `#my-id` - Inserts an `id` attribute with the value `my-id`
- `.my-class` - Inserts a `class` attribute with the value `my-class`

### Grouping

- `div>(header>ul>li*2>a)+footer>p` - Inserts a `<div>` tag with a `<header>` tag inside it, a `<ul>` tag inside it, and 2 `<li>` tags inside the `<ul>` tag. Then it inserts an `<a>` tag inside each `<li>` tag. Finally it inserts a `<footer>` tag and a `<p>` tag inside it.

> Yep, it can go little bit crazy. But you don’t have to worry about it. Rarely you will need to use it.

### CSS shortcuts

- `style` - Inserts a `<style>` tag
- `pos` - Inserts a `position` property
- `pos:absolute` - Inserts a `position` property with the value `absolute`
- `bgc` - Inserts a `background-color` property
- `bgc:red` - Inserts a `background-color` property with the value `red`
- `ma` - Inserts a `margin:auto` property

