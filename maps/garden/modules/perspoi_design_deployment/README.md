# perspoi_design_deployment

## Описание модуля
Модуль тестирует и активирует датасет [yandex-maps-perspoi-design](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-perspoi-design/versions).

## Как происходят релизы
После сборки модуля [renderer_map_stable_bundle](https://garden.maps.yandex-team.ru/stable/renderer_map_stable_bundle)
возникает два релиза в модуле [perspoi_design_deployment](https://garden.maps.yandex-team.ru/stable/perspoi_design_deployment)
c шагами `testing` и `stable`. На шаге `testing` датасет заливается в `testing`
ветку ecstatic и попадает на [datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_personalized_poi_renderer_datavalidation)
рендерера персональных POI. После этого производится обстрел этого окружения -
проверяется, что для известных тестовых пользователей отдаётся нормальное
количество POI. После завершения шага `testing` автостартер запускает шаг
`stable` - на этом шаге уже нет валидации, и датасет просто активируется в
`stable` ветке ecstatic и попадает уже в основные окружения [рендерера персональных POI](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/renderer#pro-okruzheniya).

## Как откатить релиз/выкатить релиз без валидации
Для этого надо просто вручную запустить нужный билд с шагом (deploy step)
`stable`. Валидации происходить не будет, и датасет сразу активируется в
`stable` ветке ecstatic.
Автостартер на ручные запуски `perspoi_design_deployment` отключен, поэтому
если откатываемся с билда N + 1 на билд N, то после завершения билда N билд
N + 1 автостартером запущен не будет.
