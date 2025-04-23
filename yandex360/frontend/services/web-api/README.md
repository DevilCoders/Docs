[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/web-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/web-api)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/web-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/web-api)


# Mail WebAPI

  - сервис веб-ручек `https://mail.yandex.tld/web-api/*`.
  - npm-пакет `@ps-int/mail-lib` с библиотекой методов и ручками;

## Разработка

### Quick start

```bash
cd ~/arcadia/yandex360/frontend/services/web-api
npm run prepare-dev
npm run start dev # или testing, или corp
```


### Как добавить новый сервис в web-api

 * прописать конфиг в `internal-lib/config/services/base/options/XXX.js` и импортировать его в `internal-lib/config/services/base/options/index.js`
 * реализовать методы сервиса в `internal-lib/services/XXX/XXX.js`
 * после этого можно вызывать сервис `core.services('XXX')('/method'...)`

Для примеря можно смотреть реализацию соседних сервисов.


### Как сконфигурировать TVM для сервиса

 * прописать TVM ID сервиса в `tools/specs/tvm/*.j2` для соответствующих окружений (testing / production / corp / dev / corp-dev)
 * прописать TVM ID сервиса в `../../tools/qyp/roles/tvm/files/tvmtool/yav-deploy/templates/mailfront/web-api.json.j2`
 * сделать `make -C ../../tools/qyp tvm` из **НЕ tmux** сессии (обычный ssh)
 * перезапустить все tmux и ssh сессии чтобы подхватился новый конфиг
 * теперь можно подсовывать TVM тикеты в одну строку:
 ```javascript
 options.headers['x-ya-service-ticket'] = core.req.tvm.tickets.XXX.ticket;
 ```


### Воркфлоу

Разработка ведётся в очереди [MAILAPI](https://st.yandex-team.ru/MAILAPI)

Используется воркфлоу:

`Open` → `In Progress` → `In Review` → `Review Completed` → `Dev` → `RC` → `Closed`.

* Название пулл-реквеста должно начинаться с тикета. Рекомендуется использовать Commit message из Трекера (пример: `MAILAPI-756: Локализовать папку reply_later`).
* В пулл-реквесте должны успешно пройти все необходимые проверки.
* Для ревью используется ревьюшница Арканума ([настройки тут](https://a.yandex-team.ru/arc_vcs/yandex360/frontend/services/web-api/a.yaml)).
* Для слияния ветки в `trunk` используются инструменты Арканума (кнопка `Merge` доступна после прохождения всех необходимых проверок). Поменять статус на `dev` / закрыть тикет нужно самостоятельно в Трекере. При сборке релиза через CI статусы `Rc` → `Closed` будут проставлены автоматически.
* Дежурный по заявкам коллег собирает релиз и выкатывает в продакшн. Сборка и деплой осуществляются инструментами New CI.


### Тестирование

* [Юнит-тестирование](./test)
* [Интеграционное тестирование](./test/integration)


### Публикация `@ps-int/mail-lib`

При каждом релизе web-api автоматически публикуется соответствующая версия `@ps-int/mail-lib`, patch-версия при этом всегда `0`.

Если требуется опубликовать пакет отдельно от релиза web-api:

```
# предварительно нужно поднять patch версию
npm version patch --prefix internal-lib
npm run publish-npm
```


### Релиз web-api

Релизы web-api [запускаются в интерфейсе New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend%2Fservices%2Fweb-api&id=webapi-release). Слева можно заметить список веток (`trunk` и последние релизные ветки) со статусом текущего релиза, если есть (например, может быть подсвечен `Waiting For Manual Trigger`). Тикет в стартреке заводится автоматически.

Чтобы запустить релиз, в интерфейсе CI нужно выбрать коммит и отвести от него релизную ветку (справа в бургере), после этого перейти в ветку и нажать `Run release`. Релизная ветка отводится c автоматическим инкрементом мажорной версии. Наблюдать за релизом можно в UI. Некоторые шаги требуют ручного подтверждения (например, нужен запуск после получения результатов E2E тестов, или для деплоя canary и production окружений). Если какие-то кубики в процессе выполнения "покраснели" в результате временной ошибки (можно понять по логам), их можно перезапустить в UI.

[Пример релизного флоу](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/flow?dir=yandex360%2Ffrontend%2Fservices%2Fweb-api&id=webapi-release&version=9.7)

Чтобы докинуть фикс в релиз (фикс должен быть в транке), можно черри-пикнуть его прямо в UI кнопкой `Cherry pick` (кнопка доступна сверху справа, если находиться при этом в релизной ветке), и запустить новый флоу `Run and cancel others` (кнопка в бургере у пикнутого коммита). В результате будет запущен новый релиз с инкрементом минорной версии.

Флоу поделен на стадии (prepare / build / testing / etc), каждая стадия может начать выполняться только если в предыдущем релизе она завершилась (именно поэтому "and cancel others").



## npm-пакет `@ps-int/mail-lib`

Большая часть файлов лежит в папке `internal-lib`.

Содержит:
  - модели;
  - сервисы;
  - конфиги сервисов;
  - доменные конфиги;
  - миддлвары;
  - вспомогательные хелперы;
  - библиотеку `moe` для «деклатаривного» описания сервисов и методов.

[**Интерфейс модуля**](./internal-lib/index.js)

[**Интерфейс библиотеки moe**](./internal-lib/moe.js)

Оба интерфейса должны слиться в один.


## web-api

Веб-ручки используемые в интерфейсах Яндекс.Почты ([liza](../liza),
[quinn](../quinn), [lite](../lite)).

Все ручки находятся под единым неймспейсом `web-api` и доступны по адресу вида:
```
/web-api/${method}/${version}
```

Каждая ручка версионируется отдельно. Версии могут принимать следующий вид:
- **(1)** `{interface}N`, например `liza1`, `touch5`, `lite42`;
- **(2)** `vN`, например `v0`, `v13`, `v100500`.

Версии **(1)** символизируют к какому интерфейсу относится версия данной ручки,
в такой версии реализация специфична для указанного интерфейса. Должны
использоваться только для переноса существующих ручек из интерфейса в общий
репозиторий.

Версии **(2)** обозначают, что реализация ручки в этих версиях общая для всех
интерфейсов, то есть должна работать и поддерживаться одинаково хорошо во всех
интерфейсах Яндекс.Почты.

Таким образом, если есть ручка под названием models, и реализованы версии
`liza1` и `v0`, то эти версии должны быть доступны по следующим урлам:
- `/web-api/models/liza1`
- `/web-api/models/v0`


## Документация

Документация генерируется командой `npm run docs` и публикуется в s3-бакет `s3://psf/web-api-docs/`. Для каждой ветки создаётся отдельная папка, куда складывается документация как для `web-api`, так и для `internal-lib`.

Пример: https://psf.s3.mds.yandex.net/web-api-docs/index.html
