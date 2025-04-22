# Редактор офисных документов
Включает в себя обёртку для MS Office и OnlyOffice (в зависимости от типа и настроек пользователя)

## Как начать разработку

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../tools/qyp#инструкция)).

## Запуск проекта

1. Подготовить dev-окружение (установить зависимости и выкачать секреты)
```shell script
cd ~/arcadia/yandex360/frontend/services/editor
npm run prepare-dev
```

2. Собрать клиентский бандл
```shell script
npm run build:watch
```

3. После успешной сборки бандлов запустить сервер в другом терминале
```shell script
npm start
```

4. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной машины и датацентра.
Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.disk-dev.dsd.yandex.ru/`,
если в другом дц — `https://<dc>-<vm_name>-arc.disk-dev.dsd.yandex.ru/`,
где `<dc>` — название датацентра (iva|man|myt|sas|vla),
`<vm_name>` - название виртуальной машины в QYP.

Доступно редактирование только production документов. Редактор не работает в testing-окружении.

## Логи
[в общей табличке](https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-front-editor-deploy)

 ## Как собрать и опубликовать ресурс и статику
 Выполнить локально:
 ```
 npm run package {VERSION} {RELEASE_TICKET}

 пример:
 npm run package 1.2.3 CHEMODAN-123
 ```
 Команда запушит тег, по которому Trendbox соберет и опубликует ресурс и статику с новой версией
