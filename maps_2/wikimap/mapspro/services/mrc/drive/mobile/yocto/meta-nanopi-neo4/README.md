Yocto meta layer for NanoPi-Neo4.
----

This meta layer expands the [meta-rockchip](https://github.com/rockchip-linux/meta-rockchip)
layer and adds the [armbian](https://github.com/armbian/build) BSP
for the NanoPi-neo4. The layer also supports libmali for 3D acceleration.

There's a blog post [here](https://www.stupid-projects.com/nanopi-neo4-yocto-meta-layer/)
with some more info about this layer.

## Distros
The available supported distros are
* `rk-none`: For no graphics support (only console images)
* `rk-wayland`: For Wayland support (it uses Weston)
* `rk-w11`: For Xorg support
* `rk-xwayland`: For Xorg+Wayland support

## Images
The images that are supported are:
* `rk-image-base`: The base image with a few basic packages
* `rk-image-multimedia`: Includes libdrm and gstreamer
* `rk-image-qtwayland`: Supports Qt5 with qtwayland (currently doens't work)
* `rk-image-testing`: A full blown image with a lot of debugging and test tools

The testing image includes a lot of extra tools and includes them as `packagegroups`.
You can find and edit those packagegroups in `meta-nanopi-neo4/recipes-images/packagegroup`.

The images are located in `meta-nanopi-neo4/recipes-images/images` and you can use them
to create your own custom images (e.g. a Qt5 image that includes all the testing tools).

The image build results in a `wic.bz2` file and you can use the
[bmap-tools](https://github.com/intel/bmap-tools) to flash it like that:
```sh
bmaptool copy build/tmp/deploy/images/nanopi-neo4/rk-image-testing-nanopi-neo4.wic.bz2 /dev/sdX
```

> The great thing with bmap is that you can flash huge images in an SD card in a few
seconds (depending of course the amount of real binary data in the image).

You can control the size of rootfs by changing the value of the `ROOT_EXTRA_SPACE` in
`meta-nanopi-neo4/classes/nanopi-neo4-create-wks.bbclass`. You can override this value
either in this file or in your `local.conf` file.

By default there's a small swap partition in the image and you can control the size
with the `RK_SWAP_SIZE` parameter in `meta-nanopi-neo4/classes/nanopi-neo4-create-wks.bbclass`.
If you don't want to use swap the set this value to `0` like this:
```sh
RK_SWAP_SIZE = "0"
```

## Default `local.conf` and `bblayers.conf`
There's a script that prepares the build environment that uses a default `local.conf.sample`
and `bblayers.conf.sample` file that are located in `meta-nanopi-neo4/conf/`.

## Versions
Some useful component versions for this layer:
* `u-boot`  : 2019.01
* `Kernel`  : 4.4.213
* `libmali` : r14p0

## How to use this layer
This layer has some other layer dependencies. Create a new working folder and then in this
folder run these commands:

```sh
mkdir sources
cd sources
git clone -j 8 git@bitbucket.org:dimtass/meta-nanopi-neo4.git
git clone -j 8 -b thud git@github.com:meta-qt5/meta-qt5.git
git clone -j 8 -b sumo git@github.com:openembedded/meta-openembedded.git
git clone -j 8 -b sumo git://git.yoctoproject.org/poky
git clone -j 8 git@github.com:rockchip-linux/meta-rockchip.git
cd ..
ln -s sources/meta-nanopi-neo4/scripts/setup-environment.sh
ln -s sources/meta-nanopi-neo4/scripts/flash-sd.sh
```

The commit hashes I've succesfully tested are:
* `meta-rockchip`: 226b2b3f4b584943cd1f0436cfae6285edbefe10
* `poky`: cbb677e9a09d5dad34404a851f7c23aeb5122465
* `meta-openembedded`: 8760facba1bceb299b3613b8955621ddaa3d4c3f
* `meta-qt5`: 360ca76d24453a57d4b7b50577771cc882d62be2

These commands will create a `sources/` folder and also a link to the top level folder
that points to the build prepare script. Then you need to call this script by passing
two arguments. One is the `MACHINE` and other the `DISTRO`. `MACHINE` is always
`nanopi-neo4` and `DISTRO` can be one of the supported ones of this layer (see: above).

Therefore, to build the image for the NanoPi-Neo4 and with `Wayland` support run this:
```sh
MACHINE=nanopi-neo4 DISTRO=rk-wayland source ./setup-environment.sh build
```

Then to build the `testing` image that includes a variety of testing, debugging and
development tools, run this:

```sh
bitbake rk-image-testing
```

To flash the image:
```sh
sudo IMAGE=testing ./flash_sd.sh /dev/sdX
```

> Note: Currently the Qt image doesn't work because the example application is
not available anymore. I'll fix this at a later point.

## Overclocking
There's a variable that if it's set then the overclocking is enabled for all CPUs
and the RAM. The `RK3399_OVERCLOCKING` is enabled by default in the `conf/machine/nanopi-neo4.conf`.
This adds the `recipes-core/rk-overclocking/rk-overclocking_1.0.bb` recipe in the
image. This service will set the following frequencies:
* `RAM`: 928MHz (default max is 800MHz)
* `CPU 0-3`: 1512MHz (default max is 1416MHz)
* `CPU 4-5`: 1992MHz (default max is 1800MHz)


## Benchmark
For the `rk-image-testing` and the rk-wayland `DISTRO`, you can use the `glmark2`
benchmark for testing the GPU. The image has two versions of the tool, the
`glmark2-es2-drm` and `glmark2-es2-wayland`. The first one you can just run it
from the uart console like this:
```sh
glmark2-es2-drm
```

This will also ouput the benchmark rendering on the screen. In case you want
to benchmark the raw GPU performance then you can run the benchmark and render
to an off-screen surface like this:
```sh
glmark2-es2-drm --off-screen
```

If you want to use the `glmark2-es2-wayland` then you need to do this in the
desktop environment. Therefore, you need to connect a keyboard and mouse to
the SBC. Then you need to export the `XDG_RUNTIME_DIR` and `WAYLAND_DISPLAY`
and then run the benchmark, like this:
```sh
export XDG_RUNTIME_DIR=/run/user/1000
export WAYLAND_DISPLAY=wayland-0
glmark2-es2-wayland
```

This is the output of `glmark2-es2-drm --off-screen`
```
=======================================================
    glmark2 2017.07
=======================================================
    OpenGL Information
    GL_VENDOR:     ARM
    GL_RENDERER:   Mali-T860
    GL_VERSION:    OpenGL ES 3.2 v1.r14p0-01rel0-git(966ed26).1adba2a645140567eac3a1adfc8dc25d
=======================================================
[build] use-vbo=false: FPS: 123 FrameTime: 8.130 ms
[build] use-vbo=true: FPS: 437 FrameTime: 2.288 ms
[texture] texture-filter=nearest: FPS: 482 FrameTime: 2.075 ms
[texture] texture-filter=linear: FPS: 476 FrameTime: 2.101 ms
[texture] texture-filter=mipmap: FPS: 482 FrameTime: 2.075 ms
[shading] shading=gouraud: FPS: 366 FrameTime: 2.732 ms
[shading] shading=blinn-phong-inf: FPS: 362 FrameTime: 2.762 ms
[shading] shading=phong: FPS: 319 FrameTime: 3.135 ms
[shading] shading=cel: FPS: 306 FrameTime: 3.268 ms
[bump] bump-render=high-poly: FPS: 234 FrameTime: 4.274 ms
[bump] bump-render=normals: FPS: 460 FrameTime: 2.174 ms
[bump] bump-render=height: FPS: 458 FrameTime: 2.183 ms
libpng warning: iCCP: known incorrect sRGB profile
[effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 219 FrameTime: 4.566 ms
libpng warning: iCCP: known incorrect sRGB profile
[effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 88 FrameTime: 11.364 ms
[pulsar] light=false:quads=5:texture=false: FPS: 485 FrameTime: 2.062 ms
libpng warning: iCCP: known incorrect sRGB profile
[desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 80 FrameTime: 12.500 ms
libpng warning: iCCP: known incorrect sRGB profile
[desktop] effect=shadow:windows=4: FPS: 250 FrameTime: 4.000 ms
[buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 35 FrameTime: 28.571 ms
[buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 36 FrameTime: 27.778 ms
[buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 39 FrameTime: 25.641 ms
[ideas] speed=duration: FPS: 74 FrameTime: 13.514 ms
[jellyfish] <default>: FPS: 268 FrameTime: 3.731 ms
[terrain] <default>: FPS: 16 FrameTime: 62.500 ms
[shadow] <default>: FPS: 74 FrameTime: 13.514 ms
[refract] <default>: FPS: 47 FrameTime: 21.277 ms
[conditionals] fragment-steps=0:vertex-steps=0: FPS: 464 FrameTime: 2.155 ms
[conditionals] fragment-steps=5:vertex-steps=0: FPS: 272 FrameTime: 3.676 ms
[conditionals] fragment-steps=0:vertex-steps=5: FPS: 368 FrameTime: 2.717 ms
[function] fragment-complexity=low:fragment-steps=5: FPS: 355 FrameTime: 2.817 ms
[function] fragment-complexity=medium:fragment-steps=5: FPS: 231 FrameTime: 4.329 ms
[loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 355 FrameTime: 2.817 ms
[loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 356 FrameTime: 2.809 ms
[loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 264 FrameTime: 3.788 ms
=======================================================
                                  glmark2 Score: 269
=======================================================
```


## Author
Dimitris Tassopoulos <dimtass@gmail.com>