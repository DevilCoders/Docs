# yanet

## Quick Start

```
mkdir projects
cd projects
git clone git@noc-gitlab.yandex-team.ru:nocdev/yadecap.git
git clone git@noc-gitlab.yandex-team.ru:nocdev/dpdk.git

cd yadecap/utils
make install

cd ../../dpdk/
yanet-make T=x86_64-sandybridge-linuxapp-gcc O=x86_64-sandybridge-linuxapp-gcc config
yanet-make T=x86_64-sandybridge-linuxapp-gcc O=x86_64-sandybridge-linuxapp-gcc -j8

cd ../yadecap/dataplane/
yanet-make -j4

cd ../controlplane/
yanet-make -j4

cd ../autotests/
yanet-make -j4
```

## Сборка


```
docker build -t yadecap/build build_image

docker run -it -v `pwd`/:/ya/yadecap yadecap/build /bin/bash 

cd yadecap
cd libbgp
make 
cd ../controlplane
make  -j4 YANET_CONFIG_SUFFIX=autotest
cd ../dataplane
make RTE_SDK=/ya/dpdk/ RTE_TARGET=x86_64-sandybridge-linuxapp-gcc -j4 YANET_CONFIG_SUFFIX=autotest
cd ../cli
make  -j4 YANET_CONFIG_SUFFIX=autotest 
cd ../autotests
make  -j4 YANET_CONFIG_SUFFIX=autotest 
```

### Запуск тестов
enable user_allow_other' in /etc/fuse.conf
mount arc with --allow-root

```
arc mount --allow-root ...

docker run -it -v `pwd`/:/build registry.yandex.net/nocdev/yanet/build /bin/bash
cd /build
EXTRA_CFLAGS=-g EXTRA_LDFLAGS=-g make autotest
make run
PATH=$PATH:cli/build/ autotests/build/yanet-autotest autotests/units/001_one_port/0*

```
### Отладка
add -g flag to CFLAGS and LDFLAGS and rebuild

```
docker run -it -v `pwd`/:/ya/yadecap --cap-add=NET_ADMIN --cap-add=SYS_PTRACE --security-opt seccomp=unconfined yadecap/build /bin/bash
apt install gdb
gdb build/yanet-autotest
run units/001_one_port/001_default
```
