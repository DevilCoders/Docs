## About
Sometimes there are network cards with the new Mellanox chipset.  
Our custom kernel does not recognize these cards correctly, and we need to build the actual mlx5 driver.  

## How to build it
Download latest tarball with scripts from [official site](https://docs.nvidia.com/networking/display/ConnectX6DxEN/Linux+Driver+Installation).  
Unpack downloaded tarball and run:

    ./mlnxofedinstall --without-dkms --add-kernel-support --kernel <kernel version in chroot> --without-fw-update --force

Copy dkms files from `/lib/modules/` directory to this package and build them.
