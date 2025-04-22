# VMexec tool
It acts as exec\(1\) but it transparently executed inside qemu VM.
A better alternative to docker run

## Features
* Real root capabilities
* Configurable execution environment
* Configurable HW environment
* Docker like volume management


## Quick examples
### Run vmexec in interactive mode
```
$ ya tool vmexec -- --trap
root@qavm-c3c27d43:~# apt-get update
....
```

### Forward host directory inside vm and run interactive mode
```
$ echo myfile > /tmp/myfile
$ ya tool vmexec -- -v /tmp/:/tmphost --trap
root@qavm-c3c27d43:~# df -h /tmphost/myfile
Filesystem      Size  Used Avail Use% Mounted on
volume-1         92G   70G   18G  81% /tmphost
```
### Execute "uname -a" inside VM and exit
```
$ ya tool vmexec -- -- uname -a
Linux qavm-479839ba.qemu 4.19.73-15 #1 SMP Wed Sep 18 09:41:35 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
