# Affiliate

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/front/apps/affiliate&vcs=arc)](https://oko.yandex-team.ru/arc/market/front/apps/affiliate)

Проект партнёрской сети Яндекс.Маркета.

## Как развернуть

Склонируйте репозиторий и введите команду `make`.
Загрузка зависимостей и сборка проекта пройдут автоматически.

```bash
$ arc mount -m $HOME/arcadia
$ cd arcadia/market/front/apps/affiliate
$ make
```

На удалённом сервере для разрабатывания (подробнее [тут](https://wiki.yandex-team.ru/users/yatamik/affiliate-dev-deploy/))
создайте рабочую копию.

Подключитесь по `ssh` к Логрусу и выполните следующую команду:

```bash
$ make_wc -p node.affiliate -n
```

Вывод скрипта будет содержать лог развёртывания. После завершения работы в консоли выведется информация о новой рабочей копии:

```
DONE: project copy is deployed to /var/lib/yandex/market-affiliate-node-dev/[username]
DONE: created symlink node.affiliate_[username] in your home directory
work copy URL: https://[username].affiliate.node.logrus01hd.yandex.ru
```

### Удалённый сервер («Логрус»)

На удалённом сервере перейдите в директорию с рабочей копией и выполните команду:

```bash
$ make hmr-server
```

Эта команда запустит watcher и Node-приложение с [Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement/).
HMR на сервере выполняет встраивание скрипта загрузчика на страницу с относительным путём на `localhost`.

### Локально

На локальном устройстве выполните команду:

```bash
$ make hmr-client
```

Эта команда запустит `webpack-dev-server` в режиме `watch` на порту **8080** и соберёт клиентскую часть проекта.
По умолчанию Webpack собирает проект с «лёгкими» `source maps`, однако если требуются подробные,
— добавьте флаг `--smap` при запуске сборки локально:

```bash
$ npm run build:hmr:client --smap
```

### SSL-сертификат

Для использования скриптов и стилей с `localhost` на сайтах с HTTPS, во время сборки генерируется SSL-сертификат,
но без надёжного источника.
Как решение проблемы добавьте сертификат в исключения, но так как он хранится в `node_modules`, то
после удаления этой папки сгенерируется новый сертификат, который снова потребуется добавить в исключения.

Для пользователей браузеров семейства Chromium зайдите на
[`chrome://flags/#allow-insecure-localhost`](chrome://flags/#allow-insecure-localhost) и включите опцию
`Allow invalid certificates for resources loaded from localhost`.

---

Документация на [Wiki](https://wiki.yandex-team.ru/users/yatamik/affiliate-dev-deploy/).
