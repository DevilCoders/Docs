Sign area hypotheses
===

Calculates area and location of a given sign using results of the third (Toloka) stage. The calculations are based on knowledge of:
- A horizontal and vertical angle span, bearing and location of a panorama.
- An image resolution.
- A bounding box of the sign.
- A shape of a building on which the sign may be placed.

Technicalities
---

This is a very high level look at how algorithm works.

> Trigonometry is a pathway to many abilities some consider to be unnatural.

First of all we need to find building facade *on which the sign is placed*. For this, we use the building shape and shapes of all its neighbors (all building geometry shapes can be found [in Garden](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/bld_geom&)). 

After that we translate coordinates of the bounding box (which is in our case a 4-sided polygon) to angular distances

```python
def to_angle(x, y, width, height):
    # h_angle_span, v_angle_span - is a panorama angle span

    y_norm = y / height - 0.5
    x_norm = (x / width - 0.5) * np.cos(
        # distortion correction
        # the higher a horizontal segment on the panorama the longer it looks
        np.deg2rad(y_norm * v_angle_span))

    return x_norm * (h_angle_span), y_norm * (v_angle_span)
```

Then we are drawing lines through the location of our panorama with the given angles in order to find intersections with the "neighborhood" geometry.

```python
"""
In code, localization is a tuple of:
    1. Geodesic location of an intersection on the map
    2. Building face on which this intersection is placed

Here we also pick angle relative to which we will calculate the coordinates
of projection - called reference_angle
"""
angle_localization = {}

reference_angle = (0.0, 0.0)
for angle in angles:
    # function returns (location, intersected face)
    localization = get_intersection(
        pn_pos, pn_bearing,
        # horizontal angle
        angle[0],
        building_faces)
    # and if it exists
    if localization:
        angle_localization[angle] = localization
        reference_angle = angle
```

For the next part we assume that the building facade (*on which the sign is placed*) is the perfect infinite plane orthogonal to Earth ground with a coordinate system centered on the reference angle. We want to find coordinates of the sign's projection in this coordinate system, then

```python
localized_sign_corners = []
for angle in angles:
    h_angle, v_angle = angle

    localization = angle_localization.get((h_angle, v_angle))

    # …skipped code for cases, then we didn't find any localization…

    # we are interested only in intersection geodesic location
    intersection, _ = localization

    # because we know a real world location, we can just simply calculate 
    # a real world distance between panorama and intersection point
    intersection_distance = distance(Point(pn_pos), intersection)

    localized_sign_corners.append((
        # imagine upper view of the scene
        # 
        #           | reference point
        #           v
        # ----------*-------*-----
        #           |       ^
        #           |       | projected point
        #           |
        #           |
        #           * <- camera
        # 
        # x coordinate is the real world distance between intersection point
        # and reference angle intersection point (or simply reference point)
        distance(
            intersection,
            # location of reference_angle intersection
            angle_localization[reference_angle][0]
        ) * np.sign(h_angle),
        # imagine a side view of the scene
        # 
        #          | <- wall
        #          |
        #        ^ * <- projected point    
        #        | |                   
        # height | |                   | camera
        #        | |                   v
        #        v |___________________*
        #          <------------------->
        #                distance
        # 
        # y is the height
        # to find the height we use some basic trigonometric formula
        np.tan(np.deg2rad(v_angle)) * intersection_distance
    ))
```

After that, we just calculate area of a polygon with the given coordinates, that's it!

Help
---

```console
~/arcadia/maps/poi/streetview_poi/sign_hypotheses/sign_area$ ./sign_area --help
usage: sign_area [-h] [-t THIRD_TASK_RESULTS_PATH] -o OUTPUT_TABLE_PATH
                 [-p PN_DESCRIPTION_PATH] [-b YMAPSDF_BLD_GEOM_TABLE]

Calculates signs area.

optional arguments:
  -h, --help            show this help message and exit
  -t THIRD_TASK_RESULTS_PATH, --third-task-results-path THIRD_TASK_RESULTS_PATH
                        path to toloka third task results table on yt
  -o OUTPUT_TABLE_PATH, --output-table-path OUTPUT_TABLE_PATH
                        path to output table on yt
  -p PN_DESCRIPTION_PATH, --pn-description-path PN_DESCRIPTION_PATH
                        path to panoramas description table on yt
  -b YMAPSDF_BLD_GEOM_TABLE, --ymapsdf-bld-geom-table YMAPSDF_BLD_GEOM_TABLE
                        path to ymapsdf buildings' geometry table on yt

```
