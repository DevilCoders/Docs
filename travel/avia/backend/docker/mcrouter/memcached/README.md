Собрать и опубликовать контейнер
--------------------------------

```
cd memcached
docker build --network=host -t=registry.yandex.net/avia/memcached:0.0.1 .
docker push registry.yandex.net/avia/memcached:0.0.1
```
