# Graph

### Description
A simple library to traverse small piece of road graph, considering road conditions (u-turns, forbidden maneuvers and etc). The graph is formed dynamically, taking into account history of traversed road edges.
* Nodes are road elements with a fixed direction of travel (multiple nodes may correspond to one element).
* Two nodes are connected with directed edge if it is possible to move from one road element to another via common road junction without breaking road conditions.
During graph traversing access_id attribute of conditions and road elements are considered. So you have routing for different transport types or pedestrians.

### Road conditions
* **U-turn condition** U-turn at junction is forbidden by deafult, but may be allowed with appropriate condition. U-turn consists of road element and via junction. Such condition may be specified by adding appropriate edge.
* **Short prohibiting maneuver** It's forbidden sequence of two road elements (necessarily different) and via junction between them. It's possible to specify just removing relevant edge.
* **Long prohibiting maneuver** It consists of 3 or more road elements. Such condition can no longer be formalized by removing/adding some edge.

### Main concept
The concept of directed graph is based on the [library](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/libs/graph). Also there are several important primitives
* **DirectedId** – id of the road element, considering direction of moving.
* **Trace** – valid chain of directed ids, fixes track of traversed road elements.

Nodes are generated dynamically, considering traversed path and conditions in road graph. So, each node is defined with trace, which stores essential track suffix. U-turn is specified by adding appropriate edge.

### Example
Simple graph of road elements **A**, **B**, **C**, **D**, prohibiting maneuver **В-g-С** and u-turn **A-f-A**.
```
    A     B      C
(e)<->(f)--->(g)--->(h)
              |
            D |
              V
             (j)
```
We start from element **A**, wich corresponds to node with trace **{A:Forward}**. It's possible to move to **{A:Backward}** and **{B:Forward}**. As we can see, the second node stores prefix of entered forbidden condition. Further, from **B**, there are two candidates **{D:Forward}** and **{B:Forward, C:Forward}**. But possible only the first variant, because trace **{B:Forward, C:Forward}** is forbidden.

### Using
Graph has rather abstract interface. It's recommended to get a node id of initial road element, then traverse graph, using method **edges**. Each node id can be transformed to directed id back.
```
#include <maps/wikimap/mapspro/services/mrc/libs/graph/include/graph.h>

// some code...

Graph graph{...};

DirectedId start{...};

for (const auto& edge: graph.edges(graph.getNodeId(start))) {
    const DirectedId end = graph.getDirectedId(edge.endNodeId());
    std::cout << start.roadElementId() << "->" << end.roadElementId();
}
```

Also graph is designed to be used with the [library](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/libs/graph).
```
#include <yandex/maps/wiki/graph/shortest_path.h>

// some code

Graph = graph{...};

DirectedId start{...};
DirectedId end{...};

const auto result = wiki::graph::findShortestPath(
    [&graph](graph::NodeId nodeId) {
        return graph.edges(nodeId);
    },
    graph.getNodeId(start),
    [&](graph::NodeId nodeId) {
        return graph.getDirectedId(nodeId) == end;
    }
);
```
