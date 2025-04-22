# Страница для незалогиновых пользователей (Auth)

Это приложение принимает трафик на корень (`/`) домена `disk.yandex.{tld}`.
Неавторизованным показывает красивую морду с описанием сервиса и кнопкой "Войти".
Авторизованных редиректит в [веб-клиент Диска](../disk/www) на путь `/client`

Живёт в Deploy в проекте [disk_web_auth](https://deploy.yandex-team.ru/projects/disk_web_auth)

## Разработка

Разработка ведется в [QYP](https://qyp.yandex-team.ru) ([Инструкция по заведению виртуалки](../../tools/qyp#инструкция)).

### Запуск проекта

1. Подготовить разработческое окружение (установка зависимостей + секреты)
```shell script
cd ~/arcadia/yandex360/frontend/services/disk-auth
npm run prepare-dev
`````

2. Запуск проекта
```shell script
npm start
`````

Если предпочитаете разделять окна для запусков сервера и клиента, можно выполнить
```shell script
# Запуск сервера в одном окне
npm run start:server

# Запуск клиента в другом окне
npm run start:client
`````

3. Для получения ссылки в браузере нужно выполнить `npm run url`. Ссылка в браузере зависит от названия виртуальной
машины и датацентра. Если машина находится в сасово, то адрес будет `https://<vm_name>-arc.disk-dev.dsd.yandex.ru/`, если в другом дц — `https://<dc>-<vm_name>-arc.dv-dev.dsd.yandex.ru/`, где `<dc>` — название датацентра `(iva|man|myt|sas|vla)`, `<vm_name>` - название виртуальной машины в QYP.
Открывать нужно без авторизации, иначе приложение средиректит в disk-client.

## Настройка AWS для деплоя статики в S3
На данный момент статика Морды деплоится напрямую в s3.
1) Если ранее вы не получали права на деплой, то единоразово нужно запросить админские права на сервис
   ["Фронтенд Диска"](https://abc.yandex-team.ru/services/disk-frontend/) по [данной инстукции](https://wiki.yandex-team.ru/mds/s3-api/authorization/#vydachapravrobotuilisotrudniku)
2) далее необходимо получить `AccessKeyId` и `SecretAccessKey` для доступа в s3 по [данной инструкции](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys)
3) ставим утилиту aws если раньше этого не делали: `pip install awscli`
4) настраиваем aws, используя ключ из шага 2: `aws configure`

Если всё настроено верно, то следующая команда должна вернуть список бакетов:
```bash
aws --endpoint-url=http://s3.mds.yandex.net s3 ls
```

## Деплой

Чтобы задеплоить статику и загрузить sandbox-ресурс нужно:
* поднять версию в package.json
* запустить `./build-and-deploy.sh`.

Для деплоя статики необходимо:
* поставить утилиту aws (`pip install awscli`)
* получить AccessKey (о том как это сделать можно почитать выше, или [тут](https://wiki.yandex-team.ru/vertis/howto/mds-s3-howto/#poluchenieaccesskey) и [тут](https://wiki.yandex-team.ru/users/f0rmat1k/s3/))

После того как статика задеплоится и загрузится сандбокс-ресурс нужно:
* перейти в [проект в Deploy](https://deploy.yandex-team.ru/projects/disk_web_auth)
* выбрать нужный престейбл (в Stage-е `disk_web_auth_prestable` разные `prestable`-ы заведены разными DeployUnit-ами)
* нажать "Edit"
* В нужном DeployUnit-е выбираем вкладку `Disks, volumes and resources`
* В разделе `Layers` у слоя `ID: app` меняем `URL` на собранный нами ресурс
* Раскатываем через жёлтую кнопку

## Логи
[Смотреть в табличке](https://wiki.yandex-team.ru/disk/admin/disk-logs-all/#disk-front-auth-deploy)
* [логи приложения](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/ydisk-auth-www-log)
* [логи nginx](https://yt.yandex-team.ru/hahn/#page=navigation&path=//logs/ydisk-nginx-access-front-auth-log)

Быстрые логи прода смотреть с помощью [ClickHouse](https://wiki.yandex-team.ru/disk/admin/disk_clickhouse/)


## Error booster
Клиентские ошибки логируются в `error booster`
[EB морды Диска](https://error.yandex-team.ru/projects/disk-auth)

## Мониторинги
В [табличке с графиками](https://wiki.yandex-team.ru/disk/frontend/charts/) в строке `auth`

## Как настроить ассессорскую прокси
См. в [отдельной доке](../disk-client/docs/assessors.md)

## Как попадать в эксперименты
См. в [отдельной доке](../disk-client/docs/experiments.md)

## В других репах
[Докерфайл и общие настройки](https://a.yandex-team.ru/arc_vcs/disk/admin/docker/disk/clusters/disk-front-auth-deploy).
Там же есть оверрайды для престейбла. Загрузить ресурс с оверрайдами можно так:

```
ya upload -T=DISK_COMPRESSED_RESOURCE_PRESTABLE -d='disk-front-auth overrides for prestable' --owner DISK-ADMIN -A auth-front-prestable=settings --do-not-remove --tar prestable/*
```

Получить утилиту `ya` можно [так](https://wiki.yandex-team.ru/yatool/distrib/)

[Алерты в Juggler](https://a.yandex-team.ru/arc_vcs/disk/admin/yasm/alerts/disk_front_auth.jinja2)



