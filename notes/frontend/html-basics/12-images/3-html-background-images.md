# HTML Background Images

a background image can be specified for almost any HTML element

```css
p {
    background-image: url('1.png');
}
```


## Background Image on a Page

if you want the entire page to have a background image, you must specify the background image on the `<body>`

```css
body {
    background-image: url('1.png');
}
```

## Background Repeat

if the images is smaller than the element, the image will repeat itself, horizontally, and vertically
until it reaches the end of the element

to avoid repeat

```css
body {
    background-image: url('1.png');
    background-repeat: no-repeat;
}
```
