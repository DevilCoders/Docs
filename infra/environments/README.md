# Directory structure

Each environment has following structure:
```
 |- ENVIRONMENTS_ROOT
 | | ${env_name}
 | | | script                              (sources - build scripts and configs)
 | | | script/*.sh                         (build scripts for main phase)
 | | | script/$phase/*.sh                  (scripts for phases bootstrap/pre-os/post-os)
 | | | script/SHA1SUMS                     (digest - hashes of all scripts)
 | | | script/config/config.inc            (environment config file)
 | | | script/config/config-$flavor.inc    (flavored config file)
 | | | $virt_mode-layer                    (build app/os/vm layer, OUT:layer.tar.gz)
 | | | | test
 | | | $virt_mode-layer-$flavor            (flavored app/os/vm layer, OUT:layer.tar.gz)
 | | | | test
 | | | vm-image                            (build vm image from vm-layer, OUT:rootfs.img)
 | | | | test
 | | | vm-image-$flavor                    (buld vm image for vm-layer-$flavor, OUT:rootfs.img)
 | | | | test
 | | | release                             (Place for released resource)
 | | | | $virt_mode-layer                  (OUT:layer.tar.gz)
 | | | | | test
 | | | | $virt_mode-layer-$flavor          (OUT:layer.tar.gz)
 | | | | | test
 | | | | vm-image                          (OUT:rootfs.img)
 | | | | | test
 | | | | vm-image-$flavor                  (OUT:rootfs.img)
 | | | | | test
```

See example in `template`

[layer build pipeline draft](https://st.yandex-team.ru/KERNEL-271)

# Environments types

## Regular environment
Normal environments which build from sources and may be released, for example see [qavm-bionic](file://qavm-bionic)

## Reference environmens
Has no build sources, just a reference to released resources from other environments, example [qavm](file://qavm)

## Flavors
Ya.makes for targes with flavor must include config-$flavor.inc rather than config.inc.
Config-$flavor.inc should define `ENV_FLAVOR` and enviroment variables for tuning scripts.
This allows to keep all parameters in one place.

# Build and CI

All scripts are hashed in digest (SHA1SUMS) and build targets depend on it.
Build target updates digest and saves hash of digest into /etc/yandex_environment.json

Layer build is time consuming process, ~240sec on each layer. Build is masked by ```AUTOCHECK``` flag.
```
 # Build layer from scratch
 ya make -tt infra/environments/qavm-bionic
 # Check all released images
 ya make -DAUTOCHECK -t infra/environments
```

Force rebuild after changes:
```
 # edit scripts
 \>script/SHA1SUMS
 ya make -tt app-layer
```

[Testenv CI job](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/runtime_cloud/BuildRuntimeEnvironments.yaml)

# Building sequence for script pack

Builder copy script directory into environment.
At each phase scripts run in alphabetical order.

```
mkdir	<layer_root>
chdir	<layer_root>
unpack	<base_layers>
run	<script_pack>/bootstrap/*.sh
chroot	<layer_root>
run	<script_pack>/pre-os/*.sh
start	<os>
run	<script_pack>/*.sh
stop	<os>
run	<script_pack>/post-os/*.sh
pack	<layer_root>
```

# Enviroment variables

```
virt_mode = "app"|"os"|"vm"
with_openssh_server - install ssh server (for virt_mode != vm)
root_password_encrypted = password encrypted with mkpasswd -m sha-512
root_authorized_keys = public ssh keys for root access
```

## Variables for `virt_mode=vm` and defaults

```
KERNEL_PACKAGE = "linux-image-virtual"
KERNEL_VMLINUX = "vmlinuz"
KERNEL_INITRD = "initrd.img"
KERNEL_ROOT = "LABEL=rootfs"
KERNEL_ROOT_FSTYPE = "ext4"
KERNEL_ROOT_FLAGS = "errors=panic"
KERNEL_CMDLINE = "ro console=tty1 console=ttyS0,115200n8 loglevel=7 oops=panic panic=60"
```

# BEST PRACTISE

* non-obvious steps must be documented
* add new steps as separate scripts
* relation between scripts must be documented and checked
* at any error log something and crash
* set default for environment variables if possible
* validate envirioment variables in bootstrap
* use `tee >file <<EOF` to log written content
* any hacks are allowed
* log/dump whatever you want
* add flavor or child layer for extensions
* copy whole pack for deep changes
* to force rebuild truncate digest # >script/SHA1SUMS

# LINKS

## Old PORTOVM porto layers

https://wiki.yandex-team.ru/porto/layers/

https://a.yandex-team.ru/robots//trunk/genconf/PORTOVM/


## RTC images

https://wiki.yandex-team.ru/runtime-cloud/virtual_images/


## DCA/HAAS/RND/SETUP Base Images

https://wiki.yandex-team.ru/dca/services/setup/user/peculiarity-of-ubuntu-images/

https://wiki.yandex-team.ru/dca/services/setup/devops/base-images/utils/

https://github.yandex-team.ru/HaaS/yandex-setup-base-image-utils

https://github.yandex-team.ru/HaaS/yandex-setup-base-image-utils/blob/dev/src/usr/sbin/setup-base-image-create


## Ubuntu images

https://cloud-images.ubuntu.com

https://git.launchpad.net/livecd-rootfs


# KNOWN ISSUES

* cloud-init network-config does not work before xenial

* ubuntu cloud-image bionic has 5 second boot delay


