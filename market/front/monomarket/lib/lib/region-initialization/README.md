[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/region-initialization)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/region-initialization) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/region-initialization)](https://oko.yandex-team.ru/pkg/@yandex-market/region-initialization)

# region-initialization

Высокоуровневая логика определения региона для market- и touch- Node.

### user-region-async
[Репозиторий](https://github.yandex-team.ru/market/user-region-async)
Компонет для nodules-user.
Предоставляет асинхронный интерфейс и возможность инжектить инициализированный инстанс node-geobase. Для полу-синхронной работы с регионом, предусмотрен метод ensureProps.

### nodules-user
[Репозиторий](https://github.yandex-team.ru/nodules/user)  
Базовый модуль для получения информации о пользователе, его регионе, браузере и l10n-параметрах.

### node-geobase
[Репозиторий](https://github.yandex-team.ru/varankinv/node-geobase Репозиторий)  
Клиент для геобазы, реализующий механизм драйверов. Абстрагирует работу с разными имплементациями геобазы.

### geobase-remote-driver
[Репозиторий](https://github.yandex-team.ru/varankinv/geobase-remote-driver Репозиторий)  
Драйвер для node-geobase. Работает с удаленным vertis-geobase по tcp протоколу.
На данный момент, не используется

### geobase-native-driver
[Репозиторий](https://github.yandex-team.ru/varankinv/geobase-native-driver Репозиторий)  
Драйвер для node-geobase. Является враппером над нативными биндингами для nodejs.

### vertis-geobase
[Репозиторий](https://github.yandex-team.ru/vertis/vertis-geobase Репозиторий)  
[Кондуктор](https://c.yandex-team.ru/packages/yandex-vertis-geobase)  
Надстройка над geobaas-server. Запускает воркеры с помощью luster, настраивает логирование. Дает возможность задавать конфиги для разных сред окружения (dev, prod и т.д.). Устанавливается как debian-пакет.

### geobaas-server
[Репозиторий](https://github.yandex-team.ru/varankinv/geobaas-server Репозиторий)  
Локальный сервис, предоставляющий SaaS-like интерфейс к libgeobase4 по tcp.

### Биндинги (geobase4)
[Документация](https://doc.yandex-team.ru/face/libgeobase/concepts/interfaces-nodejs.xml)

### Геобаза
[Документация](https://doc.yandex-team.ru/face/libgeobase/concepts/about.xml)

## Пример использования
```javascript
var initRegion = require('region-initialization').init;

var geobaseConfig = {
    fallback: {
        timeout: 200
    },
    remote: {
        path: 'http://yay-im-cool-url.com/geobase',
        params : {}
    },
    native: {
        path: '/usr/local/bin/geobase4.bin',
        params: {}
    }
}
var logger = stout.logger || console.log
var user = new User(...) // Обертка над nodules-user

initRegion(user, geobaseConfig, logger)
        .onResolve(function (result) {
            // Нужен редирект на соответствующий tld
            if (result.redirectUrl !== null) {
                ...
            }

            Object.defineProperties(this, {
                region: {
                    enumerable: true,
                    value: result.region
                },
                tld: {
                    enumerable: true,
                    value: result.tld
                }
            });
        }, user)
        .onReject(function () {
            logger('something went wrong...')
        });
```
