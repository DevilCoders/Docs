## Functional manual tests

To do tests on testing server:
https://api-maps.tst.c.maps.yandex.ru/${version}/tests/manual/index.html

To test local api instance:
1. Launch api instance (see how in [CONTRIBUTION.md](https://github.yandex-team.ru/maps/jsapi-v2.1/blob/2.1.76/CONTRIBUTION.md)).
2. Go http://<api_instance>/tests/manual/index.html

Example:
In cases you have Linux and starting api in docker container:
1.
```bash
    make dev.container
    # inside the container
    make deps
    make dev
```
2. Go http://localhost:8888/tests/manual/index.html.