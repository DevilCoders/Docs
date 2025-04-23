Notes
=========

## Сборка релиза

Для сборки достаточно выполнить команду
```
npm run package {VERSION} {RELEASE_TICKET}

# например
npm run package 13.0.0 CHEMODAN-123
```
Версию можно посмотреть в package.json соответствующей директории. Для нового релиза поднимаем мажорную версию.
Для обновления пакета на текущем релизе поднимаем минорную версию.

После запуска команды задачу на сборку можно найти в интерфейсе [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=release) (в поле `Select branch` указать `releases/psfront/notes/v<версия>`).
После успешного завершения в ресурсах задачи будет собранный пакет.

### Релиз в stable окружение
См. описание на [wiki](https://wiki.yandex-team.ru/disk/frontend/release-process/#vykatka)
Приложение живёт в Deploy в проекте [disk_web_notes](https://deploy.yandex-team.ru/projects/disk_web_notes)

### Разработка

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../tools/qyp#инструкция)).

#### Запуск проекта

1. Перейти в папку сервиса
```shell script
cd ~/arcadia/yandex360/frontend/services/notes
```

2. Подготовить окружение (установить зависимости и выкачать секреты)
```shell script
npm run prepare-dev
```

3. Собрать клиентский и серверный бандл
```shell script
npm run watch
```

4. После успешной сборки бандлов запустить сервер в другом терминале
```shell script
npm start
```

5. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной машины и датацентра. Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.disk-dev.dsd.yandex.ru/notes`, если в другом дц — `https://<dc>-<vm_name>-arc.dv-dev.dsd.yandex.ru/`, где `<dc>` — название датацентра `(iva|man|myt|sas|vla)`, `<vm_name>` - название виртуальной машины в QYP.

## Логи
[Описаны в табличке](https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-front-notes-deploy)
Быстрые логи прода смотреть с помощью [ClickHouse](https://wiki.yandex-team.ru/disk/admin/disk_clickhouse/)

## Error booster
Клиентские ошибки логируются в `error booster`
[EB Заметок](https://error.yandex-team.ru/projects/disk-notes)

## Как настроить ассессорскую прокси
См. в [отдельной доке](../disk-client/docs/assessors.md)

## Как попадать в эксперименты
См. в [отдельной доке](../disk-client/docs/experiments.md)

## Запуск Hermione-тестов
См. в [отдельной доке](../disk-client/docs/hermione.md)
