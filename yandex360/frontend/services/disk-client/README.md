# UFO
Верстка Яндекс.Диска
[ABC](https://abc.yandex-team.ru/services/disk-frontend/), [Startrek](https://st.yandex-team.ru/CHEMODAN/)

Репозиторий делится на несколько бандлов: `www`, `static`, `client`

## Структура репозитория

`app,scripts` — серверная часть приложения

`components`- клиентская часть приложения

## Домены и пути
Отдаётся с доменов `disk.yandex.${TLD}`.

Обрабатывает запросы:
- `/client/search` — поиск по файлам
- `/client/journal` — история
- `/client/recent` — последние файлы
- `/client/mail` — почтовые вложения
- `/client/disk/*` — файловый манагер, внутренние папки
- `/client/photo/*` — фотосрез
- `/client/shared` — расшаренные папки
- `/client/published` — публичные ссылки
- `/client/trash` — корзина
- `/client/albums/*` — альбомы

## Как работают приложения в Deploy
Приложения Диска работают в Deploy в следующих проектах:
- веб-клиент - [disk_web_client](https://deploy.yandex-team.ru/projects/disk_web_client)
- паблик - [disk_web_public](https://deploy.yandex-team.ru/projects/disk_web_public)
- заметки - [disk_web_notes](https://deploy.yandex-team.ru/projects/disk_web_notes)
- незалогиновая морда - [disk_web_auth](https://deploy.yandex-team.ru/projects/disk_web_auth)
- редактор - [disk_web_editor](https://deploy.yandex-team.ru/projects/disk_web_editor)
- промки - [disk_web_promo](https://deploy.yandex-team.ru/projects/disk_web_promo)
- почтовый виджет - [disk_web_widget](https://deploy.yandex-team.ru/projects/disk_web_widget)

В каждый контейнер приезжает:
- базовый докер-образ
- слой с приложением
- статические ресурсы - геобаза, файлы секретов и пр.

Описание сборки слоя с приложением см. в разделе Релиз папки конкретного приложения.
Базовый докер-образ собирается вручную из репозитория со всеми образами Диска в Аркадии [disk/admin/docker/disk/clusters](https://a.yandex-team.ru/arc_vcs/disk/admin/docker/disk/clusters).
Сам образ собирается автоматически при пуше в этот репозиторий.


## Сборка

Клиентские бандлы клиента, паблика и заметок собираются вебпаком. Сборка понимает следующие переменные окружения:
- `LANGS` - список языков через запятую для которых нужно собрать бандлы.  Для каждого языка собирается отдельный бандл, сборка для одного языка работает быстрее чем для всех четырёх. По умолчанию собираются все 4 языка.
- `USE_BUNDLE_ANALYZER` - подключить плагин [BundleAnalyzerPlugin](https://www.npmjs.com/package/webpack-bundle-analyzer). html-отчёт кладётся рядом с остальной статикой. По умолчанию плагин не подключен.
- `USE_SOURCE_MAP` - сгенерировать source maps. По умолчанию не генерируются.
- `NODE_ENV` - если передан `production` то будут применены оптимизации (UglifyJS, ModuleConcatinationPlugin...). Также к именам файлов js и css будут добавлены хэши, а у остальной статики имя файла будет заменено на хэш. Вся статика будет лежать плоским списком в одной папке.

Для Production-сборки смотри следующий раздел [Сборка релиза](#sborka-reliza)


## Сборка релиза

Для сборки достаточно выполнить команду
```
npm run package {VERSION} {RELEASE_TICKET}

# например
npm run package 160.0.0 CHEMODAN-123
```
Версию можно посмотреть в package.json соответствующей директории. Для нового релиза поднимаем мажорную версию.
Для обновления пакета на текущем релизе поднимаем минорную версию.

После запуска команды задачу на сборку можно найти в интерфейсе [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=release") (в поле `Select branch` указать `releases/psfront/disk-client/v<версия>`).
После успешного завершения в ресурсах задачи будет собранный пакет.

### Релиз в stable окружение
См. описание на [wiki](https://wiki.yandex-team.ru/disk/frontend/release-process/#vykatka)
Приложение живёт в Deploy в проекте [disk_web_client](https://deploy.yandex-team.ru/projects/disk_web_client)


## Разработка

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../../tools/qyp#инструкция)).

#### Запуск проекта

1. Перейти в папку сервиса
```shell script
cd ~/arcadia/yandex360/frontend/services/disk-client
```

2. Подготовить окружение (установить зависимости и выкачать секреты)
```shell script
npm run prepare-dev
```

3. Запустить проект (сервер + клиент)
```shell script
npm start
```

Для удобства можно запустить сервер и клиент в разных вкладках
```shell script
#клиент
npm run start:client

#сервер
npm run start:server
```

4. Адрес стенда выведется после запуска.
Но также можно узнать адрес отдельной командой
```shell script
npm run url
```

Ссылка в браузере зависит от названия виртуальной машины и датацентра. Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.disk-dev.dsd.yandex.ru/`, если в другом дц — `https://<dc>-<vm_name>-arc.disk-dev.dsd.yandex.ru/`, где `<dc>` — название датацентра (iva|man|myt|sas|vla), `<vm_name>` - название виртуальной машины в QYP.

Инструменты, используемые для сборки:
- GNU Make (сборка, тесты, запуск http-сервера)
- webpack (сборка клиентских бандлов)
- Grunt (сборка серверных шаблонов)

Команда `npm run start:client` (под капотом `make server-client`) запускает разовую grunt-сборку серверных шаблонов и
далее вебпак-сборку клиентских бандлов в watch режиме.
Общие для клиента и паблика моменты про сборку вебпаком можно почитать в [корневом README](https://github.yandex-team.ru/UFO/disk/blob/master/README.md#Сборка)
Пример запуска с различными переменными окружения: `LANGS=ru USE_BUNDLE_ANALYZER=1 NODE_ENV=production make server-client` - соберётся только ru бандл в прод режиме, построится отчёт от BundleAnalyzerPlugin
Особенности сборки:
- Инкрементальная сборка для yate не работает. Если были внесены изменения в yate-шаблоны (как серверные, так и клиентские) - нужно перезапустить сборку.
- Для локализации используются d2-build-tools и их адаптация к сборке вебпаком в виде [плагина](https://github.yandex-team.ru/UFO/disk/tree/master/www/tools/webpack/i18n-plugin.js)

Сервер также можно запустить в фоновом режиме через `make start`. Для старта/остановки/перезапуска HTTP-сервера нужно
выполнить `make start`/`make stop`/`make restart`.

В результате сборки создадутся ассеты и шаблоны, и положатся в папки `/static/{bundle}` и `/templates/{bundle}`. Более подробное описание будет выполнено в [отдельной задаче](https://st.yandex-team.ru/CHEMODAN-38708).

## Обновление локалей

`make tanker`

Про передачу релиза в ассесоров можно почитать [тут](https://wiki.yandex-team.ru/users/irmashirma/Peredacha-zadachi-asessoram/).

## Где живет и как работает
Серверная часть работает на [descript](https://github.com/pasaran/descript).

Клиентская — на [redux](http://redux.js.org/), [react](https://reactjs.org). Также есть legacy технологии [noscript](https://github.com/yandex-ui/noscript), [noscript-react](https://github.com/yandex-ui/noscript-react), [yate](https://github.com/pasaran/yate).

Список production машин можно узнать в qloud, либо можно воспользоваться утилитой [executer](https://wiki.yandex-team.ru/executer/), например, так:
```bash
ssh temp01h.disk.yandex.net # заходим на одну из машинок группы https://c.yandex-team.ru/groups/disk-temp
executer --user=${username} # консоль подвиснет на какое-то время. username - логин на стаффе.
describe %disk_front        # disk_all — группа фронтовых хостов диска https://c.yandex-team.ru/groups/disk_front
```

`--user` - не обязательный ключ, можно позже воспользоваться командой user
Как поставить executer локально на мак можно почитать [тут]()https://wiki.yandex-team.ru/executer/#macosx/cygwin

## Логи
[Описаны в табличке](https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-front-client-deploy)
Быстрые логи прода смотреть с помощью [ClickHouse](https://wiki.yandex-team.ru/disk/admin/disk_clickhouse/)

Приложение отправляет логи в tskv-формате в syslog и они пишутся в папку `/var/log/duffman/`. Содержимое файлов:
  * `ydisk-front-node.tskv` — бывший `yandex-ufo-www-tskv.log`, логи descript-а;
  * `duffman-access.tskv` — логи моделей и окончания запроса; А так же чего угодно через `core.console.*`;
  * `duffman-http.tskv` — логи исходящих http-запросов;
  * `duffman-master.tskv` — запуск приложения, падения воркеров, непойманные ошибки и т.п. **Не отгружается в YT**.

При запуске приложения командой `make start` stdout и stderr пишутся в файл `yandex-ufo-www.raw.log`.

На production-машинах логи так же хранятся в папке `/var/log/duffman` и отгружаются в YT.
  * https://yt.yandex-team.ru/hahn/navigation?path=//logs/ydisk-front-node-log
  * https://yt.yandex-team.ru/hahn/navigation?path=//logs/ydisk-duffman-access-log
  * https://yt.yandex-team.ru/hahn/navigation?path=//logs/ydisk-duffman-http-log

## Error booster
Клиентские ошибки логируются в `error booster`
[EB веб-клиента Диска](https://error.yandex-team.ru/projects/disk)

## Мониторинги
[Мониторинг приложения в golovan](https://yasm.yandex-team.ru/template/panel/disk-front-client/)

[Скорость отрисовки интерфейса в RUM](https://rum.yandex-team.ru/projects/disk)

[Покрытие в sonar](https://sonar.qatools.yandex-team.ru/overview?id=44120)

## Как настроить ассессорскую прокси
См. в [отдельной доке](./docs/assessors.md)

## Как попадать в эксперименты
См. в [отдельной доке](./docs/experiments.md)

## Запуск Hermione-тестов
См. в [отдельной доке](./docs/hermione.md)

## Скорость

Измерить показатели скорости на своём стенде можно следующим образом
1. `npm install -g lighthouse`
2. `chrome-debug` запускаем chrome, логинимся в нём на нужном хосте и копируем порт
3. `lighthouse --view "https://disk.yandex.com/?skip-promo=1" --port $PORT --throttling.cpuSlowdownMultiplier=6 --throttling.throughputKbps=300` в отдельной вкладке запускаем тесты. Порт нужно взять из результата предыдущей команды. Хост также прописать тот, на котором хочется протестировать.


## Misc
Пользователь с большим количеством фоток — disk.many.photos / asdfg12345
Пользователь с большим количеством "красивых" фоток - disk.pretty.photos / pretty-pretty (34.3К кластеров, 85.8К фото). Те же фото залиты в google photo пользователю iwan.klubnika@gmail.com / ivanklubnika
Пользователь с гео-альбомами в тестинге - t73s7 / qwerty12345

### Как сделать блок воспоминаний в тестинге
`curl 'http://api-stable.dst.yandex.net:8080/v1/<UID>/personality/profile/disk/cool_lenta/morda_blocks?client_id=2001055&client_name=disk-web-client-test' --data '{"photoslice_date": "2019-05-20T14:33:13.000Z", "best_resource_id": "<best_resource_id>", "resource_ids": ["<resources_id, resources_id, ...>"], "max_date": "2019-05-20T14:33:13.000Z", "min_date": "2019-05-20T10:33:13.000Z", "mtime": "2019-05-20T10:33:13.000Z", "generation_type": "default_WEEKEND", "user_timezone_id": "Europe/Moscow"}'`
`photoslice_date` - дата к которой будет отскролен фотосрез при нажатии на кнопку "все фото"
`resource_ids` - массив resource_id фотографий (можно взять из `.meta.resource_id`)
`best_resource_id` - id лучшего ресурса из массива `resource_ids` (будет выбран в качестве обложки для альбома созданного из блока воспоминаний)
`generation_type` - тип подборки (недельная/выходные/за год и ТД.) Возможные значения: `default_MONTH`, `default_ONE_DAY`, `default_WEEK`, `default_SEASON`, `year_best_YEAR`, `default_WEEKEND` (актуальные значения можно посмотреть в метрике `interface elements -> photo block -> show`)

##Как кастомизировать интерфейс для новой акции

## Описание и требования к данным описаны на wiki
https://wiki.yandex-team.ru/disk/frontend/new-promo-action/

### Чтобы организовать новую акцию нужно

1. Загрузить на yastatic картинки для новой акции
2. Завести ключ в танкере с текстом для акции
3. Сформировать json, проверить и после этого отдать его бекенду

### Как загружать картинки в s3

1. получить права на заливку в бакет disk и настроить доступ
https://github.yandex-team.ru/personal-services/frontend/tree/dev/services/disk#контейнер-для-сборки

(в `~/.aws/credentials` должны быть прописаны aws_access_key_id и aws_secret_access_key для доступа)

проверить к каким бакетам настроен доступ
`aws --endpoint-url=http://s3.mds.yandex.net s3 ls`

2. залить нужные файлы в бакет диска

про заливку можно почитить тут
https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#primery

### Как загрузить картинки для новой акции

файлы складываем в папку `/promo/{название акции}/web-disk/{discount-tooltip|onboarding|info-space-block}/`

например используя aws

`aws --endpoint-url=http://s3.mds.yandex.net s3 cp small-image.png  s3://disk/promo/february-14-2022/web-disk/info-space-block/small-image.png`

svg-ки нужно загружать вместе с gzip и br версиями (`brew install brotli` - скачать brotli)

`brotli file.svg -> file.svg.br`
`gzip file.svg -> file.svg.gz`

**Важно!** Через интерфейс заливать .svg не получится, потому что yastatic будет отдавать потом файлы с неверным
mime-type, нужно именно через консольные команды `aws`

### Как удалить картинки прошедшей акции

Пример:
`aws --endpoint-url=http://s3.mds.yandex.net s3 rm --recursive s3://disk/promo/discount-20/`


### Загружать/удалять картинки для акции можно также через интерфейс

https://yc.yandex-team.ru/folders/foo5clgjfmk87g7nukfd/storage/buckets/disk?key=promo%2F
