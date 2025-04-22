# API сервиса моделей для цезаря
## Царь-модели
TODO
## Фразовые модели
Как пользоваться.
### 1. Катнуть нужные модели на фразовые шарды сервиса моделей:
  * hamster (для dev-контура): [SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/sas_caesar_phrase_models_hamster/) и [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_caesar_phrase_models_hamster/)
  * prod (для prestable и prod): [SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/sas_caesar_phrase_models/) и [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/vla_caesar_phrase_models/)

Сейчас раскатана только [одна модель](https://st.yandex-team.ru/BIGB-1389#6019937332033277d2dfef1e)

_Примечание_: формат конфига фразового шарда в транке иногда меняется при выкладке надо проверить, что он соответствует [этому описанию](https://a.yandex-team.ru/arc/trunk/arcadia/search/begemot/rules/yabs_caesar_models/caesar_phrase_models/config/caesar_phrase_models_rule.cfgproto).

### 2. Поправить конфиг цезаря
  * Добавить идентификаторы доступных моделей в [конфигурацию графа](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/samogon/caesar/plugin/workers.py?rev=r7901671#L650) по аналогии с конфигурацией моделей в [баннерном графе](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/samogon/caesar/plugin/workers.py?rev=r7901671#L106).
  * Если не включен поход в сервис моделей, включить [этим параметром](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/samogon/caesar/plugin/workers.py?rev=r7901671#L646).
