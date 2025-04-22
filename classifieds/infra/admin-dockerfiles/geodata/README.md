# vertis/geodata Dockerfile

## Build

**NOTE:** you must have proper geodata binary in `/var/cache/geobase` on the build system.

~~~
› GEOBASE_VERSION=4 make
~~~

The command above will build data container `vertis/geodata<GEOBASE_VERSION>` which can be exported with the command:

~~~
› GEOBASE_VERSION=4 make export

› ls build/
geodata4_69b6fa82c2e0.tgz
~~~

## Usage

Now you can import geodata container into your local docker instanse:

~~~
› scp <remote-host>:/path/to/geodata4_69b6fa82c2e0.tgz /tmp/docker_geodata4_latest.tgz
···
› docker import - registry.ape.yandex.net/vertis/geodata4 < /tmp/docker_geodata4_latest.tgz
› docker run -v /var/cache/geobase --name geodata4 registry.ape.yandex.net/vertis/geodata4 /true
~~~

After that, you can use `geodata4` container as an average data container, with `--volumes-from geodata4` flag.

~~~
› docker run --rm -ti --volumes-from geodata4 registry.ape.yandex.net/vertis/base:0.1 ls -o /var/cache/geobase
total 463912
-rw-r--r-- 1 root 475043612 Jun 25 12:27 geodata4.bin
~~~
