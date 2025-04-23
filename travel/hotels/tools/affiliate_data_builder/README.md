# Подготовка данных для партнёрской программы

## Конфигурация комиссии для партнёров и пользователей

Конфигурация задаётся через [cfg_tool](https://docs.yandex-team.ru/travel/services/hotels/cfg_tool). Можно задавать разные настройки для прода и для тестинга

### Партнёры
[формат](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/proto/data_config/affiliate/affiliate_partner.proto)
| [исходники](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/affiliate_partners.config)
| [YT тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/config/affiliate_partners)
| [YT прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/config/affiliate_partners)
| [результат тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/general/affiliate_data/commission_config/latest/affiliate_partners)
| [результат прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/affiliate_data/commission_config/latest/affiliate_partners)

Здесь задаются допустимые параметры для каждого партнёра. Далее они используются для подстановки значений в параметры со значением "*".

### Комиссия для партнёров
[формат](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/proto/data_config/affiliate/affiliate_partner_commission_item.proto)
| [исходники](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/affiliate_partner_commission.config)
| [YT тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/config/affiliate_partner_commission)
| [YT прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/config/affiliate_partner_commission)
| [результат тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/general/affiliate_data/commission_config/latest/affiliate_partner_commission)
| [результат прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/affiliate_data/commission_config/latest/affiliate_partner_commission)

Основной конфиг, в котором указывается комиссия для всех партнёров

### Комиссия для пользователей
[формат](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/proto/data_config/affiliate/affiliate_user_commission_item.proto)
| [исходники](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/config/cfg_tool/affiliate_user_commission.config)
| [YT тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/config/affiliate_user_commission)
| [YT прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/config/affiliate_user_commission)
| [результат тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/general/affiliate_data/commission_config/latest/affiliate_user_commission)
| [результат прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/affiliate_data/commission_config/latest/affiliate_user_commission)

Позволяет переопределить комиссию для отдельных пользователей

### Правила построения конфига

* Разворачиваются списки и значения равные "*"
* Отбрасываются все строки, для которых не подходят даты
* Применяется переопределение по ключу (ключ описан в файле с форматом конфига). Следующее значение всегда заменяет предыдущее

### История изменений
Если построенный конфиг отличается от предыдущего, он сохраняется в папку с текущей датой. Ссылка `latest` ([тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/testing/general/affiliate_data/commission_config/latest), [прод](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/affiliate_data/commission_config/latest)) всегда указывает на актуальную версию конфига
