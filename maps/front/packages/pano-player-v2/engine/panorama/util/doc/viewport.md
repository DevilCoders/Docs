# Visible tiles calculation

Camera's visible area is restricted by a pyramid and when we use it for a panorama projected onto a sphere
to identify visible tiles (and load only them) we have to calculate intersection on the pyramyd's four planes
and the sphere, find out intersected tiles and tiles inside the region.

First of all the following conventions are used for panorama projection mapping, axis and angles directions:

![](./panorama_projection_convention.svg)

For a horizontal plane (as well as for vertical one) to find which tiles are intersected we build an equation
of plane and sphere intersection and then map vertical and horizontal angles onto the equirectangular panorama projection.

The bottom plane of the camera's pyramid in 3D has the following equation (camera is looking along the X axis):

$$ \tg(Θ)x - y = 0 $$

![](./sphere_plane_intersection.svg)

Camera (and its particular plane) azimuth rotation is not considered here (it is easier to do by adding φ shift later).

Shpere equation in the model above:
$$
x = r \cos(φ)\cos(θ)\\
y = r \sin(φ)
$$

Radius coud be normalized, i.e. `r=1` could be used withoud compromising the correctness. These sphere coordinates are to be
substituted into the plane equation, we get:

$$ \tg(Θ)\cos(φ)\cos(θ) - \sin(θ) = 0 $$

Thus we can express tilt angle via azimuth angle (and vice versa with considering periods of trigonometry functions):

$$ θ = \arctan(\tg(Θ_{plane})\cos(φ)) $$

Similar reasoning will work for vertical planes.

$$
θ = \pm \arccos(\sin(Φ_{plane}) / \sin(φ))\\
φ = \arcsin(\sin(Φ_{plane}) / \cos(θ))
$$

These equations implemented could give a picture like this (black lines - are the curves of intersection projected onto the panorama):
![](./camera_planes_sphere_impl.png)