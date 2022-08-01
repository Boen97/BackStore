# Html Basics

```html
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>My First Heading</h1>
<p>My first paragraph.</p>

</body>
</html>
```

- The `<head>` element contains `meta information` about the HTML page
- <body> is a container for all the visible contents

## The <!DOCTYPE> Declaration

- helps browsers to display web page correctly
- must appear once, at the top of the page
- not case sensitive
- `<!DOCTYPE html>` declaration for `HTML5`

## HTML Elements

- The HTML element is everything from the start tag to the end tag:
- <br> have no content, these elements are called empty elements
- Empty elements do not have an end tag!

## <html>

- The <html> element is the root element and it defines the whole HTML document.

## HTML is Not Case Sensitive

- <P> means the same as <p>.
- W3C recommends lowercase in HTML
- demands lowercase for stricter document types like XHTML.

## <img> tag with `width` and `height` attributes

- specifies the width and height of the image (in pixels)

```html
<img src="img_girl.jpg" width="500" height="600">
```

## the `lang` attributes

```html
<!DOCTYPE html>
<html lang="en">
<body>
...
</body>
</html>
```

- you should always include the `lang` attributes inside the `<html>` tag
- it declares the language of the web page
- this is meant to assist search engines and browsers

- `country codes` can also be added to the language code in the `lang` attributes
- `<html lang="en-US">` or `<html lang="zh-CN">`
- the first two `en` define the language of the HTML page
- the last two `US` define the country

### Chinese language code

1. Chinese zh
2. English en
3. Chinese Simplified zh-Hans
4. Chinese Simplified zh-Hant

### Country Codes

1. UNITED STATES (US)
2. CHINA (CN)

## Always Quote Attributes Values

## Single or Double Quotes of Attributes Values

- Double quotes around attribute values are the most common in HTML, but single quotes can also be used.
- when the attribute value itself contains double quotes, it is necessary to use single quotes, or vice versa.
