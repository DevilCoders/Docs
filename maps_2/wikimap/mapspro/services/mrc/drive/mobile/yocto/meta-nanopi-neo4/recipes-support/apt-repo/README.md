Web server for DEB packages
----

This tool is meant to be used by developers in order to install DEB
packages on various embedded Linux boards. Because it's a quite gereric
tool and can be used in various ways I'll try to explain only specific
use cases.

## Install
The tool is based on the `SimpleHTTPServer` library of `Python`. Therefore,
to use it you need to have Python3 installed. You can also choose if you like
the server to automatically detect changes in the `www` folder. If you want to
support detection then you need to also install `inotify-tools`
```sh
sudo apt install inotify-tools
```

## Usage
Using the `runwebserver.sh` is a two step procedure. First you need to paste
all the DEB packages inside the `www` folder and then run the tool.
```sh
./runwebserver.sh
```

If the `www` folder doesn't exists then it will be created automatically and also
the the `Packages.gz` will be created in `www`. Therefore, to be sure you can the
server once after git-cloning and then exit.

By default, `amd64` is used as `ARCH` in the apt list. To change this you need to
either edit the `runwebserver.sh` script or run it with a different architecture,
like this:
```sh
ARCH=arm64 ./runwebserver.sh
```

If you don't need to detect package changes inside the `www` folder then you can
run the server with the `WATCH` flag set to false.
```sh
WATCH=false ./runwebserver.sh
```

By default the script chooses the first available net-if is found with `ifconfig`.
Therefore, if you have more than one net-if (e.g. docker, qemu, USB-to-ETH e.t.c.)
then it's better to specify the IP of the desired net-if manually in the command
like this:
```sh
MY_IP=192.168.0.100 ./runwebserver.sh
```

If you run the web-server with the `inotify` support then you can copy-paste deb
packages in the `www` folder at any time and then install them from the target
without the need to restart the `runwebserver.sh` script.

There is an assumption here, that the default deb repo is located in
`apt.native-instruments.de`, which is not the case for the time being. Therefore,
the script suggests that we override the default repo.

Finally, you need to add your local apt repo to the target. To do this you need
to copy the text that the `runwebserver.sh` script suggests to the target. That is
also the fastest way to add it there. For example, if you run the script then it
might printout this text

```sh
[...]
-------------------------- start copy -------------------------
cat > /etc/apt/sources.list.d/yocto.list << 'EOF'
deb [arch=aarch64 trusted=yes] http://192.168.0.100:8000 www/
EOF

cat > /etc/apt/preferences.d/yocto.pref << 'EOF'
Explanation: local development should always be preferred
Package: *
Pin: origin 192.168.0.100
Pin-Priority: 1010
EOF
-------------------------- stop copy --------------------------
[...]
```

This means that you need to run these two commands on the target either by the RS232
terminal or an ssh terminal. These will add the new `yocto` repo in the apt list
and setup the preferences of the repo. Therefore, copy paste those two commands and
then do an update:
```sh
apt-get update
```

and then install the package you like
```sh
apt-get install <package-name>
```

> Of cource, the deb packages have to be the same ARCH as the target and also built
with the correct toolchain.

To remove a package:
```sh
apt-get remove <package-name>
```

To search for a package:
```sh
apt-cache search <package-name>
```

## Server script
In the `apt-server` folder you'll find some bash scripts that automate a bit the procedure.
Copy the content of the folder to the server and create a folder in the same level with the
scripts that is named for example `www-arm64` and copy in there all the deb packages you
want to serve and execute the `start_apt_server.sh` with the correct `ARCH`, `PORT` and `REPO`
parameters.

## Limitations
This script only supports a single architecture. Therefore, if you want to use two
different architectures at the same time you need to run two instances from a different
path and use different ports. The same net-if can be used though. This is how you do this:

Run the default `arm` arch with the default `PORT=8000`.
```sh
cd /path/to/webserver1
ARCH=arm PORT=8000 ./runwebserver.sh
```

Run another `arm64` arch server on another port.
```sh
cd /path/to/webserver2
ARCH=arm64 PORT=8001 ./runwebserver.sh
```

Of course, in both cases you need to run the printed commands to the target to install
the apt list.

#### Author
Dimittris Tassopoulos