with HTML image maps you can create clickable areas on an image
the `map` tag defines an image map
an image map is an image with clickable areas
the areas are defined with one or more `area` tags

```html
<img src="test.jpg" alt="test" usemap="#workmap">
<map name="workmap">
    <area shap="rect" coords="34,44,270,350" alt="computer" href="computer.html"></area>
</map>
```
