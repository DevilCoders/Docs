
## Хаб доставки быстрых данных до репорта

### Ссылки
- [Архитектура](https://wiki.yandex-team.ru/market/development/indexer/Arxitektura-Marketnogo-Indeksatora/SaasHubandRTY/)
- [RTY в Маркете](https://wiki.yandex-team.ru/users/iddqd/rty-in-market/)
- [Как работают процессоры](https://wiki.yandex-team.ru/users/baggins/saas-hub-kak-rabotajut-processory/)
- [Вопросы и ответы](https://st.yandex-team.ru/MARKETINDEXER-31746#5dcecac58c7003001d9bf454)
- [Сервисы в Няне](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saashub_stratocaster_sas/)
- [Деплой в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/saas-stages)
- [Расследование деградаций](https://docs.yandex-team.ru/yandex-market-indexer/investigation/quick_pipelines)

### Дашборды в yasm
Белый + синий + ПШ
- https://yasm.yandex-team.ru/template/panel/Market_Saas_Hub_stable
- https://yasm.yandex-team.ru/template/panel/Market_Saas_Hub_prestable
- https://yasm.yandex-team.ru/template/panel/Market_Saas_Hub_testing/

Турбо
- https://yasm.yandex-team.ru/template/panel/Market_Saas_Hub_turbo_stable/
- https://yasm.yandex-team.ru/template/panel/Market_Saas_Hub_turbo_testing/


### Cервисы в няне
Testing
- [testing_market_saas_hub_planeshift_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_planeshift_sas/)
- [testing_market_saas_hub_planeshift_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_planeshift_vla/)
- [testing_market_saas_hub_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_sas/)
- [testing_market_saas_hub_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_vla/)
- [testing_market_saas_hub_turbo_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_turbo_sas/)
- [testing_market_saas_hub_turbo_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_saas_hub_turbo_vla/)

Prestable
- [prestable_market_saas_hub_blue_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prestable_market_saas_hub_blue_sas/)
- [prestable_market_saas_hub_blue_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prestable_market_saas_hub_blue_vla/)
- [prestable_market_saas_hub_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prestable_market_saas_hub_sas/)
- [prestable_market_saas_hub_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prestable_market_saas_hub_vla/)

Production
- [production_market_saas_hub_blue_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_blue_sas/)
- [production_market_saas_hub_blue_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_blue_vla/)
- [production_market_saas_hub_planeshift_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_planeshift_sas/)
- [production_market_saas_hub_planeshift_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_planeshift_vla/)
- [production_market_saas_hub_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_sas/)
- [production_market_saas_hub_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_vla/)
- [production_market_saas_hub_turbo_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_turbo_sas/)
- [production_market_saas_hub_turbo_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_saas_hub_turbo_vla/)

### Prestable
1. Кросс-дц
   - по одному синему и белому контейнеру в каждой локации
   - для плейншифта нет prestable
1. Конфиг
   - общий со stable
   - отличие в настройках задается через env конфиг
1. Стейт
   - репортовый saas-kv общий со stable
   - idxapi saas-kv общий со stable в каждой локации
1. Данные топиков
   - отдельный от stable consumer для каждого топика
   - чтение без зеркалирования пятью процессорами
   - дедупликация аналогичная stable
   - данные топиков не пишутся в saas-kv
   - часть данных дропается на входе из-за пониженной мощности в сравнении со stable
   - процент обрабатываемых данных задается в конфиге, выбор рандомным способом
   - данные топиков отправляются только в shadow репорт
1. Данные NEH источников (белый фидпарсер)
   - prestable и stable хаб находятся под общим балансером в локации
   - активный/резервный парсер совпадает по местоположению с мастером белой индексации, которое обычно равно stable/prestable среде индексатора
   - активный/резервный парсер определяется по флагу IsActiveCluster внутри принимаемых данных, флаг проставляется самим парсером
   - данные активного фидпарсера пишутся в saas-kv и отправляются в stable репорт
   - данные резервного фидпарсера не пишутся в saas-kv и отправляются в shadow репорт, аналогично поведению stable хаба
1. Проверки
   - проверка живости prestable хаба
   - проверка графиков и мониторингов prestable хаба
   - мониторинги shadow репорта: ошибки, наличие потока
   - интеграционные проверки запросов в shadow репорт
1. Релизы
   - отдельные стадии prestable/stable
   - выкатка во все локации одновременно не зависит от среды индексатора
1. Дополнительно
   - не защищает от роста объема или потери части данных из топиков
   - не защищает от неправильной обработки событий фидпарсера, потому что они будут записаны в kv и отправлены на репорт для активного фидпарсера
   - при выкатке парсера данные prestable среды парсера не пишутся в kv и отправляются только на shadow репорт
