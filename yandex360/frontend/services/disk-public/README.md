Вёрстка публичных страниц Диска.

# Описание
Приложение, которое обрабатывает запросы к публичным страницам Яндекс.Диска. Обслуживает урлы вида
 - `disk.yandex.{tld}/[di]/<short_hash>`
 - `yadi.sk/[di]/<short_hash>` (старый формат, сейчас редиректит на `disk.yandex.{tld}/[di]/<short_hash>`)
 - `disk.yandex.{tld}/public/hash=<private_hash>`
 - `disk.yandex.{tld}/public/nda/?hash=<private_hash>`
 - ссылка с якорем

# Как собирать и выкатывать
## Сборка релиза

Для сборки достаточно выполнить команду
```
npm run package {VERSION} {RELEASE_TICKET}

# например
npm run package 69.0.0 CHEMODAN-123
```
Текущую можно посмотреть в package.json.

После запуска команды задачу на сборку можно найти в интерфейсе [Trendbox](https://trendbox.yandex-team.ru).
Для этого нужно в поле `Repository` указать `arc:yandex360/frontend` и найти в списке задачу `releases/psfront/disk-public/v<версия>`.
После успешного завершения в ресурсах задачи будет собранный пакет.

[Подробнее на wiki](https://wiki.yandex-team.ru/disk/frontend/build/)

## Выкладываем релиз на машину
Идём в Deploy (https://deploy.yandex-team.ru/projects/disk_web_public). Выбираем Stage `disk_web_public_prestable`.
Жмакаем _Edit_. Выбираем DeployUnit с нужным `prestable`-ом.
В DeployUnit-е выбираем вкладку `Disks, volumes and resources`. В разделе `Layers` у слоя `ID: app` меняем `URL` на собранный нами ресурс.

Ждём выкатки, следить за которой можно в интерфейсе Deploy, и проверяем версию на https://disk<номер_престейбла>.dsp.yandex.ru/version/

# Как начать разработку

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../../tools/qyp#инструкция)).

#### Запуск проекта

1. Перейти в папку сервиса
```shell script
cd ~/arcadia/yandex360/frontend/services/disk-public
```

2. Подготовить окружение (установить зависимости и выкачать секреты)
```shell script
npm run prepare-dev
```

3. В одном терминале запустить сборку
```shell script
npm run watch-web-ru
```

4. В другом терминале стартовать сервер
```shell script
npm start
```

5. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной машины и датацентра.
Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.disk-dev.dsd.yandex.ru/`,
если в другом дц — `https://<dc>-<vm_name>-arc.disk-dev.dsd.yandex.ru/`,
где `<dc>` — название датацентра (iva|man|myt|sas|vla),
`<vm_name>` - название виртуальной машины в QYP.

# Как запустить тесты
`npm run test` - юнит тесты
`npm run test-watch` - зарустить юнит тесты в watch режиме, полезно при разработке
`npm run gemini` - запустить регрессионные тесты на gemini
`npm run gemini-update` - обновить скриншоты gemini

# Где запущено приложение
Приложение запущено в Deploy в проекте [disk_web_public](https://deploy.yandex-team.ru/projects/disk_web_public).

# Логи
[Описаны в табличке](https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-front-public-deploy)
[Схема логов приложения](https://a.yandex-team.ru/arc_vcs/yandex360/frontend/packages/ufo-server-side-commons/tskv/default.schema.json)
Быстрые логи прода смотреть с помощью [ClickHouse](https://wiki.yandex-team.ru/disk/admin/disk_clickhouse/)

## Error booster
Клиентские ошибки логируются в `error booster`
[EB паблика Диска](https://error.yandex-team.ru/projects/disk-public)

## Примеры запросов
[Логи за какое-то число](https://yql.yandex-team.ru/Operations/Wgv208x7duysT7yLyA9PqnBIY5i4JYbWFnS_i-NhEA4=)

[Логи, сгруппированные по ошибкам (4хх, 5хх), за какое-то число](https://yql.yandex-team.ru/Operations/Wgv03SK7Yu_D7r23-DZ-WWmm6E_ll_KGvhs7wQ4q0iA=)

[Связываем логи с машинками с access-логапи по request_id](https://yql.yandex-team.ru/Operations/WhVHsyK7Yu_D73P8QQscKF4haWd9n0jDiST6WmKKxb4=)

# Мониторинги
В [табличке на вики](https://wiki.yandex-team.ru/disk/frontend/charts/) в строке `public`

## Как настроить ассессорскую прокси
См. в [отдельной доке](../disk-client/docs/assessors.md)

## Как попадать в эксперименты
См. в [отдельной доке](../disk-client/docs/experiments.md)

## Запуск Hermione-тестов
См. в [отдельной доке](../disk-client/docs/hermione.md)
