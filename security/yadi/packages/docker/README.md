Docker yadi wrapper
===================

If you need to run Yadi in Drone.io pipeline, please use [drone-yadi](https://a.yandex-team.ru/arc/trunk/arcadia/security/yadi/packages/drone-yadi) image.

## Installation

```
docker pull registry.yandex.net/product-security/yadi:latest
```

## Usage

```
docker run --net host -w `pwd` -v `pwd`:`pwd` registry.yandex.net/product-security/yadi:latest test
```
