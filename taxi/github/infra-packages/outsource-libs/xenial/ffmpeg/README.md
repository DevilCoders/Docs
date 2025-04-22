# ffmpeg
The backport for **Xenial** depends on:
- libmysofa
- libopenmpt

Their sources also here. First you must build and install the libraries (-dev debs), then build ffmpeg.

#### Building on non-Xenial 
You can use pbuilder (>=0.215+nmu4) following way:
- Generate dsc files (along others) for dependant libs and ffmpeg:
  - $ debuild -S
- Create build (chroot) environment with Xenial:
  - $ sudo pbuilder --create --distribution xenial --components "main restricted universe multiverse" --othermirror "deb http://mirror.yandex.ru/ubuntu/ xenial-backports main restricted universe multiverse" --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz
- Build libmysofa and libopenmpt packages:
  - $ sudo pbuilder --build --distribution xenial --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz ./libmysofa_0.6~dfsg0-2yandex0.dsc
  - $ sudo pbuilder --build --distribution xenial --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz ./libopenmpt_0.2.8760~beta27-1yandex0.dsc
- Create repo with just built libraries:
  - $ sudo bash -c "cd /var/cache/pbuilder/result/ && dpkg-scanpackages . /dev/null > ./Packages"
- Add the repo to build env:
  - $ sudo pbuilder --update --override-config --distribution xenial --components "main restricted universe multiverse" --othermirror "deb http://mirror.yandex.ru/ubuntu/ xenial-backports main restricted universe multiverse|**deb file:/var/cache/pbuilder/result/ ./**" --bindmounts "/var/cache/pbuilder/result" --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz
- Build ffmpeg packages:
  - $ sudo pbuilder --build --allow-untrusted --bindmounts "/var/cache/pbuilder/result" --distribution xenial --architecture amd64 --basetgz /var/cache/pbuilder/xenial-amd64-base-backports.tgz ./ffmpeg_3.4.1-1yandex0.dsc

All the packages will appear in /var/cache/pbuilder/result directory (by default).
