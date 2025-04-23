# Поисковое приложение

Это nodejs-приложение для:
* встраивания вертикали Автору в Поисковое Приложение (ПП) Яндекса - https://st.yandex-team.ru/AUTORUFRONT-12133
* ручки для блока Автору на веб морде Яндекса - https://st.yandex-team.ru/AUTORUFRONT-13462
* блок журнала на морде - https://st.yandex-team.ru/AUTORUFRONT-15687
* ручка для подмешивания в Объявления (o.yandex.ru) - https://st.yandex-team.ru/VTF-349

## Состав вертикали

### Веб-вью для ПП Яндекса

* прод: https://search-app.auto.ru/
* тестинг: https://search-app.test.avto.ru/
* дев: https://search-app.{ ваша виртуалка }/
* макеты: https://www.figma.com/file/bTMpbxswZ7yhzqY4KHHg4lac/YandexSearchApp

Гайды в поиске другие, поэтому многие компоненты скопированы в ПП.

### Ручка для веб морды

* прод: https://search-app.auto.ru/api/1.0/inserts/morda/?region_id=213
* тестинг: https://search-app.test.avto.ru/api/1.0/inserts/morda/?region_id=213
* дев: https://search-app.{ ваша виртуалка }/api/1.0/inserts/morda/?region_id=213

### Ручка для веб морды div2

* прод: https://search-app.auto.ru/api/1.0/listing-morda-data/?geoid=213
* тестинг: https://search-app.test.avto.ru/api/1.0/listing-morda-data/?geoid=213
* дев: https://search-app.{ ваша виртуалка }/api/1.0/listing-morda-data/?geoid=213

### Ручка для ПП Яндекса

* прод: https://search-app.auto.ru/api/1.0/app-morda-data/?geo_id=213
* тестинг: https://search-app.test.avto.ru/api/1.0/app-morda-data/?geo_id=213
* дев: https://search-app.{ ваша виртуалка }/api/1.0/app-morda-data/?geo_id=213

### Ручка для блока журнала

* прод: https://search-app.auto.ru/api/1.0/mag-morda-data/
* тестинг: https://search-app.test.avto.ru/api/1.0/mag-morda-data/
* дев: https://search-app.{ ваша виртуалка }/api/1.0/mag-morda-data/

### Ручка для объявлений (o.yandex.ru)

* прод: https://search-app.auto.ru/api/1.0/classified-data/?geo_id=213&platform=desktop&limit=15&imgSize=272x272&imgSizeRetina=456x342
* тестинг: https://search-app.test.avto.ru/api/1.0/classified-data/?geo_id=213&platform=desktop&limit=15&imgSize=272x272&imgSizeRetina=456x342
* дев: https://search-app.{ ваша виртуалка }/api/1.0/classified-data/?geo_id=213&platform=desktop&limit=15&imgSize=272x272&imgSizeRetina=456x342

Для корректной работы необходимо указать заголовок x-yandexuid: <number>Yandexuid

## Деплой

Сборка контейнера в [TC](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_Applications_AuroRuFrontendRepo_ReleaseShivaAfSearchApp?mode=branches).
Собираем из ветки задачи, которую собираемся катить.
После сборки контейнер автоматически выкладывается в тестинг.
За статусом выкладки можно следить, подписавшись на уведомления в телеграмм-ботике ***vertis_shiva_bot***.
Там же можно выкладывать в прод согласно [доке](https://wiki.yandex-team.ru/vertis-admin/deploy/).
Если после выкладки всё Ok, не забываем мержить изменения в мастер.

## Логи

Посмотреть логи можно в grafana ([тест](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Daf-search-app%20layer%3Dtest%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D), [прод](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Daf-search-app%20layer%3Dprod%20(level%3Dwarn%20or%20level%3Derror%20or%20level%3Dfatal)%20context!%3DpublicApiPersonalization%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D)).

[Графики скорости ответа со стороны ПП](https://yasm.yandex-team.ru/menu/Portal/Geohelper/geohelper/?chart=autoru%20times)

[Графики с нашей стороны](https://grafana.vertis.yandex-team.ru/d/000000595/autoru-nodejs-frontends?orgId=1&var-datasource=Prometheus&var-job=af-search-app&var-dc=All&var-group=All)

## Design doc

В это приложение ходит вся веб-морда (десктоп и тач) и ПП, поэтому в пике на приложение приходится 4000 rps.
При этом SLA ответа должен быть 300ms. Основная нагрузка приложения - поисковые пресеты с укрупнением региона (город -> область -> страна).
Из-за того, что наш поиск не может выдержать такой SLA (для поиска по всей России ответ может быть больше секунды),
поисковые пресеты подготавливаются и кешируются в YDB.

Приложение разделено на 2 части:
* `search-app` - забирает подготовленные поисковые пресеты из YDB и отвечает внешним потребителям
* `search-app-updater` - ходит в поиск, подготавливает поисковые пресеты, сохраняет их в YDB.

Пресеты подготавливаются только для крупных регионов! Для деревень их готовить не имеет смысла и можно сразу укрупняться до области.

## Как работает `search-app-updater`

Справочник всех доступных пресетов хранится в бункере по адресу (https://bunker.yandex-team.ru/auto_ru/search-app/presets?view=raw).
Конфигурация, которая позволяет определить выдачу пресета для определенной платформы (https://bunker.yandex-team.ru/auto_ru/search-app/configuration?view=raw)
Структура спроектирована так, что для каждой части (app, web-desktop, web-mobile) может быть свой набор пресетов и свое количество объявлений.

В качестве списка регионов берется страна, федеральные округа, субъекты федерации, столицы субьектов и [список больших городов](https://st.yandex-team.ru/AUTORUFRONT-13765).
Получается ~1000 регионов, для которых будут подготовлены пресеты.

Обновление пресетов запускается после старта приложения и дальше раз в час.
Для каждого пресета подготавливается не больше N объявлений, указанных в настройке пресета.

**ВАЖНО**: нельзя просто взять и увеличивать количество объявлений, это напрямую влияет на скорость работы сервиса.
По результатам стрельб оптимальным лимитом является 15 объявлений.

## Как работают пресеты в `search-app`

Входящий geo_id всегда проверяется на вхождение в список доступных регионов.
Если его нет в списке, то происходит укрупнение до субъекта федерации или страны.
Если geo_id не из России, то всегда запрашиваем Россию.

Пресеты запрашиваются для всей цепочки регионов (город -> субъект федерации -> страна) и склеиваются до тех пор,
пока не наберется достаточное количество объявлений.
Таким образом, если в городе есть достаточное количество объявлений, то объявлений из укрупнения приклеены не будут.
После этого объявления перемешиваются и обрезаются до нужного количества, чтобы создавать видимость постоянного обновления.

## Что делать, если надо поменять набор пресетов?

Если необходимо, нужно добавить новый пресет в бункер в настройки пресетов (https://bunker.yandex-team.ru/auto_ru/search-app/presets?view=raw),
затем поменять набор пресетов для конкретной части (https://bunker.yandex-team.ru/auto_ru/search-app/configuration?view=raw).
Проверить валидность параметров в бункере можно ручкой  https://search-app.test.avto.ru/api/1.0/presets-validate/ - отображаются только пресеты,
которые есть в конфигурации. В бункере у любой ноды есть состояние сохранен (test) и опубликован (dev), так что не бойтесь сохранять,
но сохраняйте осторожность при публикации данных о пресетах и обязательно проверяйте предварительные результаты на стендах и в тестинге.
В течение часа сформируется новый кеш для новых пресетов и `search-app` начнет их отдавать.
