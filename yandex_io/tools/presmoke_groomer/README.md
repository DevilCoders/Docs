## Tool for preparing device's config to be used for autopresmoke  

Usage example: ```./presmoke_groomer --presmoke_mode quasar.cfg```

Enabling presmoke mode makes all services listen on external interfaces and adds audioDevice section with tcp mic. It also saves the original version of config with suffix .orig.

If presmoke_mode is not specified the utility will print some presmoke-related info about config.  

## Use with adb

Update config for presmoke: ```./presmoke_groomer --presmoke_mode --use_adb```
In this mode presomke_groomer will pull quasar.cfg, update quasar.cfg and push quasar.cfg back to device by itself

Restore original config: ```./presmoke_groomer --restore --use_adb```
Push quasar.cfg.orig to device and reboot  device
