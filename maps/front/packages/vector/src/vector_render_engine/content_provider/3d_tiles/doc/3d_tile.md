# 3D Tiles

3D tiles are similar to 2D tile, but their visibility computation must take 3rd dimension into account. Cesium 3D Tiles hierarchical model is taken as the basis, and it is the only implementation for now, but the code works with more abstract entity where it is possible, which will allow to support other formats if required.

## Data flow
3D tiles visibility is calculated in a `Tile3DViewport`. Currently implemented only `NonRegularTile3DViewport` that works with separate models and is better suitable for heavy detailed models of a showplace or commercial objects. The viewport is notified about available models by adding root tileset (`addRootTile(tile: Tile3D)`). Later on, when user moves camera, added model's bboxes are tested for visibility by intersecting their bbox with camera's frustum. `Tile3DContentManager` listens for updates in viewport and takes care of uploading proper tile level data.

Another alternative for managing 3D Tiles is `RegularGridTile3DViewport`, that sees the world as a reglural grid. So that appropriate tiles can be loaded with some math manipulations (as it is done for 2D tiles). This viewport is supposed to be used with 3D data that cover lager areas, like cities or blocks (Google maps 3D view is a good example). It is not currently implemented as there is no data.


## Cesium 3D Tiles

A subset of the Cesium tiles spec is implemented: hierachical set of `tileset.json` files is supported and b3dm files for content storage. Looks like this:

![](./tileset_content.svg)

Processing of b3dm content is done in main thread, it is a lightweight operation, GlTF parsing is done in web workers (pool of them). This separation allows to easily reuse GlTF for custom 3D tiles format, it is not that easy to invent own GlTF.


## Content manager

3D tile's content is usually pretty heavy. It is CPU intensive as it requires to process buffer data and it can contain pretty large textures, which must be loaded into GPU. The process of tile model preparation is splitted and made asynchronous whenever it possible: buffer data is prepared via a pool of web workers (`GlTFDecoder`), renderable primitive (`GlTFRenderableAsset`) instantiation is done step-by-step (see `GlTFRenderableAsset#stepInitialization()`) asynchronously in content manager. E.g. a step could be instatiation of a texture, as it can take as much as 100ms on a modern client hardware.


## RTC rendering

WebGL 32-bit float is not enough for represinting geo data. That is why we need to support Relative-To-Center rendering. There are two types (`GltfCoordinatesType`) of coordinates that currently supported: `GEO_CARTESIAN` - Cartesian coordinates of the whole world, default for cesium, `ArcGIS Metashape` spits models out in that format, RTC coordinates are also provided, and `MODEL_CARTESIAN` - just model coordinates as they would be stored from any 3D editor like Blender or Maya, geo position is defined by additional RTC coordinates and a set of transformations, cesium files from out geo positioning tool are stored in this format.
Basically RTC coordinates allow not to work with big values and thus avoid precision loss, as it is possible to calculate model position in viewport as the difference between vectors of camera center, RTC and real vertex position:


![](./rtc.svg)

Vector **A** is what is written in buffers (as is from cesium files from our tool, preprocessed for normal cesiums). Vector **B** is computed in render unit for each frame and provided into shader as a matrix (by multiplying viewProj matrix). Vector **C** is what we really need to position our model in front of the camera, it is the result of shader math and passed to WebGL primitive assemply stage.