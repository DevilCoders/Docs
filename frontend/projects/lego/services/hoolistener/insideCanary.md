# /canary
## Как подключить /canary в свой репозиторий?
Подробная инструкция с примерами [здесь](./CANARY.md)
## Как работает /canary

На каждый комментарий, оставленный к PR в github в репозитории `islands`,  отправляется POST-запрос на `/comment`.

Если был создан комментарий `/canary`, с помощью пакета [`@yandex-lego/gh-gap`](../../packages/gap/README.md) на основании путей к измененным файлам определяется начальный список пакетов, для которых необходимо выпустить `canary`-версии.

Если такие пакеты есть, с помощью `@yandex-int/sandboxer` создается `trendbox`-задача, в которой с большей точностью определяется список измененных пакетов, а также новые версии измененных пакетов на основе `commit-messages` (утилита [`@yandex-int/iver`](../../packages/iver/README.md)).

Далее, в соответствии со списком сервисов, утилита [`@yandex-lego/hedwig`](../../packages/hedwig/README.md) публикует `canary`-версии пакетов и открывает PR с `canary`-версией в репозитории, где в `package.json` есть соответствующие зависимости.

Список открытых PR или сообщение об ошибке `hoolistener` публикует в том же PR, откуда получил `/canary`.