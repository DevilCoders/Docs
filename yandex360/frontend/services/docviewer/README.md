Docviewer
=========

Кондукторная группа
прод `%disk_deploy_dv_front_stable`
корп `%disk_deploy_dv_front_corp_stable`

### Разработка

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../tools/qyp#инструкция)).

#### Запуск проекта

1. Подготовить dev-окружение (установить зависимости и выкачать секреты)
```shell script
cd ~/arcadia/yandex360/frontend/services/docviewer
npm run prepare-dev
```

2. Собрать клиентский и серверный бандл
```shell script
npm run watch
```

3. После успешной сборки бандлов запустить сервер в другом терминале
```shell script
npm start
```

4. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной машины и датацентра.
Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.dv-dev.dsd.yandex.ru/`,
если в другом дц — `https://<dc>-<vm_name>-arc.dv-dev.dsd.yandex.ru/`,
где `<dc>` — название датацентра (iva|man|myt|sas|vla),
`<vm_name>` - название виртуальной машины в QYP.


### Сборка релиза

Для сборки достаточно выполнить команду
```
npm run package {VERSION} {RELEASE_TICKET}

# например
npm run package 35.0.0 CHEMODAN-123
```
Текущую можно посмотреть в package.json.

После запуска команды задачу на сборку можно найти в интерфейсе [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=release") (в поле `Select branch` указать `releases/psfront/docviewer/v<версия>`).
После успешного завершения в ресурсах задачи будет собранный пакет.

[Подробнее на wiki](https://wiki.yandex-team.ru/disk/frontend/build/)

#### Логи

https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-dv-front-deploy

### Выкатка

Проект в Deploy: https://deploy.yandex-team.ru/projects/docviewer
Для выкатки простого релиза достаточно в нужном окружении зайти в `Deploy unit settings` и на вкладке
`Disks, volumes and resources` поменять `URL` слоя (`Layer`) с `ID: app`.
При выкатке в прод сначала катим `docviewer-standalone` и только потом, если всё в порядке, `docviewer`.
Также не забываем выкатить `corp`-окружение
