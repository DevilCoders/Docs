Все наши веб-приложения (Портал, Лаборатория, разные специальные проекты) разрабатываются на основе стека из:

- React для описания компонентов
- Webpack для сборки приложения
- Babel для компиляции диалектов в javascript, поддерживаемый браузером
- NPM для управления зависимостями

Для разработки используется следующие команды:

- `npm i` для установки зависимостей. Нужно выполнить в самом начале разработки и любом обновлении зависимостей (файла `package.json`).
- `npm run start` для запуска в режиме разработки. При успешной компиляции приложение будет работать на `localhost:[port]`. В Портале порт 9090, в Лаборатории 9080. Любое обновление кода должно приводить к перезагрузке страницы, открытой в браузере.
- `npm run build` для сборки приложения. Результат сборки оказывается в папке `build`.


Использование локальных доменов для разработки
==============================================

Иногда CORS не дает протестировать взаимодействие полноценно. В таком случае можно "обмануть" браузер с помощью `/etc/hosts` и локального nginx. Для этого нужно:

1. Получить сертификат для локальной разработки. Для Лаборатории [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/web/lab/local-lab.crypta.yandex-team.ru.pem), для Портала [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/crypta/web/portal/local.crypta.yandex-team.ru.pem).
2. Установить и настроить nginx локально. В конфигурации (`sites-enabled/default` или `nginx.conf` в зависимости от сборки) нужно добавить запись вида:
```
    server {
        listen  [::]:443 ssl;
        server_name local-lab.crypta.yandex-team.ru;

        location / {
            proxy_pass http://127.0.0.1:9090;
        }

        ssl_certificate      /path/to/arcadia/crypta/web/lab/local-lab.crypta.yandex-team.ru.pem;
        ssl_certificate_key  /path/to/arcadia/crypta/web/lab/local-lab.crypta.yandex-team.ru.pem;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;
    }
```
Для других компонентов нужно соответственно заменить `server_name`, порт в `proxy_pass`, `ssl_certificate` и `ssl_certificate_key`.
3. Добавить в `/etc/hosts` запись вида:
```
::1             local-lab.crypta.yandex-team.ru
```

## Codestyle

На данный момент для форматирования кода мы используем утилиту **prettier**.
Помимо консольной версии, существует плагин для продуктов Jetbrains.
Инструкцию по установке плагина в Intellij IDEA можно найти [на сайте Jetbrains](https://www.jetbrains.com/help/idea/prettier.html).

Задать настройки стиля для проекта можно в `packages.json` на верхнем уровне конфига. Текущие настройки:
```json
{
    ...,
    "prettier": {
        "tabWidth": 4,
        "printWidth": 120
    },
    ...
}
```

Для форматирования прямо во время редактирования кода и при сохранении нужно в настройках проекта
проставить галочки **On code reformat** и **On save**:

![prettier-settins](https://jing.yandex-team.ru/files/unretrofied/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202021-06-17%2012-58-29.png)

и применить изменения.
