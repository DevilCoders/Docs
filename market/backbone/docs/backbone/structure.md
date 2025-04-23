# Организация
Все монолиты маркета (Репорт, Фронт, ...) должны быть разделены на ряд микросервисов, обеспечивающих текущую функциональность.

Микросервисы распадаются на два подмножества: базовые сервисы (backbone) и продуктовые сервисы (fastbone).

## Базовые сервисы (backbone)
Должны:
- быть консервативными для внесения изменений и как следствие стабильными
- быть хорошо и быстро масштабируемыми, в т.ч. при пиках нагрузки
- поддерживаться инфраструктурными командами Маркета
- периодически валидироваться по выполнению инфраструктурных SLA
- не зависеть и не блокировать развитие продуктовых сервисов

Могут:
- ходить в продуктовый, но доступность последнего не должна влиять на функционирование базового
- продуктово расширять свой функционал через конфиги
- продуктово расширять свой функционал через данные, если это не существенно влияет на производительность backbone-сервисов
- не стоять на критическом пути


## Продуктовые сервисы (fastbone)
Должны:
- обладать высоким ТТМ
- отключаться при нарушении инфраструктурных SLA (скорость, доступность) без значимой просадки бизнесовых SLA
- не влиять существенным образом на функционирование базовых сервисов (DDoS, OOM)
- поддерживаться продуктовыми командами Маркета

Могут:
- обладать пониженной стабильностью
- ходить в Базовые сервисы
- ходить в другие продуктовые сервисы, но рекомендуется иметь фолбек-сервис на случай недоступности основного продуктового сервиса
- могут переходить в базовые с передачей поддержки инфраструктуре по согласованию (напр. стали консервативными)


## Fallback-сервисы
Fallback-сервисы служат для подстраховки работы основного функционала. Могут быть использованы как в рамках продуктовых сервисов, так и базовых. Рекомендовано использовать ApiProxy для реализации фолбеков, но у фронтов есть своя специфика, т.ч. допускается фронтовая реализация.

## ApiProxy
[ApiProxy](https://wiki.yandex-team.ru/taxi/backend/architecture/apiproxy/) – таксишная реализация паттерна ApiGateway.

Его использование в Backbone-архитектуре двояко:
1. Для организации фоллбеков (как выше отмечалось)
2. Для интеграции API, т.е. сервис виджета дергает ручку ApiProxy, а ApiProxy дергает множество сервисов и компанует результат. Т.о. backend-сервисы не должны проксировать через себя данные, только идентификаторы, а резолвом идентификаторов в rich-представление займется оконченый ApiProxy

<iframe height="446px" width="100%" frameborder="0" src="https://viewer.drawio.yandex-team.ru/?lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Untitled%20Diagram.drawio#R5Vltc6IwEP41zNx90AEiSD9WbXsvvZne9Wbu%2BukmQsC0SJgY3%2FrrbwOJQFFrW5W%2B6AfJZnchu%2Fs82aCB%2BuPFBcfp6AcLSGzYZrAw0MCwbcvs2PAjJctc4npOLog4DZRSIbim90RbKumUBmRSURSMxYKmVaHPkoT4oiLDnLN5VS1kcfWuKY5ITXDt47gu%2FUMDMcqlnt0t5F8IjUb6zpZ7ks%2BMsVZWK5mMcMDmJRE6M1CfMybyq%2FGiT2IZPB2XNPxlfTXv%2FqHJ%2FQUNku8%2Fv53%2FbuXOzp9isloCJ4nYr2tXLU0sdbxIAOFTQ8bFiEUswfFZIe1xNk0CIr2aMCp0LhlLQWiB8JYIsVS1gKeCgWgkxrGaJQsq%2Fkrztu2o4U1parBQrrPBUg8SwZdlKzm%2BKU8WdtlIG%2BYrlMt6UBCPRFPpTdiU%2B2SLnsKHwDwi2%2FyhVckA1ggbE3hIsOMkxoLOqg%2BHVdFHK70isXChcvuEPKtqn%2BF4qu4U0iQACRveStStq4JLPAQuqGQOxzRK4NqH0BEOghnhggLYTtXEmAZBXiRkQu%2FxMPMns5AymohsVU7PcAarvEgHZGGsYQJlXODv0Yy56yOsvLfMtoUQyn3tHHXl7ko%2BfkmFheGEiFpaVnd9fqbsWqaAtmRlQX4In1GoRduNIQy9IYerSF5BTM85g5RASp1BLZlVwM5HVJDrFGdFPQfSr6Y4pHHcZzHjmS0KMPFCH%2BQTwdkdKc24vkeG4bZE7gaxjQlDegvRO48azgsat3RtjEoUrvX2DiKvCbI8NH2hHemr0yR9nXwE%2BvK2osFsI9NxK4CwXjuXWXaz7UX3Oe1Fpbdor1qNhrqLXeHpNAlPC9XwSYOWYK0Ej8n7AGdeylvQCfuV8zI86j5Fo%2BYI%2BGy4%2Fa%2Fg09wRn8pKQ9R6IwDdUD9HAmi9%2F9c7p%2FkJLG1wa0qwfn4naN1%2BFDDbpuV2K3tp64Wbqd6SH1gcDrt1yj1N6RVni2UthS%2Fp%2F0NHftf2%2F9lHWsDJoyTPP0c8F1he0wcD%2FUDN8KhVJtG2syuN2q%2BKRjs70mijb1E0ums02pIc%2Bi6I01wf3%2BIdiu0%2BYM49EeexeLNTS2EP%2B3ckO03OKfCHbcYsov7atyxadd8vWRziBZ11JOvZQ5SR7KHI1HKrZGqfNE6mnWab0mf0pJbxqs6MzpvgUmdzS%2FqOjo0bXpuVjo17bUMPz5%2F1tA2wwNB7fhDC7HSPR5gwLP5ezBNY%2FEmLzv4D"></iframe>

## DataApi-сервисы
Класс сервисов, который не содержит бизнес-логики, а служит просто интерфейсом предоставления данных по идентификаторам сущностей

## Frontend vs Backend
Взаимодействие происходит через ApiProxy, никакой фронтенд сервис не должен знать никакого другого endpoint'a бекенда, кроме ApiProxy. Т.о. достигается изоляция взаимодействия по интерфейсу и независимая разработка фронтов и бекенда. ApiProxy находится в области отстветственности команды бекенда.
