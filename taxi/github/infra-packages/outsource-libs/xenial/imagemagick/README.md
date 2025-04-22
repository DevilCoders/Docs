# ImageMagick
This is security update for **Xenial**, based on Debian patches. It will be replaced by the same update from Ubuntu (when released).

#### Building on non-Xenial 
You can use pbuilder following way:
- Generate dsc file (along others):
  - $ debuild -S
- Create build (chroot) environment with Xenial:
  - $ sudo pbuilder --create --distribution xenial --components "main restricted universe multiverse" --othermirror "deb http://mirror.yandex.ru/ubuntu/ xenial-backports main restricted universe multiverse" --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz
- Build ImageMagick packages:
  - $ sudo pbuilder --build --distribution xenial --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz ./imagemagick_6.8.9.9-7ubuntu5.9yandex0.dsc

All the packages will appear in /var/cache/pbuilder/result directory (by default).
