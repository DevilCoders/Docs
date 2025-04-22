# Demo
A simple HTTP service.

### Requirements
[yatool](https://wiki.yandex-team.ru/yatool/)

### Checkout
[Get ```ya``` and clone arcadia](https://wiki.yandex-team.ru/yatool/clone/)  

### Build
```
> cd arcadia/market/sre/services/yasm_unistat
> ya make --checkout ./
```

### Run tests
```
> ya make -t
```

### Run program
```
> ./demo-bin --help
usage: demo-bin [-h] [-p PORT] [-H HOST] [--mсhost MEMCACHED_HOST] [--mсport MEMCACHED_PORT] [--log-file LOGFILE]

Demo http service for memcached stats

optional arguments:
  -h, --help            show this help message and exit
  -p PORT, --port PORT  Port to listen
  -H HOST, --host HOST  Address to bind
  --mсhost               Host with memcached running
  --mсport               Port memcached listening
  --log-file LOGFILE    Log file
>
```