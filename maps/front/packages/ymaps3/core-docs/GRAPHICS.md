# Graphics

This document describe graphics layer.

## Drawing style

See `DrawingStyle` interface for details.

### stroke

Stroke contains array of `StrokeStyle` objects (see `StrokeStyle` interface definition for details).

`LineString` and `MiltiLineString` support multiple strokes so they use all of the `StrokeStyle` objects from this field. Others use only first `StrokeStyle` object.

#### palette

For every stroke of LineString geometry palette can be applied. Palette is a combination of color and number of consecutive lines from geometry (line here means two consecutive points).

Each palette splits geometry into `segments` which then colored by appropriate colors. Each segment is processed by simplification algorithm before it will be displayed. Since we can have different palettes, segments are also can be different. It leads us to the following problem: after simplification these segments may not align perfectly.

To address this issue following algorithm is used. We combine all palettes in a paletteColorStops which contains all point indexes where palettes are changing their colors. If we split geometry by paletteColorStops we get equal segments for every palette, and after simplification they will align perfectly (and we can simplify all geometry only once, what a perfect solution!).

For example we have LineString with two palettes:

- Palette #1: red: 10, white: 30, red: 15
- Palette #2: blue: 5, white: 40, green: 10

We can convert these palettes from using consecutive lines count to the point indexes where colors are change by accumulating counts:

- Palette #1: red: 10 (0 + 10), white: 40 (10 + 30), red: 55 (10 + 30 + 15)
- Palette #2: blue: 5 (0 + 5), white: 45 (5 + 40), green: 55 (5 + 40 + 10)

By collectiong uniq indexes we can compute paletteColorStops:

- 5, 10, 40, 45, 55

We can split geometry by paletteColorStops, and since it encodes all palettes we can compute colors for each paletteColorStops entry from original palettes and use this information with paletteColorStops to color each segments:

- Palette colors #1: red, red, white, red, red
- Palette colors #2: blue, white, white, white, green

See following diagram for a visual explanation:

![palette-color-stop-split](./img/palette-color-stop-split.png)

## Multiworlds

Graphic elements are rendered on all visible worlds. It works by creating copies of features with translated coordinates for each world (except for zero world because coordinates is already translated by 0). Clipping works just fine with window and feature given in overflowed `WorldCoordinates` (overflowed means coordinate can go beyound -1 1).
