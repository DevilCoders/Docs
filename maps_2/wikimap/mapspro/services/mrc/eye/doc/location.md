# Location
## Position
There is the global coordinate system. It is expansion of the [Mercator](https://en.wikipedia.org/wiki/Mercator_projection) projection. The **X** is directed from West to East, **Y** from South to North, **Z** – up. On the one hand, this is very convenient system, but requires careful work with distances (the scale changes depending on the latitude). However in small neighborhood you may work as in normal Euclidean space, it's rather possible to shift scale into meters. Also we may assume that height is always 0 to simplify the model.

## Orientation
Often there is a need to fix the orientation of some objects (e.g. direction of camera shooting). Let's define the coordinate system for each object type (camera, sign, traffic light, etc), then rotation from global to object axes specifies orientation of object in space. Actually position of object defines translation vector, but we assume that the centers are aligned already.

### Axis and angle
It's proved that any rotation can be set with unit vector $v$ describing an axis of rotation and angle $\theta$. This is probably the most intuitive way to set the orientation, but not so practical. Rotation of axes by angle $\theta$ is rotation of space by $-\theta$ with the same axis. So vector $p$ transforms to $p_{r}$
$$
p_{r} = p \cos\theta + (v \times p)\sin\theta + v ~ (v \cdot p) (1 - \cos\theta).
$$

### Rotation matrix
Rotation is also linear transformation. Let's $x_o, y_o, z_o$ is orthonormal basis vectors of object in global coordinates. Concatanate ones in matrix $R = [x_o|y_o|z_o]$, which specifies rotation of global axis to object axes, but $R^{-1} = R^T$ sets space rotation ($p_g$ – vector in global coordinates, $p_o$ – in object axis).
$$[x_o, y_o, z_o] = R \cdot [x_g | y_g | z_g] = R \cdot I$$
$$p_{o} = R^{-1} \cdot p_{g}.$$

At the same time $R^{-1}$ specifies rotation of object axis to global and $R$ is reverse rotation of space.
$$I = [x_g, y_g, z_g] = R^{-1} \cdot [x_o | y_o | z_o]$$
$$p_{g} = R \cdot p_{o}.$$

For a given axis of rotation and angle, it's possible to find transformation in matrix form
$$p_{r} = \Big(I + \sin\theta \cdot V  + (1 - \cos \theta) V^2 \Big) \cdot p$$
$$
V = \left[
    \begin{array}{ccc}
    0 & -v_z & v_y \\
    v_z & 0 & -v_x \\
    -v_y & v_x & 0
    \end{array}
\right].
$$

Inverse transformation can be also done easily, since
$$
\sin\theta\left[
    \begin{array}{ccc}
        0 & -v_z & v_y \\
        v_z & 0 & -v_x \\
        -v_y & v_x & 0
    \end{array}
\right]
= \frac{V - V^T}{2}.
$$

### Quaternion
[Quaternion](https://en.wikipedia.org/wiki/Quaternion) is the least intuitive, but compact and computationally convenient way to set rotations in space. Quaternion is used to store rotation global axis to object ones. At the same time it's transformation from the object space to the global one. So, for rotation axis $v$ and angle $\theta$ $p$ transforms to $p_{r}$.

$$q = \cos \frac{\theta}{2} + \sin\frac{\theta}{2} \cdot (v_x \mathbf{i} + v_x \mathbf{j} + v_x \mathbf{k})$$
$$p_{r} = qpq^{-1}.$$

## Frame
### Axes
Location of frame is fixed with two parameters. The first is position of camera in mercator coordinates. The second is orientation of frame, which is fixed with rotation transformation.

Pinhole camera | Frame axes
------------ | -------------
![Pinole camera](https://proxy.sandbox.yandex-team.ru/1371271342) |![frame axes](https://proxy.sandbox.yandex-team.ru/1379681146)


Look at a simple example, let the frame look to the North and have no other rotations, then orientation in matrix form is
$$
R = \left[
    \begin{array}{ccc}
        1 &  0 & 0 \\
        0 &  0 & 1 \\
        0 & -1 & 0
    \end{array}
\right].
$$

### Rotation decomposition
Rotation of frame axes may be decomposed into 3 parts:
- **heading** – azimuth of shooting, projection of frame $Z$ axis on global plane $XY$.
- **orientaiton** – orientation of frame $X$ and $Y$ axes in projection plane, reduced to 4 exif orientations.
- **pitch** – angle between frame axis $Z$ and the global plane $XY$.

## Feature
### Heading + orientation
For a set of images only azimuth of camera movement (heading) and exif [orientation](https://proxy.sandbox.yandex-team.ru/1378979166) are known. It is assumed that the camera looks in the direction of movement without any [pitch](https://en.wikipedia.org/wiki/Aircraft_principal_axes) rotation. For side shooting, suppouse that the camera is directed to the right of the movement. Hence, rotation may be decomposed into following steps:
- Using the matrix form, fix the default orientation of the camera to the East.
- Rotate around $Y$ axis to specify heading.
- Rotate around $Z$ axis for exif orientation.

### Camera Rodrigues
For some features orientation of camera is known. It's stored as 3d vector $r$ ($\theta$ is angle of rotation, $v$ – axis)
$$
r = \begin{cases}
    \theta \cdot v, ~ \theta > 0 \\
    (0, 0, 0), ~ \theta = 0.
\end{cases}
$$

There is conversion from camera Rodrigues to quaternion rotation (simple axes switching).

Camera Rodrigues | Frame axes
------------ | -------------
![Camera Rodrigues](https://proxy.sandbox.yandex-team.ru/1379691809) | ![frame axes](https://proxy.sandbox.yandex-team.ru/1379681146)
