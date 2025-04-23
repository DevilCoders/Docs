# Apparmor

This repo contains apparmor profiles. They are wrapped into the debian packages for the ease of the installation.  
Apparmor is a part of the kernel(one of LSM's), which controls an application behaviour using a whitelist of allowed actions.  
## Usefull links

what is apparmor: https://en.wikipedia.org/wiki/AppArmor  
detailed: https://en.opensuse.org/SDB:AppArmor_geeks  
how to create a profile: https://wiki.yandex-team.ru/cloud/security/research/Apparmor/  
how to process apparmor alerts: https://wiki.yandex-team.ru/cloud/security/security-duty/apparmor-alert/  

### Installing

Just add the repository to the ```/etc/apt/sources.list``` and install the package. 

### Misc
Abstractions and tunables are just some common parts, included in every profile.

