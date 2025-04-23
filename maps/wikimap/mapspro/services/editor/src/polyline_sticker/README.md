# Algorithm purpose

Algorithm takes set of polylines and reduces gaps between vertexes and edges,

which fall below given tolerance.

Polygons are represented as a set of closed polylines.

# Algorithm description

Polylines inserted and indexed

Each polyline represented as number of vertexes.

At start vertexes are not shared

Vertex considered fixed if owning polyline inserted as fixed

That means a vertex shouldn't be moved or replaced in rings

# Algorithm

1 Index all polylines vertexes

2 For each not fixed vertex replace all polylines's references to it with neighbour within tolerance distance

3 For each polyline segment insert vertex between ends within tolerance distance

4 Repeat from step 1 if steps 2 and 3 produces any updates, since geometry gaps may change

5 Remove sequential duplicates from polylines vertexes

# Known flaws

May produce degenerate polylines if input contains many vertexes in close range
