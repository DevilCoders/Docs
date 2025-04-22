# Hit Test

Hit test's implemented using [color picking][1]. Adapters are responsible for
assigning an id to every object and to have a way to provide object's metadata
by its id. Render units used to render primitives supplied by adapters are
responsible for rendering objects into special framebuffer with their ids
instead of actual colors.

## Adapters

Adapters participate in hit test in two major ways:

  1. assigning an id for an object (usually its either a unique id or some kind
     of default id for marking "non-interactive" objects), and writing the ids
     into GPU buffers.
  2. keeping a map from ids to metadata objects.

## Rendering

`HitTestManager` handles allocation of hit test buffer. Size of the buffer is
picked to be less than size of the default context render target on the one hand
(with a multiplier dependent upon `devicePixelRatio`) and multiple of 256 on the
other.

Every render unit that handles potentially interactive objects must implement
`renderHitTestBuffer` method, that should render object with their respective
ids into provided `RGBA` buffer.

## Getting pixel data from GPU

Pixel data is being read from hit test buffer in 256x256 tiles (since size of
the buffer is multiple of 255, there's always integer number of tiles in the
buffer). There's a cache for tiles to avoid reading the same data multiple
times. The cache is purges every time hit test manager decides to redraw hit
test buffer.

## Sequence

![Sequence Diagram](./hit_test.svg)

[1]: http://www.opengl-tutorial.org/miscellaneous/clicking-on-objects/picking-with-an-opengl-hack/
