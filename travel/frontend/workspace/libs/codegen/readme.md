# Кодогенерация и утилиты

## Помощь в разработке

### Локальный домен

Патчит `/etc/hosts` и запускает контейнер с прокси-nginx`ом, позволяющим работать с localhost через https://localhost.msup.yandex.ru
или [любой другой доступный хост](./templates/dev/local-domain/domains)

#### Требования

-   docker
-   docker-compose

#### Использование

-   Запускайте корне проекта
-   `sudo` обязателен из-за модификации `/etc/hosts`

```shell
# Выбираете домен и порт вашего приложения
sudo yarn g dev local-domain
```

```shell
# Ручное указание всех аргументов без интерактивности
sudo yarn g dev local-domain --silent --domain localhost.msup.yandex.ru --port 3000
```

### <a name="local-tvm"></a>Локальный TVM

> **TODO Добавить выбор [окружения BlackBox](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#okruzhenijablackbox)**

Запускает локальный [TVM демон](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon).
Доступные конфигурации лежат в [templates/dev/local-tvm/templates](./templates/dev/local-tvm/templates),
при необходимости просто модифицируйте и перезапускайте.
Если не хотите менять существующие шаблоны, - можете создать `tvm.local.json`

#### Требования

-   Наличие TVM приложения (нужен его ID)
-   Наличие TVM токена (берется из [Секретницы Yav](https://yav.yandex-team.ru))
    -   [Пример](https://yav.yandex-team.ru/secret/sec-01g167q9x5n929qyj0m3tzvb0b/explore/versions)
-   При необходимости (если это новое приложение) - создайте шаблон в [templates/dev/local-tvm/templates](./templates/dev/local-tvm/templates)

#### Использование

-   Запускайте корне проекта
-   После первого запуска сохраняет выбранные настройки, что упрощает перезапуск

```shell
# Выбираете шаблон, подтверждаете свойства шаблона, вводите секрет
yarn g dev local-tvm
```

```shell
# --silent пропускает предзаполненные аргументы
# При первом запуске вы выбираете шаблон и вводите секрет
# При повторном запуске ничего не запрашивается (аргументы подтянутся с последнего запуска)
yarn g dev local-tvm --silent
```

```shell
# Ручное указание всех аргументов без интерактивности
yarn g dev local-tvm --silent --template tvm.bizdev-admin.json --secret XyzIfo1_ba2baz
```
