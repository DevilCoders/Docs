# More compact version of tile index

[TOC]

## Tile

Can be found in `<impl/tile.h>`. Tile is defined by its offset from the top left corner and zoom.

Tile offset structure is something like vector with unsigned integer coordinates. It behaves like ordered
regular type and supports ring operations (element-wise +, -, *).

Tile also is an ordered regular type. Tiles form a hierarchy with Earth tile (0, 0 offset and 0 zoom) at the
top. Each tile has one parent and four children. You can navigate between them using `ancestor` and `child`
methods. To check weather one tile is inside other tile use `contains` and `within` methods. For tile to be
valid its offset should not be greater than maximum for the given zoom: $offset  < 4^{zoom}$.

Tile position within its direct parent is determined by the quadrant structure. It's the offset with
coordinates $x, y \in [0, 2)$ from top-left corner of parent tile encoded to $index \in [0, 4)$. Offset to
index coding is following:

###### Pic, quadrant mapping

```
  0 1 
 ┌─┬─┬─> x
0│0│1│
 ├─┼─┤
1│2│3│
 ├─┴─┘
 V y
```

For all $x, y \in [0, 2)$ holds that

```c++
Quadrant q{x, y};
assert(q.x() == x && q.y() == y);
```

You can iterate over all quadrants using `AllQuadrants` class:

```c++
for (Quadrant quad : AllQuadrants{}) { }
```

### Tile range

Can be found in `<impl/tile_range.h>`. Allows to iterate over all child tiles with given zoom withing the
given tile. Iteration order is row-major, e.g. y coordinate changes faster.

```c++
for (const Tile& tile: TileRange{zoom, TilePos::Earth()}) { } 
```

Also can iterate atomically in multithreaded environment.

```c++
TileRange range{10, TilePos::Earth()};
auto next = range.atomic();
// In each thread
while (const auto it = next()) {
    const Tile tile = *it;
}
```

## Release

Can be found in `<include/release.h>`. It is a structure we add to index. Consists of issue id and some mosaic
geometries. Each geometry correspond to a certain zoom level. Release cannot contain empty geometries.

Releases can be stored and loaded from file system. Geometries are stored in separate files in WKB format.
Directory structure has the following view:

```text
root_dir
├ 1
│ ├ 2.wkb
│ └ 3.wkb
└ 4
  ├ 5.wkb
  ├ 6.wkb
  └ 7.wkb
```

This corresponds to following releases structure:

```xml
<releases>
  <release issue="1">
    <geometry zoom="2" data="root_dir/1/2.wkb">
    <geometry zoom="3" data="root_dir/1/3.wkb">
  </release>
  <release issue="4">
    <geometry zoom="5" data="root_dir/4/5.wkb">
    <geometry zoom="6" data="root_dir/4/6.wkb">
    <geometry zoom="7" data="root_dir/4/7.wkb">
  </release>
</releases>
```

