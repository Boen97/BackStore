# HTML Paragraphs

- a paragraph always start a newline, and is usually a block of text.
- browsers automatically add some white space (a margin) before and after a paragraph

## HTML Display

- you cannot be sure how HTML will be displayed
- large or small screens, and resized windows will create different results.
- With HTML, you cannot change the display by adding extra spaces or extra lines in your HTML code.
- `The browser will automatically remove any extra spaces and lines when the page is displayed:`

```html
<p>
This paragraph
contains a lot of lines
in the source code,
but the browser
ignores it.
</p>

<p>
This paragraph
contains         a lot of spaces // space will be ignored
in the source         code,
but the        browser
ignores it.
</p>
```

## <hr> HTML Horizontal Rules

- `<hr>` defines a thematic break in an HTML page, and is most often displayed as a horizontal rule.
- the `<hr>` element is used to separate content (or define a change) in an HTML page.
- the `<hr>` tag is an empty tag, which means that it has no end tag.

## HTML Line Breaks

- The HTML `<br>` element defines a line break.
- Use `<br>` if you want a line break (a new line) without starting a new paragraph

## The Poem Problem

- This poem will display on a single line:

```html
<p>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
</p>
```

### Solution - The HTML <pre> Element

- the HTML `<pre>` element defines `preformatted text`.
- the text inside a `<pre>` element is displayed in a fixed-width font, and it preserves both spaces and line breaks

```html
<pre>
  My Bonnie lies over the ocean.

  My Bonnie lies over the sea.

  My Bonnie lies over the ocean.

  Oh, bring back my Bonnie to me.
</pre>
```
