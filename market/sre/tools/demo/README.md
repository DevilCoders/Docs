# Demo
A simple program that gets market front hostname.

### Requirements
[yatool](https://wiki.yandex-team.ru/yatool/)

### Checkout
[Get ```ya``` and clone arcadia](https://wiki.yandex-team.ru/yatool/clone/)  
```
> ya clone mini-arcadia
> cd mini-arcadia
> ya make --checkout -j0 arcadia/market/sre/tools/demo
```

### Build
```
> cd arcadia/market/sre/tools/demo
> ya make --checkout ./
```

### Run tests
```
> ya make -t
```

### Run program
```
> ./demo-bin --help
usage: demo-bin [-h] [-t TIMEOUT]

Demo program gets Market's main page

optional arguments:
  -h, --help            show this help message and exit
  -t TIMEOUT, --timeout TIMEOUT
                        Request timeout
> ./demo-bin
pepelac19d.market.yandex.net

>
```