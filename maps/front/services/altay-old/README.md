# Алтай

## [![oko health](https://badger.yandex-team.ru/oko/repo/altay/altay-www/health.svg)](https://oko.yandex-team.ru/repo/altay/altay-www)


## Окружения
* Продакшен: [UI](https://altay.yandex-team.ru/), [Y.Deploy](https://deploy.yandex-team.ru/stages/altay-www-production)
* Престейбл [UI](https://altay-www-prestable.yandex-team.ru), [Y.Deploy](https://deploy.yandex-team.ru/stages/altay-www-prestable)
* Тестинг: [UI](https://altay.test.yandex-team.ru/), [Y.Deploy](hhttps://deploy.yandex-team.ru/stages/altay-www-testing)

## Алерты
* 5xx ошибки – https://yasm.yandex-team.ru/alert/altay-5xx-errors

## Разное
* [Метрика](https://metrika.yandex.ru/dashboard?id=39101280)
* [Гайд по цветам](guide_v.1.png)

## Доступы
1. Добавить пользователя в проект в танкере - https://idm.yandex-team.ru/. Запросить роль -> Система "Танкер" -> Тип "Проект" -> "Алтай" -> Тип "Общие для проекта" -> "Разработчик проекта".
2. Тестовый Управлятор - https://idm.yandex-team.ru/. Запросить роль -> Система "Altay (testing)". Нужно выбрать вот эти поля: `read_and_write`, `cc_advanced`, `telephony_read`.
3. Продакшеновый Управлятор - https://idm.yandex-team.ru/. Такие же шаги как в п.2.
4. Если не работают тесты - запросить доступ к гриду https://wiki.yandex-team.ru/search-interfaces/infra/infratest/duty/Tunneler/#vydachadostupov. Если не спасло – писать на infraduty@

## Локальная разработка
Рекомендуемые версии Node.js – ```v12.20.1``` и npm – ```v6.14.10```
Выполняем `nvm install` в директории проекта, чтобы выбрать версию ноды. Или включаем нужную версию по умолчанию:
```bash
$ nvm alias default 12.20.1
```

### Шаги локального запуска:
* Монтируем Аркадию https://docs.yandex-team.ru/devtools/intro/quick-start-guide
* Код проекта расположен по адресу `$(arc root)/maps/front/services/altay-old`
* Заходим в проект и устанавливаем зависимости `npm ci`
---------------
#### 1. Добавляем конфиг пользователя
Для использования локальных конфигов, необходимо создать файл `/etc/yandex/environment.type` со строкой `local`.

Чтобы не коммитить `uid` в репозиторий, локальный конфиг будет пытаться подключить неверсионируемый файл `configs/local/local.js`, из которого можно экспортировать `uid` и, при необходимости, любые другие приватные данные:
```js
module.exports = {
    uid: 100500,
    login: 'gela-d',
    tvm: {
        serverUrl: 'http://localhost:8001',
        token: 'tvmtool-development-access-token'
    }
};
```
Свой uid можно взять из урла внутренней почты (перейти на https://mail.yandex-team.ru/).

---------------
#### 2. Добавляем конфиг для получения сервисных тикетов
Положить в экспорт локальных переменных
```
##### Секрет для TVM для локальной разработки
export ALTAY_TVM_SECRET_LOCAL=<tvm-secret>
```
`<tvm-secret>` - секрет tvm-приложения altay-frontend-local для локального получения сервисных тикетов. Его нужно взять из секретницы https://nda.ya.ru/3VsjdG (доступ только у Группы разработки общих сервисов)

---------------

* Собираем проект `npm run make:enb`
* Запускаем команду `npm run dev` (получение сервисного ключа + запуск magicdev)
* Открываем в браузере `https://localhost.msup.yandex-team.ru:8082/`

Для таких файлов можно создавать собственные дополнительные уровни переопределения.

Разрабатываться удобно с помощью `magic server`.

## Разработка на стабах
Запустить `npm run start-stub`

## Локальный запуск на продакшен - данных
Внимание! Этот способ позволяет локально изменять продакшен данные, используйте с осторожностью.

1. в файл `tvmtool.conf` подставьте продакшен конфиг (не комитьте эти изменения)

```
{
    "BbEnvType": 1,
    "clients": {
        "altay": {
            "secret": "env:ALTAY_TVM_SECRET_LOCAL",
            "self_tvm_id": 2017705,
            "dsts": {
                "blackbox": { "dst_id": 223 },
                "callCenter": { "dst_id": 2015629 },
                "companyEditor": { "dst_id": 2001093 },
                "editor": { "dst_id": 2001093 },
                "feedback": { "dst_id": 2015549 },
                "reviews": { "dst_id": 2000749 },
                "search": { "dst_id": 2001093 },
                "signals": { "dst_id": 2015549 },
                "suggestMaps": { "dst_id": 2016731 },
                "geospamProcessor": { "dst_id": 2033965 }
            }
        }
    }
}
```

2. В локальный конфиг `./configs/local/local.js` добавьте секцию `backends` из конфига `./configs/production/config.js`

3. Запустите проект как обычно `npm run dev`

## Флоу
1. Перед началом работы над задачей переводим тикет в статус «В работу».
2. Разработчик создает pull request, показывает менеджеру, если нужно, переводит тикет в «На ревью».
3. После ревью задача вливается в ветку trunk.
4. Задача переводится в статус "Коммит".

## Выгрузка переводов из Танкера
Переводы выгружаются командой `tanker pull` в корне проекта и коммитятся локально при каждом релизе.
Выгрузка переводов не требует токен, но, если вдруг переводы перестанут скачиваться, нужно получить токен по ссылке https://nda.ya.ru/3SjQY7 и добавить его в свою переменную окружения `TANKER_OAUTH_TOKEN`.
Проект в танкере - https://tanker-beta.yandex-team.ru/project/altay

### Релиз
1. Открываем страницу https://a.yandex-team.ru/projects/maps-front-altay/ci/releases/timeline?dir=maps/front/services/altay-old&id=release и нажимаем кнопку `Run release`
1. В списке создастся новый релиз вида "Release #258", заходим в него
1. Кликаем в иконку Cтартрека, проверяем созданную релизную задачу
1. Проверяем, что в [тестинг](https://deploy.yandex-team.ru/stages/altay-www-testing) и [престейбл](https://deploy.yandex-team.ru/stages/altay-www-prestable) (внимание! в престейбле продовые данные!) выкатилась нужная версия. Примерное время раскатки новой версии - 30 минут.
1. Призываем в тикет всех исполнителей релизных задач, чтобы каждый сам протестировал свои задачи в тестинге и престейбле или пишем коллегам в рабочий чат.
1. (Опционально) При тестировании, переводим задачу в статус "Тестируется". После тестирования - в статус "Протестировано".
1. Если все хорошо, и все задачи протестированы, уточняем у менеджера момент выкатки прода. После отмашки, запускаем кубик "Deploy to production" в релизном флоу, который обновляет https://deploy.yandex-team.ru/stages/altay-www-production.
1. Дожидаемся выкатки продакшена и если все ок запускаем кубик "Закрытие релизного тикета", который закрывает все связанные с релизной задачей задачи.

### Подготовка к работе с `docker`

1. Установить [docker-machine](https://docs.docker.com/mac/step_one/)
2. Запустить `Docker Quickstart Terminal` — это по сути локальный терминал с
выставленными переменными окружения для прозрачной работы с виртуалкой, где
крутится `docker` (команда в терминале `bash --login '/Applications/Docker/Docker Quickstart Terminal.app/Contents/Resources/Scripts/start.sh'`).

### Работа с `docker`

#### Сборка контейнера
`docker build -t registry.yandex.net/altay/frontend .`
или
`npm run docker-build`
Проставление тега:
* для публичной версии (тестинг) перед сборкой делаем `npm version minor` и `npm run docker-build`
* для разработческой версии задаем кастомный префикс `user=gela-d- npm run docker-build`

#### Заливка контейнера в репо
`docker push registry.yandex.net/altay/frontend`
или
`npm run docker-push`
Если собирали тег, то `user=gela-d- npm run docker-push`

#### Теги
* Просмотр всех тегов:
  `curl -H "Authorization: OAuth <TOKEN>" -v https://registry.yandex.net/v2/altay/frontend/tags/list`

* Удаление тега:
  * https://packages.tools.yandex-team.ru/docker/altay%2Ffrontend/
  * Ручное: Нужно получить sha-сумму нового тега: `curl -H "Authorization: OAuth <TOKEN>" -H "Accept: application/vnd.docker.distribution.manifest.v2+json" 'https://registry.yandex.net/v2/altay/frontend/manifests/<TAG>' | shasum -a 256`
  * Удалить тег: `curl -H "Authorization: OAuth <TOKEN>" -H "Accept: application/vnd.docker.distribution.manifest.v2+json" 'https://registry.yandex.net/v2/altay/frontend/manifests/sha256:<SHASUM>' -X DELETE`
  * Благодаря пакету `remove-docker-tag` можно удалять теги командой `rdt **тег**`

#### Локальная отладка
##### Запуск собранного контейнера
`docker run -p 8082:80 -e PORT=80 registry.yandex.net/altay/frontend`
или
`npm run docker-run`

##### Запуск терминала в собранном контейнере:
`docker run -i -t --entrypoint /bin/bash registry.yandex.net/altay/frontend`
или
`npm run docker-shell`

## Тесты:
### Локальный запуск тестов
1. Запросить роль https://nda.ya.ru/t/tCR0D_po5FLHVH
1. Сделать экспорт в локальных переменных `export HERMIONE_OAUTH_TOKEN=<token>`, где token можно получить по ссылке https://nda.ya.ru/t/oS7IIVYz5FLKkR

### hermione
1. Запускаем в отдельной вкладке сервер со стабами `npm run start-stub`
2. В другой вкладке запускаем тесты командой `hermione gui`
3. Для отладки можно делать в тестах скриншоты командой `.saveScreenshot('111.png')`

#### Для получения моков данных:
1. Указываем в спеке вместо готового мока данных строку указывающую на источник этих данных (см. пример). При построении спеков указанный URL будет запрошен у сервера (стартует автоматически на генерацию спеков) и произведена замена исходной строки на полученные данные. Запросить можно и `json`, и `bemjson`. Для получения только части необходимых данных можно использовать параметр запроса `jspath` c [jspath](https://github.com/dfilatov/jspath#usage) к необходимой части данных, в формате `__LOADMOCK:${URL}__`. Например, тут находится блок `badges`
```js
const json = JSON.parse(
  '___LOADMOCK:/cards/89521921?bemjson=1&jspath=..content{.block==="badges"}[0]___');
```
будет заменено при сборке на
```js
const json = JSON.parse(
    '{"block":"badges","mods":{"type":"list","theme":"islands","size":"s"}...'
);
```
1. По очевидным причинам строку с параметром запроса (`__LOADMOCK:${URL}__`) разрывать/переносить нельзя :)
1. Для запроса данных можно использовать и `POST` запросы, для этого вместо простой строки - урла запроса `${URL}` в `__LOADMOCK:${URL}__` нужно указать *валидный* `JSON` с параметрами запроса (`url`, `method`, `body`). Например:
```js
const bemjson = JSON.parse(
    '___LOADMOCK:{"body":{"id":123},"url":"/api/blacklist-modal/?bemjson&jspath=..{.block==\"blacklist-edit\"%26%26.elem==\"content\"}[0]"}___'
);
```
1. Если `body` указан, то по умолчанию `method: 'POST', headers: { content-type: application/json }`
1. Кавычки в `jspath` приходится экранировать
