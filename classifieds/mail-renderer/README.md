# mail-renderer
Генератор писем для вертикальных сервисов

Пакет и контейнер собираются в [Аркадии](https://a.yandex-team.ru/projects/autoru/ci/releases/timeline?dir=classifieds%2Fmail-renderer&id=autoru-app-ssr) и катятся через [Shiva](https://admin.vertis.yandex-team.ru/services/mail-renderer).

[Дашборд](https://grafana.vertis.yandex-team.ru/d/8vfPyjKiz/mail-renderer)

## Разработка
Сервис поднимается на рабочей виртуалке классическим способом:
1. Склонировать репу на виртулку
```
git@github.com:YandexClassifieds/mail-renderer.git
```
2. Установить зависимости, создать конфиг
```
make
```
Этой же командой осуществляется пересборка проекта
3. Старт проекта `npm start`

# Создание шаблона подписки
Шаблон рассылки можно сверстать 2 способами (в любом случае необходимо договариваться с backend'ом):
1. Создать новый [action](https://github.com/YandexClassifieds/mail-renderer/blob/master/app/controller/pages/autoru.js#L224), который будет учтен в настройках [YandexClassifieds/subscriptions](https://github.com/YandexClassifieds/subscriptions/blob/12e21dae74eb4f4a56067015d097d99b7566f03b/subscriptions-plugins/src/main/resources/plugins.conf)
2. Попросить пробрасывать кастомное поле в json-данные шаблона (например, в секцию [view](https://github.com/YandexClassifieds/mail-renderer/blob/master/app/resource/autoru.sub.json#L1681))

# Где смотреть
Примеры шаблонов будут доступны по ссылкам вида:

`http://mail-renderer-eljusto.eljusto-02-sas.dev.vertis.yandex.net/autoru/sub`,

где `eljusto` - ник, `autoru/sub` - подписка.
Тестовые данные для шаблонов лежат в папке `/app/resource/`.

# Cхема работы Вертикальных сервисов подписок
[Схема](https://wiki.yandex-team.ru/vertis/subscriptions2/)
