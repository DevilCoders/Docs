#### Loading gps tracks from YT

Signals are filtered by bounding box given in arguments. They are sorted by uuid and then by time on YT. Table of signals is saved to a tab-separated values file as a sequence of **Signal** structures. There is a hard limit for the number of signals that can be loaded from YT.

#### Generating edges from tracks

This procedure takes a number of signals from a file, forms tracks and generates edges based on them. Signals in the file should be sorted by uuid and then by time. Optionally it saves intermediate data into files that may be read by EasyView (for visualization) and further part of hypotheses generating (in a separated launch mode).

**Tracks** are constructed from a sequence of signals with the same uuid. In one track consecutive signals are bounded by *maximal time difference* and *maximal distance*.

The turns in the tracks (**turn samples**) are detected by the change of movement and speed. There is *maximal turning speed* and *minimal change of angle* of a trajectory.

The turn samples are clustered to form **turns** of the roads. For each turn sample other samples with similar turn angle (in and out angle differences are bounded by *maximal turn angle difference*) and position (*turn cluster distance*) are grouped together. Turn samples of one cluster are averaged to form a turn of a road. Each turn has *weight* - number of turn samples that formed it.

Road turns are clustered the same way (with distance bounded by *cross cluster distance*) to form **intersections** (crossroads). The position of the intersection is a weighted average of the positions of the turns.

**Link** is a part of one track between two consecutive intercections.

Links of one pair of intercections are averaged in a special way to form an **edge** (polyline of a road). Points of each link are projected on a line formed by intercections. Algorithm travels along projection. At each position, where point of a link exists, it takes a group of interpolated points of all links and averages them to form a point of the edge.


#### Geometrical difference between hypotheses and editor graph

Editor **graph** is loaded with revision library. It is split in tiles with *cell span* size and loaded with one request per tile.

Each **hypothesis edge** is assigned to a tile (several if crossess a tile edge).

Tiles are processed separately. Buffer polygon is constructed around all **graph edges**. For every **hypothesis edge** this polygon is geometrically subtracted, leaving only *non-present in the graph* part of hypothesis.

If metric needs to be calculated, hypotheses and editor graph are swapped.

After final hypotheses acquired they are written to a file in the import format for hypotheses of the editor.

Results are optionally rendered for EasyView visualization.
