# Rendering in RenderUnits

Render scene is described via compositon of abstract RenderUnits. A RenderUnit can be seen as a separate peace (atomic, independant, self-sufficient, etc) of GL commands that forms specific part of the scene (e.g. rendering of polygons or post process antialiasing). RenderUnits can contain other RenderUnits, in that case it becomes CompositeRenderUnit. Thus all data/commands that needed for rendering are represented in a tree structure (technically it can be a graph, with cycle dependencies between nodes, but it is not encouraged) of RenderUnits. Something like this:

![render unit tree](./tree_of_abstract_renderunits.png)

## PrimitiveRenderUnit
Most visible objects in scene are rendered from data sources that get filled in run time. To get data in time PrimitiveRenderUnit contains a primitive provider, that abstracts out the source of primitives.
```typescript
interface RenderUnit {
    onUpdate: VoidEventEmitter;
    render(target: RenderTarget, ...args);
}

interface PrimitiveProvider<PrimitiveT> {
    onUpdate: VoidEventEmitter;
    primitives: Iterable<PrimitiveT>;
}

class WorldPrimitiveRenderUnit<PrimitiveT> implements RenderUnit {
    public primitiveProvider: PrimitveProvider<PrimitiveT>;
    // renders primitives from provider in world coordinates
}
```

## MapEngine render scene structure
`MapEngine` predefines some layers (`RenderUnit`'s that blend over one another) that reflect the business logic of the content. In contrast to the base `Engine` class that know about the root `MainRenderUnit` only.

To specify how the map is to be look like and what data it shows these layers must be provided with primitive render units. It is supposed to be done during initialization somewhere outside of the `MapEngine` or `VectorApiAdapter`.

Then engine watches updates in the main render unit (`CompositeRenderUnit`s propagate updates from their children) and updates in camera. If something has changed it runs rendering by calling the `render()` method of the main (root in the tree) render unit. `CompositeRenderUnit`'s  call their children's `render()` methods and the whole tree gets deep traversed.

Primitive render units take primitives from their providers, while providers get filled by adapter.

![render unit tree](./map_engine_renderunits_hierarchy.png)


## Extension
There is a separate phase of configuring scene structure, so the map can be assembled of different `RenderUnit`s (third paty provided as well). To simplify implementation of most popular business rules (e.g. render something above roads or render something below labels) there are some `CompositeRenderUnit`s exposed from `MapEngine` (ground/building/icons/labels). They are call "layers" since they are rendered in fixed order and just blend over one another. This concept also seems quite simple for external users. Currently layers implementated as `ListRenderUnit`s (if not speficiend anything else) they render added RenderUnits in the order of addition.
For example if we need to mix default map content with, say, some traffic information we assemble map instance like the following:

```typescript
const vectorApiAdapter = ...;
const trafficAdapter = ...;

engine.groundLayer.addRenderUnit(new PolygonRenderUnit(context, vectorApiAdapter.opaquePolygonsProvider));
engine.groundLayer.addRenderUnit(new PolygonRenderUnit(context, trafficAdapter.opaquePolygonsProvider));
...
engine.labelsLayer.addRenderUnit(new CurvedLabelRenderUnit(context, vectorApiAdapter.opaquePolygonsProvider, visibilityProvider));
engine.labelsLayer.addRenderUnit(new CurvedLabelRenderUnit(context, trafficAdapter.opaquePolygonsProvider, visibilityProvider));
...
```
Note that some `RenderUnit`s could be reused as long someone (traffic adapter in this case) provides appropriate primitives via shared primitive provider. Or, if it is required to render unknow primitives, custom implementation of `RenderUnit` could be added the same way.
