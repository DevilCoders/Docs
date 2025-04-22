# Player

Player based on `<canvas>` HTML element.

## Main concepts

Frame rendering logic is wrapped inside `useDrawImage` hook.
`HTMLImageElement` is created inside this hook with `src`
attribute from component props. When the image is loaded,
it is immediately drawn on `canvas` element.

If `fps` prop is provided, image will be drawn on canvas
with `1000 / fps` interval. This may be useful for MJPEG streams.

Frame rendering may be customized with `onFrame` callback.
It is called on each rendered frame and may be used for adding
different effects to the original image. Note that the original frame
is already rendered on canvas before `onFrame` callback is called.

## TODO

- [ ] use `ReadableStream` to fetch frames from the resource passed in `src` prop
