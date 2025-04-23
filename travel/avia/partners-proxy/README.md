# partners-proxy

Прокcи (3proxy) до партнеров через ipv4.

Исходники: https://github.com/3proxy/3proxy

## Сборка и загрузка бинарника 3proxy

Пример для версии `0.8.13`

Сборка:
```
$ wget -q  https://github.com/z3APA3A/3proxy/archive/0.8.13.tar.gz
$ tar -xf 0.8.13.tar.gz
$ cd 3proxy-0.8.13/
$ make -f Makefile.Linux
```

Загрузка ресурса в Sandbox:

```
$ ya upload --type AVIA_3PROXY_BINARY --owner AVIA --description "3proxy-0.8.13 binary" --arch linux --attr 3proxy_version=0.8.13 --attr platform=$(uname -i) src/3proxy
```

В интерфейсе sandbox нужно зарелизить ресурс.

После загрузки идентификатор ресурса необходимо прописать в `pkg.json`

## Локальная сборка и загрузка в sandbox
```
$ ya package --checkout --tar --upload --sandbox --owner=AVIA travel/avia/partners-proxy/pkg.json
```
