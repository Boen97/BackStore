# HTML Styles - CSS

- CSS stands for `Cascading Style Sheets`
- CSS saves a lot of work, it can control the layout of multiple web pages all at once.

## What is CSS

- Cascading Style Sheet (CSS) is used to format the layout of a webpage

> the word `cascading` means that a style applied to a parent element will alsp apply to all children
> unless you specify something else.

## Using CSS

- CSS can be added to HTML documents in 3 ways:

1. Inline
   `style` attribute
2. Internal
   by using a `<style>` element in the `<head>` section
3. External
   by using a `<link>` element to link to an external CSS file

> the most common way to add CSS, is to keep the styles in external CSS files

### Internal CSS

- an internal CSS is used to define a style for a single HTML page.
- defined in the `head` section within a `style` element

```html
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

## External CSS

- an external CSS is used to define the style of many HTML pages.
- add a link in the `head` section for each HTML page.

```html
<!DOCTYPE html>
<html>
<head>
    <link ref="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

- the external css file must be saved with a `.css` extension
- External style sheets can be referenced with a full URL or with a path relative to the current web page.

```html
<link rel="stylesheet" href="https://www.w3schools.com/html/styles.css">
<!-- links to locate in the html folder on the current web site -->
<link rel="stylesheet" href="/html/styles.css">
<!-- in the same folder as the current page -->
<link rel="stylesheet" href="styles.css">
```

