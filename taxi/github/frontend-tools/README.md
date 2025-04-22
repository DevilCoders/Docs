## Tools for taxi-frontend

### Conductor hooks

-   Обновляет статус задачи на "Можно тестировать" после выкладки пакета.
-   Добавляет в задачу комментарий ссылкой на демостенд.
-   Добавляет в закрытые задачи ссылки на продакшн.
-   Создаёт релизные тикеты.

**api**

[POST] /conductor/api - Ручка для вебхуков кондуктора

[GET][/conductor](https://frontend-tools.front.taxi.dev.yandex-team.ru/conductor) - Информация о настроенных проектах

**details**

https://doc.yandex-team.ru/Debian/conductor-guide/task/packages.xml#webhooks_new

### Release utils

Приложения для создания релизной задачи

[GET][/release](https://frontend-tools.front.taxi.dev.yandex-team.ru/release)

### Настройка на dev-сервере

Приложение запускается в качестве демона из `/etc/init.d/frontend-tools` и лежит в `/usr/local/www/frontend-tools`
Рекомендованный способ обновления прода из мастера: `sudo npm run upgrade` - тянет обновление кода, пересобирает всё и перезапускает
демон.

## Запуск локально в dev-режиме

1. Рекомендуется запуск на домене frontend-tools.\${your-login}.local.dev.yandex.ru
2. Создаём алиасы на 127.0.0.1 или соответствующий IP6 в `/etc/hosts`:
3. Идём в [golem](https://golem.yandex-team.ru/certs/) и генерируем себе внутренний сертификат на домен \*.\${your-login}.local.dev.yandex.ru / .kz / .com (заменить v8cult на свой логин).
4. Скачиваем .pem файл с сертификатом или забираем с коммуналки
5. Кладём .pem файл в папку проекта под именем `server.pem`
6. Запускаем командой `npm run local`, открываем на порту 8443
7. Скопировать с дев-сервера из /etc/yandex/taxi-secdist/taxi.json относящиеся к проекту ключи в локальный файл с таким же именем.
8. Запускаем командой `npm run local`
