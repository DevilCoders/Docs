# Mellanox MFT
This directory contents Mellanox Firmware Tools

## How to update
* Go to https://network.nvidia.com/products/adapter-software/firmware-tools/
* Select newest version for Linux deb-bases x64
* Download tarball
* Upload it to sandbox with `ya upload --ttl=inf mft_VERSION.tgz`
* Update version.inc with the new version and sandbox resource id

## How to build
DEB packages from mft tarball are pre-built, except the DKMS part
As we do not want to build kernel module on every switch, here we build it inside qemu VM
All other debs from the original tarball are extracted in the `debs` subdirectory during `ya make` execution

