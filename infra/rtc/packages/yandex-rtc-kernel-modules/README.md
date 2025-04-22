## About
This directory contains rules to build various packages for `systemd-modules-load`.

## Note
Module loading implemented by 'systemd-modules-load' systemd unit. Modules are loaded at boot and refreshed (loaded if they ain't present in kernel) daily.
Systemd unit 'systemd-modules-load' it intended to load modules on host boot. 
We do not want to write own statefull moduels loadeder, becouse it costs too much for us in this monent. 
Kernel module removal operation is non-trivial and sometimes requires reboot, so modules removal handling should be implemented using module-specific scripts.
And now we had restrictions on some use cases. eg. now we can not unload kernel module using systemd-modules-load unit.

## Edit 
Modules configurations stored in etc/modules-load.d files. Packages declarations in pkgs dir.
Build packages with sandbox tasks, defined in a.yaml

## Deploy
* Change units.d files 
* Commit changes
* Create deployment PR's in core repo with hmctl `hmctl push units.d/systemd-modules-load.yaml  -c ALL -r core -m 'systemd-modules-load: bump to <rev>'`
