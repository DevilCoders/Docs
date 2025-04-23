# О библиотеке
Библиотека предоставляет собой конфигурации для чтения данных mbi-data из логброкера.

#Формат данных
Данные представлены в proto-формате
https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/proto/mbi_data_proto

## Интеграция с логброкером
Для интеграции с логброкером нужно импортировать в проект требуемые конфиги данных.

* PartnerLogbrokerConfig - изменения по партнеру;
* BusinessLogbrokerConfig - изменения по бизнесу;
* PartnerAppLogbrokerConfig - изменения по заявке на подключение(юр данных) партнера;

В проперти `market.logbroker.mbi.changes.consumerPath` указать путь до вашего консюмера.
Нужно использовать 1 консюмера на все топики.

Так же нужно указать проперти топика, данные с которого потребляются.
Например `market.logbroker.mbi.business.changes.topicPath`для данных изменения бизнеса.

Нужно создать бин GeneralLogbrokerDataProcessor с нужным generic-типом и названием.
Например `GeneralLogbrokerDataProcessor<BusinessDataOuterClass.BusinessData> businessLogbrokerDataProcessor`
для изменений по бизнесу.

# Топики логброкера, из которых получаем данные
## Прод
* [Изменения партнера](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/partner-data-changes)
* [Изменения бизнеса](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/business-data-changes)
* [Изменения юр данных партнера(заявки на подключение)](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/partner-app-data-changes)

## Тестинг
* [Изменения партнера](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/partner-data-changes)
* [Изменения бизнеса](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/business-data-changes)
* [Изменения юр данных партнера(заявки на подключение)](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/partner-app-data-changes)

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)
cd ~/arc/arcadia; ./ya ide idea --iml-in-project-root -lr ~/projects/IdeaProjects/mbi-data-integration market/mbi/mbi-data-integration
