Нужно завести себе собственную разработческую витруалку в [QYP](https://qyp.yandex-team.ru),
разработка ведётся только оттуда по причине наличия зависимостей от сетевых правил файрвола
и грантов для системы авторизации.
Для входа на неё нужно сгенерировать и добавить на Стафф ssh-ключ ([инструкция](https://wiki.yandex-team.ru/doc-and-loc/doc/newbies/mac/ssh-authentication-keys/)).
Если у вас уже есть почтовая дев-машина, можно вести разработку прямо на ней.
Для того, чтобы всё работало корректно и с нужными доступами, нужно также состоять
[в группе ABC](https://abc.yandex-team.ru/services/maya/).

* [Настроить](../../../tools/qyp) qyp машину 
* Перейти в папку сервиса
```bash
cd arcadia/yandex360/frontend/services/maya/
```
* Запустить первоначальную настройку
```bash
npm run dev-setup
```
* Установить зависимости
```bash
npm ci
```
**n.b.** Локально на ноутбуке стоит запустить `npm ci` в корне монорепозитория `arcadia/yandex360/frontend/`,
чтобы начали работать arc-git-хуки (`pre-commit`, например, описаны в секции `husky`
в корневом проектном [package.json](../../package.json)).

* Запустить
```bash
npm start
```
Интерфейс будет доступен по адресу:
```
Паблик версия
https://<vm_name>-<folder_name>.maya-dev.calendar.yandex.ru

Корпоративная версия
https://<vm_name>-<folder_name>.maya-dev.calendar.yandex-team.ru
```
Где `vm_name` - имя машинки в QYP,
а `folder_name` - название папки в домашней директориии, куда счекаутили проект, обычно `arcadia`.

Пример
https://tavriacalendar-arcadia.maya-dev.calendar.yandex-team.ru/


### Запуск в фоне через screen

Помогает держать проект запущенным на постоянной основе (например, для поднятия стенда для фичи) и не зависеть от ssh-сессии.

```bash
screen -S <name>
npm start
```

```bash
# Создание сессии:
screen -S <name>
# где <name> - любое имя

# Посмотреть список сессий:
screen -ls

# Возврат к сессии:
screen -r <name>
```

## Возможные проблемы

- Иногда при первом запуске проекта приходится его остановить и запустить заново, иначе будет 404.

- После запуска, адрес рабочей копии в браузере отвечает 502
  1. Попробуйте перемонтировать `arc` с параметром `--allow-other`, иначе у `nginx` не будет доступа к запущенным серверам на сокетах `webpack.sock/node.sock` и адрес рабочей копии будет отвечать всегда `502`;

        ```bash
        arc mount --allow-other
        ```

  2. Убедитесь, что правильно указали адрес рабочей копии;

  3. Проверьте, что запущен `nginx`;
        ```bash
        sudo service nginx start
        ```
  
  4. Ошибки `nginx` можно найти тут `cat /var/log/nginx/maya/error.log`.

- Для автодеплоя по sftp нужно включить предпочтение ipv6 в WebStorm (`Cmd` + `Shift` + `A` => `Edit Custom VM Options`)
```
-Djava.net.preferIPv4Stack=false
-Djava.net.preferIPv6Addresses=true
```
