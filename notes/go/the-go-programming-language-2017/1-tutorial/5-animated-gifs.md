# Animated GIFs

> demonstrates basic usage of Go's standard image packages
> which we'll use to create a sequence of bit-mapped images and then encode the sequence as a GIF animation.

- import a package whose path has multiple components, like `import image/color`
- we refer to the package with a name that comes from the last component, such as `color.White`

- a `const` declaration gives names to constants, values that are fixed at compile time.
- like `var` declaration, `const` declarations may appear at package level,
- so the names are visible throughout the package
- **the value of a constant must be a number, string or boolean**

- `[]color.Color{...}` and `gif.GIF{...}` are **composite literals**
- a compact notation for instaniating any of Go's composite types from a sequence of element values.
- here, the first one is called a slice, and the second one is a `struct`

- `gif.GIF` is a struct type.
- a `struct` is a group of values called `fields`
- often of different types, that are collected together in a single object that can be treated as a unit.
- the individual fields of a struct can be accessed using dot notation.

- the `lissajous` functon has two nested loops.
- the outer loop runs for 64 iterations, each producing a single frame of the animation.
- it creates a new 210 x 210 image with a palette of two colors, white and black

- `io.Writer` which let us write to a wide range of possible destinations.

- the inner loop runs the two oscillators.
- the x oscillator is just the sine function.

```golang
package main

import (
	"image"
	"image/color"
	"image/gif"
	"io"
	"math"
	"math/rand"
	"os"
)

var palette = []color.Color{color.White, color.Black}

const (
	whiteIndex = 0 // first color in palette
	blackIndex = 1 // next color in palette
)

func main() {
	lissajous(os.Stdout)
}

func lissajous(out io.Writer) {
	const (
		cycles  = 5     // number of complete x oscillator revolutions
		res     = 0.001 // angular resolution
		size    = 100   // image canvas covers [-size..+size]
		nframes = 64    // number of animation frames
		delay   = 8     // delay between frames in 10ms units
	)
	freq := rand.Float64() * 3.0 // relative frequency of y oscillator
	anim := gif.GIF{LoopCount: nframes}
	phase := 0.0
	for i := 0; i < nframes; i++ {
		rect := image.Rect(0, 0, 2*size+1, 2*size+1)
		img := image.NewPaletted(rect, palette)
		for t := 0.0; t < cycles*2*math.Pi; t += res {
			x := math.Sin(t)
			y := math.Sin(t*freq + phase)
			img.SetColorIndex(size+int(x*size+0.5), size+int(y*size+0.5), blackIndex)
		}
		phase += 0.1
		anim.Delay = append(anim.Delay, delay)
		anim.Image = append(anim.Image, img)
	}
	gif.EncodeAll(out, &anim)
}
```