See also [spatial data formats](https://dev.mysql.com/doc/refman/5.7/en/gis-data-formats.html).

## Tile index

Can be found in `<include/tile_index.h>`. The main goal of the index is to check when the given tile was
covered by release's geometry. Logic of the process is equivalent to this pseudo code:

```python
def resolve(fromIssue, tile):  
  for issue in range(fromIssue, -1, -1):  
    geometry = findRelease(issue).geometry(tile.zoom)
    if intersects(geometry, tile):
      return issue
  return None
```

## Implementation

### Glossary

- **Child**: A node directly connected to another node when moving away from the Root. The inverse
  relationship is that of a **parent** node. If node $v$ is a child of node $u$, then $u$ is the parent node
  of $v$.
- **Descendant**: A node reachable by repeated proceeding from parent to child.
- **Ancestor**: A node reachable by repeated proceeding from child to parent.
- **Degree**: The degree of a node is the number of children of the node.
- **Depth**: The depth of node $v$ is the length of the path from $v$ to the root node. The root node is said
  to have depth 0.
- **Edge**: The directed connection between two nodes.
- **Height**: The height of node $v$ is the length of the longest path through children to a leaf node.
- **Internal node**: A node with at least one child.
- **Leaf node**: A node with no children. In other words the node without outgoing edges.
- **Root node**: A node distinguished from the rest of the tree nodes. Usually, it is depicted as the highest
  node of the tree. Root node does not have any incoming edges.
- **Sibling nodes**: These are nodes connected to the same parent node.
- **Origin node**: First endpoint of a directed edge. Also a parent node.
- **Destination node**: Second endpoint of a directed edge. Also a child node.
- **Adjacent**: If there is an edge between nodes $v$ and $u$ then both $v$ and $u$ are said to be adjacent.
- **Incident**: An edge is said to be incident on a node if the node is one of the endpoints of that edge.
- **Outgoing edge**: A directed edge is said to be outgoing edge on its origin node.
- **Incoming edge**: A directed edge is said to be incoming edge on its destination node.
- **Directed acyclic graph (DAG)**: A directed graph with no directed cycles. That is, it consists of many
  nodes and edges, with each edge directed from one node to another, such that there is no way to start at any
  node $v$ and follow a consistently-directed sequence of edges that eventually loops back to $v$ again.
  Equivalently, a DAG is a directed graph that has a topological ordering, a sequence of the nodes such that
  every edge is directed from earlier to later in the sequence.
- **Topological ordering**: Every directed acyclic graph has a topological ordering, an ordering of the nodes
  such that the starting endpoint of every edge occurs earlier in the ordering than the ending endpoint of the
  edge. The existence of such an ordering can be used to characterize DAGs: a directed graph is a DAG if and
  only if it has a topological ordering. In general, this ordering is not unique; a DAG has a unique
  topological ordering if and only if it has a directed path containing all the nodes, in which case the
  ordering is the same as the order in which the nodes appear in the path.
- **Quadtree**: A tree in which each internal node has exactly four children. Quadtrees are the
  two-dimensional analog of octrees and are most often used to partition a two-dimensional space by
  recursively subdividing it into four quadrants or regions. The data associated with a leaf cell varies by
  application, but the leaf cell represents a "unit of interesting spatial information".

### Tree

This names is somewhat inaccurate because it is really a rooted DAG. All child nodes reachable from any root
form a quad tree. It can be viewed as a single quadtree with saved history of all it's previous versions. Each
version has a unique number. At the beginning the current version is 0, next version will be 1 and so on. Each
root has index which is equal to the version of the tree formed by its children. Each leaf node marked by the
version of the tree when it was added. So we can traverse any version of the tree starting from the
corresponding root and query each leaf for the version when it was added.

For example, after marking _{1, 1, 1}, {3, 1, 2}, {5, 1, 3}_ tiles the resulting tree will have the following
structure:

###### Pic, tree with one root

```text
  0 1 2 3 4 5 6 7
0┌───────┬─┬─┬───┐→ x
1│       ├─╆━┪   │        root 0
2│       ├─┺━╋━━━┪        └── (0, 0, 0) tile with (x, y, zoom)
3│       │   ┃   ┃            ├── (1, 0, 1)
4├───────╆━━━┻━━━┫            │   ├── (2, 0, 2)
5│       ┃       ┃            │   │   └── (5, 1, 3) leaf 0
6│       ┃       ┃            │   └── (3, 1, 2) leaf 0
7│       ┃       ┃            └── (1, 1, 1) leaf 0
 └───────┺━━━━━━━┛        
 ↓ y
```

Lets name all marked leafs as a _region 0_:

```text
  0   roots
  ┬
┌─┴─╮
│ 0 │ regions
╰───┘
```

Add some more _{1, 1, 2}, {0, 2, 3}_ tiles to a new _region 1_:

```text
  0      1     roots
  ┬      ┬
┌─┴─╮ ┌──┴╮
│ 0 │ │ 0╭┴──┐ regions
╰───┘ ╰──┤ 1 │
         └───╯
```

After that the tree will have the following structure:

###### Pic, tree with two roots

```text
  0 1 2 3 4 5 6 7
0┌───┬───┬─┬─┬───┐→ x     root 0                            root 1
1│   │   ├─╆━┪   │        └── (0, 0, 0)                     └── (0, 0, 0)
2┢━┱─╆━━━╅─┺━╋━━━┪            ├── (1, 0, 1)                     ├── (0, 0, 1)
3┡━╃─┨   ┃   ┃   ┃            │   ├── (2, 0, 2)                 │   ├── (0, 1, 2)  
4├─┴─┺━━━╋━━━┻━━━┫            │   │   └── (5, 1, 3) leaf 0      │   │   └── (0, 2, 3) leaf 1
5│       ┃       ┃            │   └── (3, 1, 2) leaf 0          │   └── (1, 1, 2) leaf 1
6│       ┃       ┃            └── (1, 1, 1) leaf 0              ├── (1, 0, 1)     
7│       ┃       ┃                                              │   ├── (2, 0, 2)
 └───────┺━━━━━━━┛                                              │   │   └── (5, 1, 3) leaf 0
 ↓ y                                                            │   └── (3, 1, 2) leaf 0
                                                                └── (1, 1, 1) leaf 0
```

Tree base class can be found in `<impl/tree.h>`. It has methods shared across mms and editable trees.

You can notice that payload is stored only in leafs and internal nodes store only links to other nodes. This
fact allows us to optimize memory requirements by storing either leaf payload or child node index for any edge
destination node with flag to distinguish between them. For example structure for [tree with one root](#Pic,
tree with one root), where `│(0)│` - leaf destination node with _0_ payload, `│ - │`  - _null_ destination
node, `│ 3 │` - destination node pointing to node with index _3_:

###### Pic, nodes structure with one root

```text
   ┌───┐
   │ 1 │ roots array with indices to root nodes
   └─┬─┘  
     v 
   ┌─┴─┬───┬───┬───┐
  1│ 2 │ - │ - │ - │  all destination nodes are at zoom 0
   └─┬─┴───┴───┴───┘
     v e1/0 edge where 1 is the origin node index and 0 is the quadrant
   ┌─┴─┬───┬───┬───┐
  2│ - │ 3 │ - │(0)│  zoom 1
   └───┴─┬─┴───┴───┘
     ╭─<─╯ e2/1
   ┌─┴─┬───┬───┬───┐ 
  3│ 4 │ - │ - │(0)│  zoom 2
   └─┬─┴───┴───┴───┘ 
     v e3/0
   ┌─┴─┬───┬───┬───┐ 
  4│ - │ - │ - │(0)│  zoom 3
   └───┴───┴───┴───┘ 
```

After marking [second region](#Pic, tree with two roots):

###### Pic, nodes structure with two roots

```text
   ┌───┬───┐
   │ 1 │ 5 │ roots array
   └─┬─┴─┬─┘  
     v   ╰───────────>───╮
   ┌─┴─┬───┬───┬───┐   ┌─┴─┬───┬───┬───┐  
  1│ 2 │ - │ - │ - │  5│ 6 │ - │ - │ - │  zoom 0
   └─┬─┴───┴───┴───┘   └─┬─┴───┴───┴───┘  
     v e1/0              v e5/0
   ┌─┴─┬───┬───┬───┐   ┌─┴─┬───┬───┬───┐
  2│ - │ 3 │ - │(0)│  6│ 7 │ 3 │ - │(0)│  zoom 1
   └───┴─┬─┴───┴───┘   └─┬─┴─┬─┴───┴───┘
e2/1 ╭─<─╯─────e6/1──────v───╯ e6/0
   ┌─┴─┬───┬───┬───┐   ┌─┴─┬───┬───┬───┐
  3│ 4 │ - │ - │(0)│  7│ - │ - │ 8 │(1)│  zoom 2
   └─┬─┴───┴───┴───┘   └───┴───┴─┬─┴───┘
     v e3/0              ╭─────<─╯ e7/3
   ┌─┴─┬───┬───┬───┐   ┌─┴─┬───┬───┬───┐
  4│ - │ - │ - │(0)│  8│(1)│ - │ - │ - │  zoom 3
   └───┴───┴───┴───┘   └───┴───┴───┴───┘
```

Here each _node_ consists of four adjacent _destination nodes_. Nodes at _zoom 0_, also called _root nodes_,
always have last 3 destination nodes equal _null_. Each tree has special node at index _0_, also called _
NULL_IDX_, it has all four destinations equal _null_. Each destination can be either index of child node or
payload for that child node when it is a leaf. Destination node with _0_ index is called a _NULL_DESTINATION_.
To query destination node from the tree we have to use an _edge_, that is defined by its _origin_ node index
and [quadrant](#Pic, quadrant mapping) that serves as an index of the destination node. Edge origin cannot
be _null_.

### MMS tree

Can be found in `<impl/tree_mms.h>`. Stores nodes in compact format but does not support marking. It can be
saved to a file, loaded or memory mapped to that file. To modify mms tree you have to copy it to editable form
using function `expand` from `<impl/tree_compact_expand.h>`. To convert back use `compact` function. Exact
nodes representation can vary but the approach is to remove zero bytes from indices and payloads. We can also
reduce magnitude of stored integers by subtracting current node index from its destination indices, assuming
that they will always be less than current node index due to topological sorting.

### Editable tree

Can be found in `<impl/tree_editable.h>`. Not so compact but support marking separate tiles or all tiles
intersected with some geometry. Marking should be performed in 3 steps:

- Calling `beginMarking`. It creates new root corresponding to a tree with new version and sets it as current.
  Version will be _0_ if the tree was empty or _previous version + 1_ otherwise.
- Marking some geometries using `markGeom` or tiles using `markTile`. All marked leafs will have the current
  version mark.
- Calling `endMarking`. It searches for references to the previous versions to make tree structure valid.

To convert this tree to compact version it's required to topologically sort all nodes
using `topologicallySorted` method. After that all children will have indices lower than the parent node
index. That allows to copy nodes sequentially that is required than we does not know node index until it is
added to the tree.

### Visitors and iterators

Can be found in `<impl/visitors.h>` and `<impl/tree_iterators.h>`. Iterators allows as to easily iterate over
tree roots, nodes, outgoing edges or just print tree as a list of nodes. Visitors visit all destination nodes
in DFS manner. For example in order to check tree invariants or print it in tree form.

# Tools

Can be found in `<tools>` directory. Allows to do all kinds of things with tile index and tile keys lists.

## Formats

### Tile as uint64

Each tile offset, zoom and issue id for release when it was marked can be stored in just 64 bits. This format
is called `uint64` and is used by default to interchange data between utilities.

### Index range

All range values are parsed using this format. Format string has form `a:b` that corresponds to [a, b) range.
It handles missing or negative numbers with similar to python's slice semantics.

Examples:

* `2:4` from 2 to 4 included
* `3` only with index 3
* `:3` from 0 to 3 included
* `10:` from 10 to the last
* `-1` the last one
* `-4:` last 4 items
* `:` all items

## Load releases from database

Utility for loading releases with geometries from database and saving them to the given folder.

Usage: `load_releases_from_db -c <filename> <options...>`.

Options:

* `-c, --config <filename>` Database connection string or path to configuration `.json` file with it..
* `-o, --out <dir>` Directory to save releases.
* `--info` Print releases information and exit.
* `-s, --issue <value>` Issue id in [index range format](#Index range).
* `-a, --add` Don't remove out directory if it exists.

## Build or edit index

Utility for creating or modifying tile index.

Usage: `build_index -i <filename> <options...>`.

Options:

* `-i, --index <filename>` Load index from this file. Create if not exists.
* `-r, --releases <dir>` Load releases from this directory. Treat as 0 releases when not set. Dir should exist
  when set.

## Show index information

Show information about tile index.

Usage: `show_index_info -i <filename> <options...>`.

Options:

* `-i, --index <filename>` Load index from this file.
* `-s, --size` Show tree size information.
* `-n, --stat` Calculate and show nodes statistics.
* `-c, --check` Check trees consistency.
* `-m, --meta` Show releases information.
* `-t, --tiles` Show tiles count for each zoom.
