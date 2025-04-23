Disk + Duffman
==============

Всё происходит в папке `www/app`

* `duffman-routes/ufo` — Массив роутов. Ссылается на папки `middleware` и `routes`;
* `routes` — обработчики роутов;
  * `controllers` — кусок дескрипта;
  * `client`, `models`, `descript-handler` — обёртки для вызова `descript`;
  * `copy` (и папка `copy/`) — обработчик роута `/copy/`;
  * `unsubscribe` — обработчик роута `/m/unsubscribe`;
* `middleware`
  * `common` — загружаются всегда;
  * `duffman` — загружаются в роутах которые обслуживаюся даффманом;
* `lib`
  * `core` — класс ядра даффмана
  * `auth` — класс хранилища авторизации
  * `models` — модели
  * `services` — сервисы

Компоненты
----------
### Обработчики роутов
Обработчик это просто Express middleware.

По смыслу соответвует jsx-файлам из папки `www/scripts`. Его задача вызвать все «глобальные» middleware, подготовить ядро, проверить авторизацию, отработать бизнес-логику и сформировать ответ.

### Ядро
Описание в [Duffman Wiki](https://github.yandex-team.ru/Daria/Duffman/wiki/%D0%A1%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D1%8F%D0%B4%D1%80%D0%B0).

Аналог контекста (`context`) в дескрипте. Содержит в себе описание моделей и сервисов, а так же дополнительные данные о текущем запросе.

### Модель
Описание в [Duffman Wiki](https://github.yandex-team.ru/Daria/Duffman/wiki/%D0%A1%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D0%B8).
```js
function publicResource(params, core) { ... }
```
Модель по смыслу такая же как и в дескрипте.

Примеры в [редакторе](https://github.yandex-team.ru/personal-services/frontend/tree/dev/services/editor/server/models).

Чаще всего достаточно тривиальна, подготавливает параметры и вызывает
`core.service('service')(method, params, options)`.

Но может вызвать несколько сервисов и/или другие методы или вообще ничего не вызывать, а возвращать какую-нибудь статичную информацию.

### Сервис
Описание в [Duffman Wiki](https://github.yandex-team.ru/Daria/Duffman/wiki/%D0%A1%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0).
```js
function mpfs(core, method, params, options) { ... }
```
Сервис соответствует бекенду (`mpfs`, `cloud` и т.п.). Очень близкий родственник дескриптового модупя.

**Настоятельно рекомендуется** ходить в бекенды только с помощью сервисов (пока в диске это далеко не так).

Примеры в [disk-server-common](https://github.yandex-team.ru/personal-services/frontend/tree/dev/packages/disk-server-common/services).

Сервис это функция которая принимает 4 аргумента:
  * `core` — ядро. В частности метод `core.got`;
  * `method` — строка, в 99% случаев это путь на беке (`/json/info`, `/api/v2/folders`), но не обязательно;
  * `params` — параметры метода. Опять же чаще все это `query`;
  * `options` — опции для `core.got()` и дополнительные опции сервиса.

Обычно просто обогощает параметры метода всякими обязательными параметрами и заголовками для бекенда и вызывает `core.got()`.
