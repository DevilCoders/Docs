# Zoom ranges

This document describe zoom ranges architecture.

## Map zoom range

User can set zoom range on map construction by passing optional `zoomRange` field.

If user pass zoom which is out of range when constructing map or via methods which allows to set zoom then zoom value will be clamped to zoom range.

## Data sources zoom ranges

User can set zoom range for a specific data source by passing optional `zoomRange` field to the data source.

Data source can affect map zoom if user set optional option `clampMapZoom` to `true`. Final map zoom range is the intersection of map zoom range and all zoom ranges from data sources for which `clampMapZoom` is set to true.

User can update zoom range for any existing data source by using `updateTileDataSource` method on a `map`.

If one of the data source zoom range for which `clampMapZoom` is set to true do not intersect with map zoom range or with zoom range from another `clampMapZoom` data source an error will be thrown.
