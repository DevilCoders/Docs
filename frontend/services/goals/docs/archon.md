### Команды
#### `archon dev`

Запускает окружение разработчика из вебпак-дев-сервера и бекенда на экспрессе.

Доступные параметры:
- `archon dev -с` запустить только клиентскую часть с вебпак-дев-сервером. (По умолчанию фронт ходит в бэкенд в тестинг (`https://goals.test.yandex-team.ru`))
- `archon dev -с --endpoint URL` позволяет выбрать любой backend endpoint в режиме работы только клиента
- `archon dev -s` - запуск в режиме только сервера

#### `archon build`

"Собирает" проект (в продакшен режиме, со всеми оптимизациями), без выкладки его в Docker Registry и Deploy.
Файлы складываются в папку build

Доступные параметры:
- `archon build -с` - собрать только клиентский код
- `archon build -s` - собрать только серверный код

#### `archon release`

Собирает проект и выкладывает его в Docker Registry.

Обязательные параметры:
- `archon release --type=(beta|testing|master|production)` для выбора требуемых окружений.

Некоторый аналог выполнения:
```shell script
$ archon build
$ docker build -t registry.yandex.net/tools/goals-frontend:NEW_VERSION .
$ docker push registry.yandex.net/tools/goals-frontend:NEW_VERSION
$ frontend-deploy deploy
```

- `archon release --beta` - создает бету в ПР, запускается при обновлении ПР
- `archon release --testing` - собирает релиз, запускается на обновление релизной ветки, обновляет тетсинг и препродакшен
- `archon release --production` - выкладывает релиз в продакшен, создаёт тег, закрывает релизный тикет

#### `archon hermione`

Запускает тесты Гермионы через Selenium Grid. Почитать про Гермиону можно
в консоли `npx hermione -h` или на [вики][hermione-docs].

Доступные параметры:
- `archon hermione --oauth-yav OAUTH` для передачи токена Секретницы.
  Получить токен для доступа к API Секретницы можно командой
  `yav oauth` или через [браузер][vault-oauth].
  Также токен может быть задан в файле `.env`:
  ```
  OAUTH_TOKEN_YAV=AQAD-MOI_PREKRASNYI_TOKEN_123
  ```
- `archon hermione --endpoint URL` позволяет выбрать любой backend endpoint.
  По умолчанию стоит бэкенд тестинга
  (`https://goals.test.tools.yandex-team.ru`).
- `archon hermione --clement-mode create` позволяет выбрать, как clement будет работать с дампами. Возможные варианты: `create`, `read`, `write`, по умолчанию `read`
- `archon hermione --local-port PORT` указывает на каком порту поднять сервер.
  По умолчанию стоит 9001, чтобы не конфликтовать с `archon watch`.
- `archon hermione --tunnel-port PORT` указывает удаленный порт Туннелера.
  По умолчанию стоит 53334, чтобы не конфликтовать с `archon watch`.

#### `archon get-ssh-key`

Получает SSH ключ робота robot-goals-tests. Нужно для Trendbox.
Пользоваться этим не надо. Если для чего-то требуется SSH ключ, то
должен быть использован твой персональный SSH ключ, залитый на Стафф.

#### `archon remove-stands`

Удаляет неиспользуемые стенды для pr в Deploy. Работает через пакет [https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend.ci.deploy](`@yandex-int/frontend.ci.deploy`)

Доступные параметры:
- `archon remove-stands --oauth-yav OAUTH` для передачи токена Секретницы.
  Получить токен для доступа к API Секретницы можно командой
  `yav oauth` или через [браузер][vault-oauth].
  Также токен может быть задан в файле `.env`:
  ```
  OAUTH_TOKEN_YAV=AQAD-MOI_PREKRASNYI_TOKEN_123
  ```

#### `archon gen-cert`

Обновляет/генерирует ssl сертификат для локальной разработки. Выполняется автоматически при запуске режима разарботки
