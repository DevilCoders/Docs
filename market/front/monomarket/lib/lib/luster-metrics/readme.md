## Luster-metrics

Расширение для luster, позволяющее собирать метрики с приложения.


## Пример использования

```
...
    extensions: {
        ...
        '@yandex-market/luster-metrics': {
            socket: process.env.LUSTER_METRICS_SOCK, // путь до unix сокета
            workers: 2, // число воркеров приложения
        },
    },
...
```