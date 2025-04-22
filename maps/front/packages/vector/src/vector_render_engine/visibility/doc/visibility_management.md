# Visibility of objects

Some of primitives (only labels for now) may overlap each other,
to prevent unreadable mess overlapped primitives are to be hidden.
Potentially there may be other reasons to hide primitives (e.g. external styles),
but for now only collisions and removals from scene are considered.


## Collision resolution

Colliding primitives are not static on the screen, their positions and shapes depend
on current camera state (tilt/rotation/center), e.g. curved labels are allocated
on polylines specified in world coordinates. And there may be quite a lot of them in a scene (hundreds?).
So, performance is one of the first things to worry about here.

Collision resolution is an important part of engine's global visibility management,
it is described in appropriate steps of the whole visibility process in the next paragraph.

## Visibility resolution

Solution described here assumes high utilization of GPU and minimum communication with CPU.
Even though it makes the whole process quite complicated, performance benefits are considered
more important.

The process is stateful: visibility data calculated on previous frame is used to mitigate (prevent crazy blinking
of primitves during map movements) low precision of the overlapping detections. These textures are used:
 * current visibility texture - for storing current primitive alpha, overlap zoom, tilt and azimuth (256x256)
 * prev visiblity texture - the same as above but for previous frame (256x256)
 * scene visibility texture - single flag of presence in scene is stored, required for correct circular id reuse (256x256)
 * overlap texture - the fact of overlapping of one primitive by another (256x256)
 * direct priority scene texture - scene rendered in color id mode in direct priority order (scene height x width)
 * reverse priority scene texture - the same as above but in reverse priority order (scene height x width)

If the scene is changed significantly (isDirty) visibility recalculation is done by the following steps:

1. Clear current visiblity texture
2. Fill scene visiblity texture: clear it and set flags for primitives that are in scene
3. Render direct and reverse primitive scenes in color id mode: \
    rendered primitives must use getVisibility() utility to prevent mess rendering, which is not handled properly by this algorithm
4. Set "overlap" flag for all primitives
5. Calculate proper overlapping state for visible (according to scene textures) primitives: \
    same pixels are compared and if they are not identical overlapping is logged
6. Compute final visibility state (alpha channel)

This algorithm relies on the scene rendered into simplified grids, even though grid's precision is customizable
there are still some issues arise, most notably unstable overlap detection due to how GPU rasterization works.
It can be fixed by introducing some "hacks" like stability shift or storing zoom where overlap's happened, but
is should be noted that they work well for not tilted map only, something similar is to be invented when
tilting of the map gets required.
