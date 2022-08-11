# HTML Links

- HTML links are `hyperlinks`

> a link does not have to be text. A link can be an image or any other HTML element

## HTML Links - Syntax

- `<a>` tag defines a hyperlink
- `<a href="url">link</a>`

- by default, links will appear as follows in all browsers.
1. an unvisted link is underlined an blue.
2. a visited link is underlined and purple.
3. an active link is underlined and red.

> links can of course be styled with CSS, to get another look

## HTML Links - the target Attribute

- by default, the linked page will be displayed in the current window.
- you can change this with `target` attribute
- the `target` specifies where to open the linked document
1. `_self` default
2. `_blank` in a new window or tab
3. `_parent` open the document in the parent frame
4. `_top` open the document in the full body of the window

## Absolute URLs and Relative

```html
<h2>Absolute URLs</h2>
<p><a href="https://www.w3.org/">W3C</a></p>
<p><a href="https://www.google.com/">Google</a></p>

<h2>Relative URLs</h2>
<p><a href="html_images.asp">HTML Images</a></p>
<p><a href="/css/default.asp">CSS Tutorial</a></p>
```

- relative, a link to a page within the same website


## links to an email address

- use `mailto`, it will open the user's email program.

```html
<a href="mailto:someone@example.com">Send email</a>
```

## button as a link

- to use an button as a link, you have to add some javascript code.

```html
<button onclick="document.location='default.asp'"></button>
```
