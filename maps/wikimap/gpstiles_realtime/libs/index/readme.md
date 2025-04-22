# gpstiles_realtime index library
Provides classes for combining temporal and spacial indexing of geometrical objects.
 - template class **`IntervalIndex`** stores objects which time lies within given time interval together with a `maps::geolib3::DynamicGeometrySearcher` spatial index for them
 - template class **`Index`** is a thread-safe collection of `IntervalIndex`'es that allows querying objects by `Query`: combined *time interval* + *bounding box*
 - template class **`RotatedIndex`** is an `Index` wrapper that allows to rotate stored objects in time: add recent and delete outdated objects
## Requirements for Object and Geometry template parameters
All index classes are **`template <class Object, class Geometry>`**
`Object` and `Geometry` classes must meet the following requirements:
 - `Object` class should provide `maps::chrono::TimePoint time() const` method which is used to get object's time
 - `Object` class should hold its geometry and return it by `const Geometry&` reference
 - `Geometry` class should provide `maps::geolib3::BoundingBox boundingBox() const` method which is used for spatial indexing
## IntervalIndex class description
**`include/interval_index.h`**
#### Construction:
```c++
    IntervalIndex(
        const TimeInterval& timeInterval,
        ObjectsHolder objects,
        GeometryCallback getGeom,
        const Grid& grid);
```
Parameters:
 - `timeInterval` - used to filter objects by time. Only objects within timeInterval will be indexed
 - `objects` - objects to store
 - `getGeom` - `std::function` used to get geometry of an object
 - `grid` - `geolib3::DynamicGeometrySearcher` grid index parameters (region and vertical/horizontal cells count)
`IntervalIndexBuilder` class is also provided for convenience.
#### Querying objects
```c++
    boost::optional<QueryResult> find(const Query& query) const;
```
Returns `boost::none` if time interval of `query` param does not intersect time interval of index.
Otherwise returns `QueryResult` object which provides forward filtering iterator to objects matching query.
#### Notes
- index is immutable after creation
- grid spatial index used in `geolib3::DynamicGeometrySearcher` shows good performance when used for storing objects which are highly non-uniformly distributed
- performing `find()` method can be much faster than iterating through its result (due to lazy filtering iteration). If you have to iterate over query result more than once it may be more efficient to create a new (filtered) collection of objects and use it instead.
#### Usage examples
See `tests/interval_index_tests/interval_index_tests.cpp`.
## Index class description
**`include/index.h`**
#### Construction
Empty index is default-constructible.
#### Adding/removing data
```c++
    void add(IntervalIndex intervalIndex);
```
There are no additional constraints on `IntervalIndex` objects that can be added.
```c++
    void remove(const TimePoint& thresholdTime);
```
All indexes which time interval ended earlier than `thresholdTime` will be deleted.
#### Querying objects
```c++
    QueryResult find(const Query& query) const;
```
Same like `IntervalIndex::find()`, returns its own `QueryResult` object which provides forward filtering iterator to objects matching query. 
`QueryResult::Iterator` is a chained iterator over collection of `IntervalIndex::find()` results for all indexes which time interval intersects with time interval from `query`.
*Same notes for lazy filtering apply*, as in `IntervalIndex`.
#### Thread safety
Access to `IntervalIndex` objects collection is guarded by `std::shared_timed_mutex` to allow
- shared access of multiple "readers" - `find()` queries
- unique access of  "writers" - `add()` or `remove()` queries.
#### Usage examples
See `tests/index_tests/index_tests.cpp`.
## RotatedIndex class description
**`include/rotated_index.h`**
#### Description
`RotatedIndex` consists of:
- a queue of objects to add. Client can add new objects in queue calling `push()` method.
- `Index` object
- `Updater` and `Deleter` objects which update queue and index in their own `maps::concurrent::BackgroundThread`s:
    - `Updater`, when awakes, takes all objects from queue, builds `IntervalIndex`'es from these objects and adds them to index
    - `Deleter`, when awakes, removes all interval indexes which are older than specified max storage duration
#### Construction
```c++
    RotatedIndex(
        std::chrono::minutes storageDuration,
        std::chrono::seconds updateDuration,
        Builder builder);
```
Parameters:
- `storageDuration` - max age of objects which are stored 
- `updateDuration` - sleep duration for `Updater` and `Deleter` workers
- `builder` - `IntervalIndexBuilder` object which will be used to construct new `IntervalIndex`'es from objects in queue

To start rotation cycle, call `start()` method after construction.
#### Adding objects
```c++
    void push(QueueChunk objects) { updater_.push(std::move(objects)); }
```
Objects are added to `Updater`'s queue via `push()` method.
#### Querying objects
You can access underlying `Index` object via `index()` method.
#### Usage examples
See `maps/wikimap/gpstiles_realtime/renderer/lib/storage.h`.
