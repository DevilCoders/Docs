# Метрика промо 2016 [![Build Status](http://drone-beta.haze.yandex.net/api/badges/Metrika/promo-merika-2016/status.svg)](http://drone-beta.haze.yandex.net/Metrika/promo-merika-2016)

Продакшн - https://metrika.yandex.ru/about

## Танкер

https://tanker.yandex-team.ru/?project=promo-metrika-2016
Для импорта ключей нужно использовать команду

    npm run i18n

## Бункер

https://bunker.yandex-team.ru/promo-metrika-2016
Ключи импортируются автоматически в зависимомти от окружения выставляется период автообновления ключей
На dev среде период самый мальенький на проде самый больщой

#### Инструкция по работе с Бункером

https://wiki.yandex-team.ru/sales/marketing/advertising/howto/

#### Настройка бункера

https://wiki.yandex-team.ru/verstka/tools/bunker/stuff/

https://bunker.yandex-team.ru/.schema/json-schema-draft-03?view=raw

## Запуск проекта

Для сборки и старта в статичком режиме

    npm start

Для сборки с стара с автоматической презагруской и пересборкой при изменении кода

    npm run watch

Если проект развернут на машине разраработки метрики metrika-dev01it.mtrs.yandex.ru
И лежит в папке ~/www/promo

То он станет видимым по url

    https://promo-<UserName>.metrika-dev.haze.yandex.ru

где UserName - имя пользователя от чьего имени запушенно приложение

## Как собирать релиз вручную

Сначала нужно создать отдельную бранчу для релиза формы `release-<version>` ( пример: `release-0.17` ).

Затем нужно обновить [./debian/changelog](./debian/changelog) файл. На линуксе это можно сделать cli тулой,
но главное чтобы файл начинался с:

```
promo-metrika-2016 (<version>) testing; urgency=medium

  *

 -- Eric Cartman <robot-metrika-test@yandex-team.ru>  <date>

```

`<version>` должен быть номером версии релиза, например `0.17.0` ( заканчивается на `.0` НЕ как в имени бранчи ).
`<date>` должно быть будущей датой типа: `Thu, 26 Dec 2019 23:40:00 +0300`.

Затем нужно пойти ( и залогиниться ) на https://jenkins.metriqa.yandex.ru.

Выбрать Frontend ( https://jenkins.metriqa.yandex.ru/view/Frontend/ ), затем Promo Release.

В левой части страницы нужно выбрать Build with Parameters и там указать имя релизной бранчи которую мы создали ранее
( в нашем примере это `release-0.17` ). Затем нажать Build. В левом нижнем углу появится таска и ее прогресс.

Когда build завершиться готовый пакет можно посмотреть на https://c.yandex-team.ru/packages. Имя пакета
можно посмотреть в этом репозитории, в [./debian/control](./debian/control).
