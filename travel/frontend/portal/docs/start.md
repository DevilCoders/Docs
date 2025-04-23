# Запуск проекта

<!-- toc -->

-   [Клонирование и запуск проекта](#%D0%BA%D0%BB%D0%BE%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B8-%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)
    -   [Настройка nginx](#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-nginx)
    -   [Настройка TVM](#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-tvm)
    -   [Запуск](#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA)
    -   [Сборка конкретного проекта](#%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BA%D0%BE%D0%BD%D0%BA%D1%80%D0%B5%D1%82%D0%BD%D0%BE%D0%B3%D0%BE-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)
-   [Доставка кода](#%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B0-%D0%BA%D0%BE%D0%B4%D0%B0)

<!-- tocstop -->

Для начала нужно создать виртуальную машину в QYP https://qyp.yandex-team.ru. Сделать это можно по этому гайду https://ui.yandex-team.ru/dev-server.
После создания тачки в QYP есть лаг, когда ты не можешь зайти на нее по ssh. Необходимо просто подождать какое-то время.
Выполняем все шаги из этой документации. Но конфиг nginx и TVM устанавливаем по документации ниже.

## Клонирование и запуск проекта

В яндексе используется своя VCS под названием ARC

1. Для начала работы нужно установить её по [инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide) (также рекомендуется добавить расщирение в своё IDE, arc хоть и похож на git, но на старте расширение может значительно выручать)
2. Далее нужно перейти в директорию проекта в монорепозитории `arcadia/travel/frontend/portal` и произвести начальную настройку

```
$ cd ~/arcadia/travel/frontend
$ cp .env.development.example .env.development
$ npm run dependency:dev
```

### Настройка nginx

Создаем конфиг по шаблону:

```bash
sudo USER=<user> node ./scripts/createNginxDevConfig.js init
```

1. По умолчанию конфиг будет лежать в папке `/home/<USER>/nginx` и линковаться в `/etc/nginx/sites-enabled`
2. По умолчанию сертификаты будут браться из `/crt`
3. По умолчанию логи будут писаться в `/home/<USER>/logs/ya-travel`, папка с логами будет создана автоматически.
4. Задать пользователя можно через переменную окружения USER, она также используется в формировании путей по умолчанию.

Перезапускаем nginx:

```bash
sudo service nginx reload
```

### Настройка TVM

Есть [автоматизированный способ](../tools/tvm/README.md) настройки tvm с помощью bash скриптов.

Конфиг TVM `/etc/tvmtool/tvmtool.conf`: шаблон в `tools/tvm/tvm.blank.json`.

Значение поля `secret` берем из секретницы https://yav.yandex-team.ru - `tvm.secret.2002416` (поле client_secret).

Редактируем файл `/var/lib/tvmtool/local.auth`

```
$ sudo vim /var/lib/tvmtool/local.auth
```

Заменяем содержимое на:

```
41111111111111111111111111111111
```

Перезагружаем TVM

```
$ sudo service yandex-passport-tvmtool restart
```

Полезно настроить автостарт

```
$ sudo systemctl enable yandex-passport-tvmtool
```

### Запуск

```
$ npm run dev
```

_Для того чтобы работа дев-сервера не зависела от ssh подключения можно
использовать [tmux](tmux.md)._

### Сборка конкретного проекта

Если работа идет над конкретным проектом, то для ускорения сборки можно указать переменную окружения:

```
DEVELOPMENT_BUILD_PROJECTS=hotels
```

Все возможные варианты задания данной переменной окружения можно посмотреть в `.env.development.example`.

## Доставка кода

Кто-то пересылает свой код средствами IDE, здесь описан альтернативный способ с помощью rsync. Подразумевается, что локально уже установлен rsync, на UNIX-based ОС, как правило, он уже установлен. Для windows потребуется установить порт bash'a, а потом сам rsync. После этого:

1. Создать в корне проекта файл `.rsyncpath` (Он уже добавлен `.gitignore`).
2. В файл положить такую строку `<user>@<user>.ui.yandex.ru:<path-to-project>`.
   Пример: `nskulikov@nskulikov.ui.yandex.ru:/home/nskulikov/ya-travel/`
3. Локально запустить команду `npm run build:prerequisites`, так как переводы синхронизируются.
4. Локально запустить команду `npm run watch`.
