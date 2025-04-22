# Build package

Install depencies:

    sudo apt-get install ruby-dev build-essential
    sudo gem install fpm

Download latest release tarball from [github](https://github.com/influxdata/telegraf/releases) and apply patch to extracted data (we're using 1.22.1 version as example):

    $ tar zxvf telegraf-1.22.1.tar.gz && cd telegraf-1.22.1
    $ patch -p1 <../0001-solomon-patch.patch

Build package:

    $ make clean package include_packages="amd64.deb"

Extract deb content to `package` directory:

    $ cd ../package
    $ ar -x ../telegraf-1.22.1/build/dist/telegraf_1.22.1~-0_amd64.deb
    $ tar zxvf control.tar.gz -C debian
    $ tar -zxvf data.tar.gz

    # Revert control, that by default doesn't contain Source section
    $ arc checkout -- debian/control

Update debian/changelog (append latest revision ID or hash) and run debuild:

    $ dch -i
    $ debuild
