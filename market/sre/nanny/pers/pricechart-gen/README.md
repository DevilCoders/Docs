# Market Pricechart-gen

## Documentation

## Services
[Service Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pricechart/)
Services Balancer(testing): [pricechartgen-testing.n.yandex-team.ru](https://pricechartgen-testing.n.yandex-team.ru)
Services Balancer(production): [https://pricechart-gen.yandex.net/](https://pricechart-gen.yandex.net/)

## Sandbox tasks
### Build tasks
[BUILD_PORTO_LAYER](https://sandbox.yandex-team.ru/tasks/?order=-updated&type=BUILD_PORTO_LAYER) with the following options:
[Example: https://sandbox.yandex-team.ru/task/105453862/view](https://sandbox.yandex-team.ru/task/105453862/view)

### Update service
не надо делать этого, но если всё таки очень надо, то
1. меняем нужный код в https://github.yandex-team.ru/market-java/pricechart/tree/master/pricechart-gen
2. апаем версию в debian/changelog 
3. собираем пакет и заливаем его в репу market
4. далее пакет должен оказаться в ветке stable 
5. используя таску https://sandbox.yandex-team.ru/task/105453862/view собираем новый porto_layer
6. если что-то менялось в https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/pers/pricechart-gen/pkg.json то нужно ещё пересобрать конфиги через https://sandbox.yandex-team.ru/task/95628387/view=380
7. после удачного выполнения таски из п.5(или 6) нажимаем наверху кнопку "Release" и выбираем тестинг(это действие проставит бесконечное время хранения созданного ресурса)
7. берём полученный resource id из п.5 -> идём в сервис на вкладку instance spec(пример https://nanny.yandex-team.ru/ui/#/services/catalog/testing_pricechart_gen_sas/instance_spec) -> находим "List of layers to assemble instance FS" -> удаляем текущий "Top layer" -> вбиваем Resource id в поле ниже и нажимаем Add -> нажимаем Save(на вкладке Runtime слева)
8. в главном окне(пример https://nanny.yandex-team.ru/ui/#/services/catalog/testing_pricechart_gen_sas/) нажимаем Change на самом верхнем(?табе/контроле/хз?) -> нажимаем Active, пишем комментарий и ставим галочку "Set snapshot as current" -> Apply
9. по кнопке Instances можно увидеть статус развёртывания(два последних столбца должны быть Active Active)
10. проверяем, что поднялось -> повторяем для каждого из https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pricechart/

### Auxiliary tasks
[HTTP_UPLOAD](https://sandbox.yandex-team.ru/tasks/?type=HTTP_UPLOAD&page=1&pageCapacity=20&forPage=tasks) with the following options:
[Example: https://sandbox.yandex-team.ru/task/94145245/view](https://sandbox.yandex-team.ru/task/94145245/view)


[MARKET_YA_PACKAGE](https://sandbox.yandex-team.ru/tasks/?type=MARKET_YA_PACKAGE&page=1&pageCapacity=20&forPage=tasks)
[Example: https://sandbox.yandex-team.ru/task/95628387/view](https://sandbox.yandex-team.ru/task/95628387/view)

## Dashboards
[HQ Panel](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_pricechart/hq-panel/)
