# cycle-canvas
A canvas driver for Cycle.js. Great for games or art.

Currently highly experimental. Expect major breaking changes.

Installation
---

```bash
$ npm install cycle-canvas --save
```

Example
---

```js
import {run} from '@cycle/core';
import {makeCanvasDriver, rect, text} from 'cycle-canvas';
import {Observable} from 'rx';

function main () {
  return {
    Canvas: Observable.just(
      rect({
        x: 10,
        y: 10,

        width: 160,
        height: 100,

        draw: [
          {fill: 'purple'}
        ],

        children: [
          text({
            x: 15,
            y: 25,

            value: 'Hello World!',

            font: '18pt Arial',

            draw: [
              {fill: 'white'}
            ]
          })
        ]
      })
    )
  };
}

const drivers = {
  Canvas: makeCanvasDriver(null, {width: 800, height: 600})
};

run(main, drivers);
```

Looks like this:

![img](http://i.imgur.com/1LCZxrg.png)

Also check out the [flappy bird example](http://widdersh.in/cycle-canvas).

You can find the source for flappy bird [here](https://github.com/Widdershin/cycle-canvas/tree/master/examples/flappy-bird).

## API

#### Drawing shapes and text

- [`rect`](#rect)
- [`line`](#line)
- [`text`](#text)


#### Transformations
- [`translate`](#translate)
- [`rotate`](#rotate)
- [`scale`](#scale)

### <a id="rect"></a> `rect(options = {})`

Draws a rectangle given an object containing options.

#### options:

- `x: number` The x axis for the starting point
- `y: number` The y axis for the starting point
- `width: number` The rectangles width
- `heigh: number` The rectangles height
- `draw: array` List of drawing operation objects. Current supported operations:
	- `fill: string` The color or style to use inside the rectangle. Default is *black #000*
	- `stroke: string` The color or style to use as the stroke style. Default is *black #000*
	- `clear` Sets all pixels in the rectangle to transparent.

#### Example:
```js
// Draws a filled rectangle with a width/height of 100
// at coordinates 10,10. The fill color is #CCCCCC
rect({
	x: 10,
	y: 10,
	width: 100,
	height: 100,
	draw: [
		{fill: '#CCCCCC'}
	]
})
```

### <a id="line"></a> `line(options = {})`

Draw line given an object containing options.

#### options:

- `x: number` The x axis for the starting point
- `y: number` The y axis for the starting point
- `width: number` The rectangles width
- `heigh: number` The rectangles height
- `draw: array`

#### Example:
```js
// Draws a line
line({
	x: 10,
	y: 10,
	width: 100,
	height: 100,
	draw: [
		{fill: '#CCCCCC'}
	]
})
```

### <a id="text"></a> `text(options = {})`

Draws text given an object containing options.

#### options:

- `x: number` The x axis for the starting point
- `y: number` The y axis for the starting point
- `value: string` The text to draw
- `font: string` The text style. Uses same syntax  as the [CSS font](https://developer.mozilla.org/en-US/docs/Web/CSS/font) property.
- `draw: array` List of drawing operations objects. Current supported operations:
	- `fill: string` The color or style to fill the text. Default is *black #000*
	- `stroke: string`The color or style to use as the stroke style. Default is *black #000*

#### Example:
```js
// Draws text, 'Hell World!' in 18pt. Arial, at coordinates 10,10.
// The fill color is black.
text({
	x: 10,
	y: 10,
	value: 'Hello World!',
	font: '18pt Arial',
	draw: [
		{fill: '#000000'}
	]
})
```
