# HTML Colors

- HTML colors are specified with predefined color names

## Color Values

- In HTML, colors can also be specified using `RGB values, HEX values, HSL values, RGBA values, and HSLA values`.

## RGB and RGBA Colors

- an `RGB` color represents `RED`, `GREEN`, `BLUE`
- an `RGBA` is an extension of RGB with an `Alpha channel(Opacity)`

### RGB Color Values

- `rgb(red, green, blue)`
- each parameter defines the intensity of the color with a value between 0 and 255
- this means there are `256 * 256 * 256 = 16777216` possible colors
- `rgb(255, 0, 0)` is red, red is highest value, and others are 0
- `rgb(0, 0, 0)` is black
- `rgb(255, 255, 255)` is white

### Shades of Gray

- shades of gray are often defined using equal values for all there parameters
- `rgb(60, 60, 60)` to `rgb(240, 240, 240)`

### RGBA Color Values

- `rgba(red, green, blue, alpha)`
- the `alpha` is a number between 0.0 and 1.0

## HTML HEX Colors

- `hexadecimal` color like `#RRGGBB`, where `RR`(red), `GG`(green), `BB`(blue)

- `#rrggbb`
- `rr`, `gg`, `bb` are values between 00 and ff (same as decimal 0 - 255)

## HTML HSL and HSLA Colors

- `HSL` stands for `hue`, `saturation`, and `lightness`
- `HSLA` is an extension of `HSL` with opacity
- `hsl(hue, saturation, lightness)`

- Hue is a degree on the color wheel from `0 - 360`, 0 is red, 120 is green, and 240 is blue
- Saturation is percentage value, 0% means a shade of gray, and 100% is the full color.
- lightness is also a percentage value, 0% is black, and 100% is white.

- Saturation can be described as the intensity of a color.
- 100% is pure color, no shades of gray
- 50% is 50% gray, but you can still see the color.
- 0% is completely gray, you can no lonber see the color.
