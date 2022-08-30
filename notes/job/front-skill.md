## dynamic hover color

```js
periodStyle(): any {
    return {
        ...this.bgColorStyle,
        ...this.heightStyle,
        ...this.widthStyle,
        marginBottom: `${this.periodMarginBottom}px`,
        '--active-hover-bg-color': this.activeHoverBgColor,
        '--inactive-hover-bg-color': this.inactiveHoverBgColor,
      };
},
```

```css
.on:hover {
  background-color: var(--active-hover-bg-color) !important;
}
.off:hover {
  background-color: var(--inactive-hover-bg-color) !important;
}
```
