# Introduction
Raster image : 2d grid of pixels, color of pixel consists of (r,g,b) value. And the range is going to be in a range of 0-255 (1 byte).

Examples:
- color = (255, 0, 0) = bright red

Coordinate system of the screen (for almost all low level graphics library), the origin is TOP-LEFT (0,0 at TOP-LEFT) and positive x goes to the right and positive y goes to the bottom.

`size(400, 400)` creates a window of the size 400x400 pixels.

> (Note that pixel count goes from 0 to n-1).

Drawing commands:
- `rect(x,y,width,height)`:  to draw a rectangle, sample: `rect(100,200,10,10)`
- `ellipse(x,y,width, height)` : to draw an ellipse (also a circle), the x and y is the center of the circle, samle: `ellips(200,200,30,30)`

Last fill or stroke is stored in memory, so you can simply reuse, no need to call fill or stroke repeatedly.

## Conversion from cartesian to image processing coordinates.
Converting x with range (-2, 2) to range (0, 500)
- First step is to convert it to 0 range, so (0, 4)
- And then to translate it to the second system, multiply any points by 500 and divide by 4.0 (remember that most languages assume integer division which causes tons of problems, so make it **floating point**)

Converting x with range (0, 1024) to (-1, 1)
- First step simply -512 to make range (-512, 512)
- And then to translate is  * 1/512

x' = (x-512)/512

## Flipping the y coordinate (to make origin be on bottom left rather than upper left)
y' = (height-1) - y

## Trigonometry reminder
An angle theta, x,y points in the circle can be represented as
(x,y) = (cos theta, sin theta)

Processing uses radians
