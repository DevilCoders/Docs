# Equirectangular to perspective image reprojection

The algorithm used in `getCoordinateMapsForPinhole` for reprojection of
equirectangular panorama is described here.

## Algorithm description

To create a perspective projection with given horizontal field of view `hFOV`
and image height `h` and width `w`, we rotate points of the image plane and
project them to a sphere of fixed radius `R`. Given the coordinates of a
projection (longitude and latitude) we can directly sample points from the
equirectangular image (panorama) to get perspective view. This is ilustrated on
the image (for simplicity looking only on the horizontal axis).

![Reprojection](https://jing.yandex-team.ru/files/irubachev/Projection.png)

Algorithm works as follows:
1) Create coordinate maps of size `h x w` by rotating (given a direction) normalized 3d points `[x,y,R]` (where `x,y ∈ [−1,1]`
2) Computing horizontal and vertical angles where the ray through the center of projection and this point intersects panorama (on the picture above this is clearly `atan2(x,R)`
3) Sampling projected image from panorama using computed coordinates.

## Examples

Example of a reprojection (done using the described algorithm)
![example](https://jing.yandex-team.ru/files/irubachev/example.png)

## Note

Resulting image might look distorted, if field of view is wide (> 100 degrees).


