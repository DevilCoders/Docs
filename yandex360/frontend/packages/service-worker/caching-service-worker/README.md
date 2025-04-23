[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/service-worker/caching-service-worker&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/service-worker/caching-service-worker)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/service-worker/caching-service-worker&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/service-worker/caching-service-worker)

## Caching ServiceWorker
Обертка над [Google Workbox](https://developers.google.com/web/tools/workbox).
<br>
Универсальный модуль для запуска кеширующего воркера.
<br>

### Подключение
Подключается с CDN с помощью importScript.

```js
importScript('https://yastatic.net/ps/caching-service-worker/caching-service-worker-<contenthash>.js');
```

Текущий хеш можно узнать в `/artifacts/caching-service-worker.manifest.json`

### Настройка
Ожидает в глобальном пространстве воркера два объекта настроек:
- `self.RpcConfig` с командами для [channel-rpc](/packages/channel-rpc)
```js
self.RpcConfig = {
    upstreamResolver: () => {},
    commands: {
        someCommandName: () => { /* some command handler */ }
    }
};
```

- `self.CacheServiceWorkerConfig` с параметрами кеширования
```js
self.CacheServiceWorkerConfig = {
    projectName: 'ServiceWorker',
    projectVersion: '0.0.0',
    storeConfig: {
        prefix: '',
        suffix: ''
    },
    precache: [
        { url, revision }
    ],
    caches: {
        // Пока поддержаны настройки только для этой сратегии.
        cacheFirst: [
            { name, match, maxAgeDays, maxEntries }
        ]
    }
};
```

### Роутер
Для проектов, использующих Даффман в качестве сервера, в пакете есть генератор роутера.
<br>
Роутер проводит полную настройку воркера и меет кучу виртуальных методов, которые стоит переопределить.
```js
const defineRoute = require('@ps-int/caching-service-worker/duffman/route');

const BaseRoute = require('./route');
const BaseCore = require('./core');

const CachingServiceWorkerBase = defineRoute(BaseRoute, BaseCore);

class CachingServiceWorker extends CachingServiceWorkerBase {

  getPrecache() {
    return [
        { url: 'some-file.<revision>.js', revision: null }
    ];
  }

  getStoreConfig() {
    return {
      prefix: 'project-csw',
      suffix: ''
    };
  }

  getCachesConfig() {
    return {
        cacheFirst: [ {
            name: 'images',
            match: '\\.(?:png|gif|jpg|jpeg|svg)$',
            maxAgeDays: 30,
            maxEntries: 60
        } ]
    };
  }
}

module.exports = new CachingServiceWorker().createRouteHandler();

```
