## Example usage:

Call library graph to create FileResource with icons archive:

```
from maps.garden.libs.basemap_icons.lib.graph import fill_render_icons_graph
from maps.garden.modules.renderer_map_stable_bundle.lib import bundle_info as stable_map_design

...

fill_render_icons_graph(
    graph_builder, 
    stable_map_design.get_map_bundle_info(), 
    OUTPUT_RESOURCE_NAME
)
```
